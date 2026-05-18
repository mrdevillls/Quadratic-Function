# Quadratic Function
I made a code which take the value of "a", "b" and "c" after that it will calculate the roots of function with mathematical shape of the equation at the end it will sketch the result on graph



import math
from sympy import symbols, Eq, solve
import matplotlib.pyplot as plt
import numpy as np

print("\n Quadratic Functions ")
print("\n *********************************")



try:
    a = int(input("enter your 'a' number for function: "))
    b = int(input("enter your 'b' number for function: "))
    c = int(input("enter your 'c' number for function: "))

    equation_str = f"{a}x² + {b}x + {c}".replace("+ -", "- ")
    print(f"your function is: {equation_str}")

    if a == 0:
        x_vals = np.linspace(-10, 10, 400)
        y_vals = b * x_vals + c 
        plt.plot(x_vals, y_vals, label=f"{b}x + {c}", color='purple')
        plt.title("Linear Function Plot (a = 0)")
        plt.xlabel("X-axis")
        plt.ylabel("Y-axis")
        plt.axhline(0, color='black', linewidth=0.5)
        plt.axvline(0, color='black', linewidth=0.5)
        plt.legend()
        plt.grid(True)
        plt.savefig("output_plot.jpg")
        plt.show()
        x = symbols("x")
        equation = Eq(b*x, -c)
        solution = solve(equation, x)
        print("x =", solution) 


    else:
        delta = b**2 - 4 * (a * c)
        print("your delta is:", delta, "\n")
        
        roots = []

        if delta > 0:
            route1 = (-b + math.sqrt(delta)) / (2 * a)
            route2 = (-b - math.sqrt(delta)) / (2 * a)
            round_route1 = round(route1, 2)
            round_route2 = round(route2, 2)
            roots = [round_route1, round_route2]
            
            print("your first root (x1) is:", round_route1)
            print("your second root (x2) is:", round_route2)
            
        elif delta == 0:
            repeated_root = round(-b / (2 * a), 2)
            roots = [repeated_root] # Only one root
            print("your repeated root is:", repeated_root)
            
        else:
            print("\a your function doesn't have any real 'x' roots!")

        min_and_max = (-b / (2 * a), -delta / (4 * a))
        if a < 0:
            print(f"your maximum point is: {min_and_max}")
        elif a > 0:
            print(f"your minimum point is: {min_and_max}")
        x_vals = np.linspace(-10, 10, 400)
        y_vals = a * x_vals**2 + b * x_vals + c
        
        plt.plot(x_vals, y_vals, label=equation_str)
        plt.scatter(min_and_max[0], min_and_max[1], color='red', label="Min/Max Point", zorder=5)
        
        if len(roots) > 0:
            plt.scatter(roots, [0]*len(roots), color='green', label="Roots", zorder=5)
        plt.title("Quadratic Function Plot")
        plt.xlabel("X-axis")
        plt.ylabel("Y-axis")
        plt.axhline(0, color='black', linewidth=0.5)
        plt.axvline(0, color='black', linewidth=0.5)
        plt.legend()
        plt.grid(True)
        plt.savefig("output_plot.jpg")
        plt.show()#Same as the plotting logic for the one above


except Exception as error:
    print(f"Something went wrong! {error}")
print("\n********************************************************************************** \t")
print("created by mrdevilll_s (shayan)")