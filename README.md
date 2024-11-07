import random
import tkinter as tk
from tkinter import simpledialog, messagebox, Toplevel, Label

def get_user_choice():
    user_input = simpledialog.askstring("Input", "Enter rock, paper, or scissors:").lower()
    while user_input not in ["rock", "paper", "scissors"]:
        user_input = simpledialog.askstring("Input", "Invalid choice. Please enter rock, paper, or scissors:").lower()
    return user_input

def get_computer_choice():
    return random.choice(["rock", "paper", "scissors"])

def determine_winner(user_choice, computer_choice):
    if user_choice == computer_choice:
        return "It's a tie!"
    elif (user_choice == "rock" and computer_choice == "scissors") or \
         (user_choice == "paper" and computer_choice == "rock") or \
         (user_choice == "scissors" and computer_choice == "paper"):
        return "You win!"
    else:
        return "You lose!"

def show_result(user_choice, computer_choice, result):
    result_window = Toplevel()
    result_window.title("Game Result")
    result_window.geometry("300x200")
    Label(result_window, text=f"You chose: {user_choice}", font=("Helvetica", 14)).pack(pady=10)
    Label(result_window, text=f"Computer chose: {computer_choice}", font=("Helvetica", 14)).pack(pady=10)
    Label(result_window, text=result, font=("Helvetica", 16, "bold")).pack(pady=20)
    if messagebox.askyesno("Play Again?", "Do you want to play again?"):
        result_window.destroy()
        play_game()
    else:
        result_window.destroy()

def play_game():
    while True:
        user_choice = get_user_choice()
        computer_choice = get_computer_choice()
        result = determine_winner(user_choice, computer_choice)
        show_result(user_choice, computer_choice, result)
        break

if __name__ == "__main__":
    root = tk.Tk()
    root.withdraw()  # Hide the main window
    play_game()
