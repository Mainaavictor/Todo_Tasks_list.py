# Todo_Tasks_list.py
A Python web Task Review to add and remove listings on tasks already done and onto tasks"
import os

TASKS_FILE = "tasks.txt"

def load_tasks():
    if not os.path.exists(TASKS_FILE):
        return []
    with open(TASKS_FILE, "r") as f:
        return [line.strip() for line in f.readlines()]

def save_tasks(tasks):
    with open(TASKS_FILE, "w") as f:
        for task in tasks:
            f.write(task + "\n")

def show_tasks(tasks):
    if not tasks:
        print("No tasks yet!")
    else:
        for i, task in enumerate(tasks, 1):
            print(f"{i}. {task}")

def main():
    tasks = load_tasks()

    while True:
        print("\nMenu:\n1. Show tasks\n2. Add task\n3. Remove task\n4. Exit")
        choice = input("Choose an option: ").strip()

        if choice == "1":
            show_tasks(tasks)

        elif choice == "2":
            task = input("Enter a new task: ").strip()
            if task:
                tasks.append(task)
                save_tasks(tasks)
                print("Task added.")

        elif choice == "3":
            show_tasks(tasks)
            if tasks:
                num = input("Enter task number to remove: ").strip()
                if num.isdigit():
                    num = int(num)
                    if 1 <= num <= len(tasks):
                        removed = tasks.pop(num - 1)
                        save_tasks(tasks)
                        print(f"Removed task: {removed}")
                    else:
                        print("Invalid task number.")
                else:
                    print("Please enter a valid number.")

        elif choice == "4":
            print("Bye!")
            break

        else:
            print("Invalid option. Try again.")

if __name__ == "__main__":
    main()
# Todo.py - A simple command-line todo list application
# This script allows users to manage a todo list by adding, removing, and viewing tasks.

#TODO_Test.py code
import unittest
import os
from Todo import load_tasks, save_tasks
# Todo.py - A simple command-line todo list application
class TestTodo(unittest.TestCase):

    def setUp(self):
        # Setup before each test
        self.test_file = "test_tasks.txt"

    def tearDown(self):
        # Cleanup after each test
        if os.path.exists(self.test_file):
            os.remove(self.test_file)
            

    def test_load_tasks_empty(self):
        if os.path.exists(self.test_file):
            os.remove(self.test_file)
        tasks = load_tasks()
        self.assertEqual(tasks, [])

    def test_save_and_load_tasks(self):
        tasks = ["Task 1", "Task 2"]
        save_tasks(tasks)
        loaded = load_tasks()
        self.assertEqual(tasks, loaded)

if __name__ == "__main__":
    unittest.main()

