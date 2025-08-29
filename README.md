import tkinter as tk
from tkinter import messagebox
import re

# Function to solve math or logic questions
def solve_question(question):
    question = question.lower().strip()

    try:
        # Square related question
        if "square of" in question:
            num = int(re.findall(r'\d+', question)[0])
            return f"The square of {num} is {num * num}"

        # Car distance problem
        elif "car" in question and "hour" in question:
            numbers = list(map(int, re.findall(r'\d+', question)))
            if len(numbers) >= 2:
                speed, time = numbers[0], numbers[-1]
                distance = speed * time
                return f"The car will travel {distance} km in {time} hours"

        # Rupees problem
        elif "rupees" in question and "bill" in question:
            numbers = list(map(int, re.findall(r'\d+', question)))
            if len(numbers) >= 3:
                ali, adnan, bill = numbers[0], numbers[1], numbers[2]
                total = ali + adnan
                if total >= bill:
                    share = bill // 2
                    ali_rem = ali - share
                    adnan_rem = adnan - share
                    return f"Ali will have {ali_rem} rupees, Adnan will have {adnan_rem} rupees left."
                else:
                    return "Not enough money to pay the bill."

        # Simple math equations
        else:
            try:
                result = eval(question)
                return f"The answer is {result}"
            except:
                return "Sorry, I didn't understand. Please enter a valid question."

    except Exception as e:
        return "Invalid input! That is incorrect please change syntax."


# Function to get answer and show in result label
def get_answer():
    q = entry.get()
    ans = solve_question(q)
    result_label.config(text=ans)


# GUI setup
root = tk.Tk()
root.title("Math Problem Solver")
root.geometry("500x400")
root.configure(bg="#2C3E50")  # Set background color

# Heading
title = tk.Label(root, text="🤖 Math Problem Solver", font=("Arial", 18, "bold"), bg="#2C3E50", fg="white")
title.pack(pady=15)

# Entry box
entry = tk.Entry(root, font=("Arial", 14), width=35, bd=3, relief="solid")
entry.pack(pady=10)

# Answer button
btn = tk.Button(root, text="Get Answer", font=("Arial", 14, "bold"), bg="#27AE60", fg="white", relief="raised", command=get_answer)
btn.pack(pady=10)

# Result Label
result_label = tk.Label(root, text="", font=("Arial", 14), bg="#2C3E50", fg="yellow", wraplength=450, justify="center")
result_label.pack(pady=20)

# Bind Enter key to trigger answer
root.bind("<Return>", lambda event: get_answer())

# Run the app
root.mainloop()

