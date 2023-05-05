```python
from threading import Lock, Condition
import threading
import time

class TrafficLight:
    def __init__(self):
      self.green_on = 1          # 1 or 2 for Road A or B
      self.car_crossing = 0    # Keep track of current number of crossing car
      self.cv = Condition(Lock())

    def carArrived(
      self,
      carId: int,                      # ID of the car
      roadId: int,                     # ID of the road the car travels on. Can be 1 (road A) or 2 (road B)
      direction: int,                  # Direction of the car
      turnGreen: 'Callable[[], None]', # Use turnGreen() to turn light to green on current road
      crossCar: 'Callable[[], None]'   # Use crossCar() to make car cross the intersection
    ) -> None:
        print("Thread:", threading.get_ident())

        cv = self.cv
        with cv:
        # Check other road for crossing car count
            if self.green_on != roadId:
                while self.car_crossing > 0:
                    cv.wait()
        # It now safe to request light siwtch to current road
                self.green_on = 1 if self.green_on == 2 else 2
                turnGreen()

        with cv:
            self.car_crossing += 1 

        crossCar()

        with cv:
            self.car_crossing -= 1
            if self.car_crossing == 0:   # When all car crossed, notify other road so they can cross.
                cv.notify_all()
```