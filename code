import tkinter as tk
from datetime import datetime
import os


def load_tasks(filename):
    tasks = []
    if not os.path.exists(filename):
        return [("Файл не найден", "2000-01-01")]

    with open(filename, 'r', encoding='utf-8') as f:
        for line in f:
            if '|' in line:
                date_part, title_part = line.strip().split('|')
                tasks.append((title_part, date_part))
    return tasks


def create_app():
    root = tk.Tk()
    root.title("Что мне делать, как мне жить?")
    root.configure(bg='black')
    root.geometry("850x650")

    tk.Label(
        root,
        text="Мои текущие задачи",
        font=("Times New Roman", 40, "bold", "underline"),
        fg="yellow",
        bg="black",
        pady=20
    ).pack()

    content_frame = tk.Frame(root, bg="black")
    content_frame.pack(expand=True, fill="both", padx=50)

    events = load_tasks("tasks.txt")
    today = datetime.now().date()

    for text, date_str in events:
        try:
            event_date = datetime.strptime(date_str, "%Y-%m-%d").date()
            delta = (today - event_date).days

            if delta == 0:
                label_text = f"Прямо щаз происходит {text}"
                color = "#D4AF37"
            elif delta > 0:
                label_text = f"Прошло {delta} дней от {text}"
                color = "red"
            else:
                label_text = f"Осталось {abs(delta)} дней до {text}"
                color = "lightblue"
        except ValueError:
            label_text = f"Ошибка формата: {text}"
            color = "white"

        tk.Label(
            content_frame,
            text=label_text,
            font=("Arial", 16),
            fg=color,
            bg="black",
            pady=3
        ).pack(anchor="w")

    root.mainloop()


if __name__ == "__main__":
    create_app()
