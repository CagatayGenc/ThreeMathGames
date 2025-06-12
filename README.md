```python
import matplotlib.pyplot as plt
import numpy as np
import random
from ipywidgets import interact, FloatSlider

#Scatter Plot Game
def scatter_plot_game(num_points=5, x_range=10, y_range=10):
    x_vals = [random.randint(0, x_range) for _ in range(num_points)]
    y_vals = [random.randint(0, y_range) for _ in range(num_points)]

    plt.figure(figsize=(6, 6))
    plt.scatter(x_vals, y_vals, color='blue')

    for i in range(num_points):
        plt.text(x_vals[i] + 0.3, y_vals[i] + 0.3, str(i + 1), fontsize=12, color='green')

    plt.title("Guess the Coordinates")
    plt.grid(True)
    plt.xlim(0, x_range)
    plt.ylim(0, y_range)
    plt.xlabel("X")
    plt.ylabel("Y")
    plt.show()

    score = 0
    for i in range(num_points):
        guess = input(f"Guess the coordinates for point #{i+1} (format: x,y): ")
        try:
            gx, gy = map(int, guess.strip().split(','))
            if gx == x_vals[i] and gy == y_vals[i]:
                print("✅ Correct!")
                score += 1
            else:
                print(f"❌ Incorrect. Correct was ({x_vals[i]}, {y_vals[i]})")
        except:
            print("⚠️ Invalid input.")
    print(f"Your score: {score}/{num_points}")

#Algebra Practice Game
def solve_equation_game(num_questions=5):
    score = 0
    for _ in range(num_questions):
        step_type = random.choice(['one', 'two'])
        a = random.randint(-10, 10)
        while a == 0:
            a = random.randint(-10, 10)
        x = random.randint(-10, 10)

        if step_type == 'one':
            b = a * x
            print(f"Solve: {a}x = {b}")
        else:
            b = random.randint(-10, 10)
            c = a * x + b
            print(f"Solve: {a}x + {b} = {c}")

        try:
            answer = float(input("x = "))
            if abs(answer - x) < 1e-3:
                print("✅ Correct!")
                score += 1
            else:
                print(f"❌ Incorrect. Correct answer: x = {x}")
        except:
            print("⚠️ Invalid input.")
    print(f"Your score: {score}/{num_questions}")

#Projectile Game
def projectile_path_game():
    wall_x = random.randint(5, 15)
    wall_height = random.randint(5, 15)

    def plot_path(a, b, c):
        x_vals = np.linspace(0, 20, 400)
        y_vals = a * x_vals**2 + b * x_vals + c

        plt.figure(figsize=(10, 6))
        plt.plot(x_vals, y_vals, label="Your parabola")
        plt.axvline(x=wall_x, color='red', linestyle='--', label='Wall')
        plt.axhline(y=wall_height, color='black', linestyle=':')
        plt.scatter(wall_x, wall_height, color='red', label='Wall Top')
        plt.ylim(0, max(20, wall_height + 5))
        plt.xlim(0, 20)
        plt.grid(True)
        plt.title("Adjust the parabola to clear the wall!")
        plt.legend()
        plt.show()

    print(f"Wall position: x = {wall_x}, height = {wall_height}")
    interact(plot_path,
             a=FloatSlider(min=-2, max=0, step=0.1, value=-0.5),
             b=FloatSlider(min=0, max=10, step=0.5, value=5),
             c=FloatSlider(min=0, max=10, step=0.5, value=1))

#Main Menu
def main_menu():
    while True:
        print("\n🎮 MATH GAMES MENU 🎮")
        print("1. Scatter Plot Game")
        print("2. Algebra Practice Game")
        print("3. Projectile Game")
        print("4. Exit")
        choice = input("Choose a game (1-4): ")

        if choice == '1':
            scatter_plot_game()
        elif choice == '2':
            solve_equation_game()
        elif choice == '3':
            projectile_path_game()
        elif choice == '4':
            print("Thanks for playing! 👋")
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 4.")

main_menu()
```
