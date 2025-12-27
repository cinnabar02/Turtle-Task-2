# Turtle Task 2
## Упражнение №1. Броуновское движение
```python
import turtle as t
import random

t.shape('turtle')
t.speed(0)

for _ in range(500):
    t.forward(random.randint(5, 100))
    if random.randint(0, 1) == 1:
        t.right(random.randint(0, 360))
    else:
        t.left(random.randint(0, 360))

t.done()
```

## Упражнение №2. 