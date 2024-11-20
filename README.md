# nomer
import tkinter as tk
from tkinter import messagebox
import mysql.connector

def db_connector():
    return mysql.connector.connect(
    host = "localhost",
    user = "user",
    password = "password",
    database = "database"
    )

class libraryApp:
    def __init__(self, master):
        self.master = master
        master.title("Учет книг")
        master.geometry("400x300")

        self.entries = {}
        for label in ("название", "Автор", "год", "жанр"):
            tk.Label(master, text= label).pack()
            self.entries[label]=tk.Entry(master)
            self.entries[label].pack()

        tk.Button(master, text="Добавить Книгу",command=self.add_book).pack()
        tk.Button(master, text="Показать книги", command=self.view_books).pack()

    def add_book(self):
        title, author, year, genre = (self.entries[label].get()for lable in self.entries)
        if all([title,author,year.isdigit(), genre]):
            messagebox.showinfo("успешно")
        else:
            messagebox.showerror("Ошибка")

    def view_books(self):
        pass

if __name__ == "__main__":
    root= tk.Tk()
    app=libraryApp(root)
    root.mainloop()

