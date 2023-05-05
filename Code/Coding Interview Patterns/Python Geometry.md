#### Point class and finding center/mid-point
```python
class Coord:
    x: float
    y: float

    def __init__(self, p1, p2) -> None:
        self.x = p1
        self.y = p2

    def __repr__(self) -> str:
        return str(vars(self))

    def __eq__(self, __o: "Coord") -> bool:
        return __o and \
            __o.x == self.x and __o.y == self.y

    @classmethod
    def calcCenter(clz, c1, c2: "Coord") -> "Coord":
            print("centering", c1, c2, end="=")
            return Coord(
                (c1.x + c2.x)/2,
                (c2.y + c2.y)/2)

```

#### Find a bounding box
```python
       def findCenters(coords: List[Coord]) -> Coord:
			xs = [c.x for c in coords]
            ys = [c.y for c in coords]
            retCoord = Coord.calcCenter(
                Coord(min(xs), min(ys)),
                Coord(max(xs), max(ys)))
            
            return retCoord

```