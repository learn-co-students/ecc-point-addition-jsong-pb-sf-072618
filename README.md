# Point Addition

The main reason that Elliptic Curves are useful is because of something called Point Addition.

It turns out that for every elliptic curve, a line will intersect at either 1 or 3 points.

The two exceptions are when a line is _tangent_ to the curve and when a line is exactly vertical.

We will come back to these two cases later.

What's interesting is that we can define something called *point addition* using this fact. Like with Field Addition, we define point addition ourselves. In our case, point addition is defined this way:

For any two points P~1~=(x~1~,y~1~) and P~2~=(x~2~,y~2~), we get P~1~+P~2~ by:

* Find the point intersects the elliptic curve a third time by drawing a line through P~1~ and P~2~
* Reflect the resulting point over the x-axis

As you can see, point addition is not easily predictable. We can calculate point addition easily enough with a formula, but intuitively, the result of point addition can be almost anywhere given two points on the curve. That is, point addition is non-linear.

### Math of Point Addition

The reason why we have "addition" in the Point Addition name is that Point Addition satisfies certain properties that we think of as addition. Specifically, addition has these properties:

* Identity
* Commutativity
* Associativity
* Invertibiltiy

Identity here means that there's a zero. That is, there exists some point (I) which when added to a point (P) results in P. We'll call this point the point at infinity (reasons for this will become clear in a bit). That is:

I + P = P

This is also related to invertibility. For some point P, there's some other point -P which results in the Identity point. That is:

P + (-P) = I

Visually, these are points opposite each other in the elliptic curve.

This is why we call this point the point at infinity. We have one extra point in the elliptic curve which makes the vertical line intersect a third time.

Commutativity means that P+Q=Q+P. This is obvious since the line going through P and Q will intersect the curve a third time in the same place no matter what order.

Associativity means that (P+Q) + R=P + (Q+R). This isn't obvious and is the reason for flipping over the x-axis.


### Exercise

#### For the curve \\(y^2 = x^3 + 5x + 7\\), what is \\((2,5) + (-1,-1)\\)?

```python
# Exercise 6.1

x1, y1 = (2,5)
x2, y2 = (-1,-1)
# formula in python:
# s = (y2-y1)/(x2-x1)
# x3 = s**2 - x2 - x1
# y3 = s*(x1-x3)-y1
```

### Exercise

#### For the curve \\(y^2 = x^3 + 5x + 7\\), what is \\((-1,1) + (-1,1)\\)?

```python
# Exercise 7.1

a, b = 5, 7
x1, y1 = -1, -1

# formula in python
# s = (3*x1**2+a)/(2*y1)
# x3 = s**2 - 2*x1
# y3 = s*(x1-x3) - y1y3 = s*(x1-x3) - y1
```

### Add the `__add__` method to your library:

```python
from ecc import Point

class Point:

    def __add__(self, other):
        if self.a != other.a or self.b != other.b:
            raise RuntimeError('Points {}, {} are not on the same curve'.format(self, other))
        # Case 0.0: self is the point at infinity, return other
        # Case 0.1: other is the point at infinity, return self

        # Case 1: self.x == other.x, self.y != other.y
        # Result is point at infinity
        # Remember to return an instance of this class:
        # self.__class__(x, y, a, b)

        # Case 2: self.x != other.x
        # Formula (x3,y3)==(x1,y1)+(x2,y2)
        # s=(y2-y1)/(x2-x1)
        # x3=s**2-x1-x2
        # y3=s*(x1-x3)-y1
        # Remember to return an instance of this class:
        # self.__class__(x, y, a, b)

        # Case 3: self.x == other.x, self.y == other.y
        # Formula (x3,y3)=(x1,y1)+(x1,y1)
        # s=(3*x1**2+a)/(2*y1)
        # x3=s**2-2*x1
        # y3=s*(x1-x3)-y1
        # Remember to return an instance of this class:
        # self.__class__(x, y, a, b)
```
