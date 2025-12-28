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

## Упражнение №2. Почтовый индекс
```python
import turtle

t = turtle.Turtle()
t.shape("turtle")
t.speed(0)

STEP = 30

MOVES = {
    "U":  (0, STEP),   "D":  (0, -STEP),
    "L":  (-STEP, 0),  "R":  (STEP, 0),
    "UL": (-STEP, STEP), "UR": (STEP, STEP),
    "DL": (-STEP, -STEP), "DR": (STEP, -STEP)
}

DIGITS = {
    "0": ["PD","D","D","R","U","U","L","R"],
    "1": ["PU","D","PD","UR","D","D","U","U"],
    "2": ["PD","R","D","L","D","R","L","U","R","U"],
    "3": ["PD","R","DL","R","DL","UR","L","UR"],
    "4": ["PD","D","R","U","D","D","U","U"],
    "5": ["PD","D","R","D","L","R","U","L","U","R"],
    "6": ["PD","D","D","R","U","L","U","R"],
    "7": ["PD","R","DL","D","U","UR"],
    "8": ["PD","D","D","R","U","L","U","R","D","U"],
    "9": ["PD","D","R","DL","UR","U","L","R"]
}

ACTIONS = {
    "PU": t.penup,
    "PD": t.pendown
}


def draw_digit(d):
    for a in DIGITS[d]:
        if a in ACTIONS:
            ACTIONS[a]()
        else:
            dx, dy = MOVES[a]
            t.goto(t.xcor() + dx, t.ycor() + dy)


def draw_number(text):
    for d in text:
        draw_digit(d)
        t.penup()
        t.forward(STEP * 1.5)


t.penup()
t.goto(-250, 0)
draw_number("141700")

turtle.done()
```
##
### Упражнение №3. Почтовый индекс 2
```python
import turtle

STEP = 30

MOVES = {
    "U":  (0, STEP),   "D":  (0, -STEP),
    "L":  (-STEP, 0),  "R":  (STEP, 0),
    "UL": (-STEP, STEP), "UR": (STEP, STEP),
    "DL": (-STEP, -STEP), "DR": (STEP, -STEP)
}

t = turtle.Turtle()
t.shape("turtle")
t.speed(0)


def load_font(filename):
    font = {}
    with open(filename, encoding="utf-8") as f:
        for line in f:
            if ":" not in line:
                continue
            digit, commands = line.split(":")
            font[digit.strip()] = commands.split()
    return font


DIGITS = load_font("digits.font")


def draw_digit(d):
    for cmd in DIGITS[d]:
        if cmd == "PU":
            t.penup()
        elif cmd == "PD":
            t.pendown()
        else:
            dx, dy = MOVES[cmd]
            t.goto(t.xcor() + dx, t.ycor() + dy)


def draw_number(text):
    for d in text:
        draw_digit(d)
        t.penup()
        t.forward(STEP * 1.5)


t.penup()
t.goto(-250, 0)
draw_number("141700")

turtle.done()
```
[Файл с шрифтом](digits.font)