# GAME
import tkinter as tk
import random

words = ["python", "computer", "keyboard", "variable", "internet", "program", "database"]
current_word = ""
score = 0

def scramble(word):
    word_list = list(word)
    random.shuffle(word_list)
    return "".join(word_list)

def new_word():
    global current_word
    current_word = random.choice(words)
    scrambled_word = scramble(current_word)
    scrambled_label.config(text=scrambled_word)
    hint_label.config(text="")
    entry.delete(0, tk.END)

def check_answer():
    global score
    guess = entry.get().lower()
    if guess == current_word:
        score += 10
        score_label.config(text=f"Score: {score}")
        result_label.config(text="🎉 Correct!", fg="green")
        new_word()
    else:
        result_label.config(text="❌ Try again!", fg="red")

def show_hint():
    hint_label.config(text=f"Hint: starts with '{current_word[0].upper()}'")

# Window UI
window = tk.Tk()
window.title("Word Scramble Game")
window.geometry("400x380")
window.config(bg="#C1EFFF")

# Game Box
frame = tk.Frame(window, bg="white", bd=5, relief="ridge")
frame.place(x=50, y=40, width=300, height=300)

title = tk.Label(frame, text="🌈 Word Scramble", font=("Arial", 18, "bold"), bg="white", fg="#6A0DAD")
title.pack(pady=10)

scrambled_label = tk.Label(frame, text="", font=("Arial", 22, "bold"), bg="#FFED9D", fg="black")
scrambled_label.pack(pady=10)

entry = tk.Entry(frame, font=("Arial", 16), justify="center", bd=3)
entry.pack(pady=10)

submit_btn = tk.Button(frame, text="Submit", font=("Arial", 12), bg="#AECFFF", command=check_answer)
submit_btn.pack(pady=5)

hint_btn = tk.Button(frame, text="Hint", font=("Arial", 12), bg="#D8AAF8", command=show_hint)
hint_btn.pack(pady=5)

skip_btn = tk.Button(frame, text="Skip", font=("Arial", 12), bg="#F7A8A8", command=new_word)
skip_btn.pack(pady=5)

hint_label = tk.Label(frame, text="", font=("Arial", 12), fg="purple", bg="white")
hint_label.pack()

result_label = tk.Label(frame, text="", font=("Arial", 14))
result_label.pack(pady=5)

score_label = tk.Label(window, text="Score: 0", font=("Arial", 14, "bold"), bg="#C1EFFF")
score_label.place(x=160, y=10)

new_word()
window.mainloop()
