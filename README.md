# turtle_tree.py
import turtle
import random

screen = turtle.Screen()
screen.title("Cây thông nhỏ xinh")
screen.bgcolor("skyblue")

t = turtle.Turtle()
t.hideturtle()
t.speed(0)

def draw_triangle(x, y, width, height, color):
    t.up()
    t.goto(x, y)
    t.color(color)
    t.begin_fill()
    t.down()
    t.setheading(0)
    t.forward(width / 2)
    t.left(120)
    t.forward(width)
    t.left(120)
    t.forward(width)
    t.left(120)
    t.forward(width / 2)
    t.end_fill()
    t.up()

def draw_tree(x=0, y=-150, levels=4, width=200):
    # mỗi tầng nhỏ hơn tầng trên
    for i in range(levels):
        w = width - i * (width // (levels + 1))
        h = w // 2
        draw_triangle(x - w / 2, y + i * (h*0.6), w, h, "forest green")
    # thân
    t.goto(x - width*0.07, y - 20)
    t.color("sienna")
    t.begin_fill()
    for _ in range(2):
        t.down()
        t.forward(width*0.14)
        t.left(90)
        t.forward(width*0.2)
        t.left(90)
    t.end_fill()
    t.up()

def decorate(x=0, y=-150, levels=4, width=200, ornaments=20):
    # randomly place ornaments on the green area
    for _ in range(ornaments):
        # pick a level and random position within that triangle width
        lvl = random.randint(0, levels - 1)
        w = width - lvl * (width // (levels + 1))
        h = w // 2
        # horizontal range inside triangle: center +/- w/2 scaled by level height fraction
        rx = x + random.uniform(-w/2 + 10, w/2 - 10)
        ry = y + lvl * (h*0.6) + random.uniform(0, h*0.9)
        t.goto(rx, ry)
        t.dot(random.randint(6, 12), random.choice(["red", "gold", "yellow", "cyan", "magenta"]))

def draw_star(x, y, size=30, color="gold"):
    t.up()
    t.goto(x, y)
    t.setheading(0)
    t.down()
    t.color(color)
    t.begin_fill()
    for _ in range(5):
        t.forward(size)
        t.right(144)
    t.end_fill()
    t.up()

if __name__ == "__main__":
    draw_tree(x=0, y=-150, levels=5, width=260)
    decorate(x=0, y=-150, levels=5, width=260, ornaments=30)
    draw_star(0, 40, size=40)
    t.goto(-250, -200)
    t.color("black")
    t.write("Chúc bạn code vui vẻ! 🎄", font=("Arial", 14, "bold"))
    screen.mainloop()
