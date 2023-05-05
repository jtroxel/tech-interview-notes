Shopping Cart Abandonment

**Key Points**
- Need to log users by guid to update last time?
- Need to access all used by date < something
-

```python
'''
Track events for users and periodically generate a list of users potentially abandoning their cart

Event:
- UUID: user id string
- action:  ["product_viewed", "added_to_cart", "checkout_started", "checkout_complete"]

tracking API:
  captureUserEvent(ev: Event)

abandoned cart detection API
  getAbandonedCartUsers(time: minutes)

Approach
  capture and hold data for events
  DS should allow getting users where last-event-timestamp < time limit
    - Need to get the timestamps less than now() - time-limit
    - Need users with last-timestamp in that list

    - A filter on a normal dict could scan all

    - If we pretend to write to a timeseries db or time-partitioned WH, it would look like
      just writing every event
      - with streaming api could aggregate over window
       - simulate that with a replacing with last
      lastUserActivity: dict[timestamp] -> uuid
        - ordered on timestamp
        - iterate in reverse, faster than scan?



'''
from threading import Timer
import time
from datetime import datetime, timedelta
from collections import OrderedDict
from dataclasses import dataclass
from enum import Enum

@dataclass
class Event:
    uuid: str = None
    action: str = None


class Abandonment:
    lastUserActivity: OrderedDict[str]

    def __init__(self):
        self.lastUserActivity = OrderedDict()

    def captureUserEvent(self, ev: Event):
        nowish = time.time()
        self.lastUserActivity[ev.uuid] = nowish
        self.lastUserActivity.move_to_end(ev.uuid)
        print(datetime.fromtimestamp(nowish), self.lastUserActivity)

    def getAbandonedCartUsers(self, in_last: int) -> list[str]:
        nowish = time.time()
        before_dt: datetime = (datetime.fromtimestamp(nowish) + timedelta(seconds=-in_last))
        print(datetime.fromtimestamp(nowish), in_last, before_dt)
        before = before_dt.timestamp()
        last_first = reversed(self.lastUserActivity)
        print("check before", datetime.fromtimestamp(before), [u for u, e in self.lastUserActivity.items()
                                                               if e <= before])
        return [abandoned_user for abandoned_user in [u for u, e in self.lastUserActivity.items()
                                                      if e <= before]]


class Actions(Enum):
    VIEWED = "product_viewed"
    ADDED = "added_to_cart"
    CO_STARTED = "checkout_started"
    CO_COMPLETE = "checkout_complete"


c = Abandonment()

c.captureUserEvent(Event(uuid="abcd1234", action=Actions.ADDED.value))
c.captureUserEvent(Event(uuid="abcd1234", action=Actions.ADDED.value))
time.sleep(1)

c.captureUserEvent(Event(uuid="qwer4321", action=Actions.ADDED.value))
c.captureUserEvent(Event(uuid="xyzz9999", action=Actions.ADDED.value))

test = c.getAbandonedCartUsers(0)
assert set(test) == set(["xyzz9999", "qwer4321", "abcd1234"]), str(test)

time.sleep(5)
test = c.getAbandonedCartUsers(6)
assert test == ["abcd1234"], str(test)

# Running the detection on a schedule:
def schedule():
    # Note for real use-case, use 4*60 or whatever, for minutes as seconds
    Abandonment().getAbandonedCartUsers(1)
    # do something with foo
    Timer(0.5, schedule).start()

schedule()
c.captureUserEvent(Event(uuid="qwer4321", action=Actions.ADDED.value))
time.sleep(1)
c.captureUserEvent(Event(uuid="xyzz9999", action=Actions.ADDED.value))
c.captureUserEvent(Event(uuid="qwer4321", action=Actions.ADDED.value))
c.captureUserEvent(Event(uuid="xyzz9999", action=Actions.ADDED.value))





