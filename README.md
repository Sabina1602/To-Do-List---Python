# Our to-do list is saved here
tasks = []


def show_tasks():
    #Display all tasks currently in the to-do list.
    print("\n--- Your Tasks ---")
    if not tasks:
        print("  No tasks yet!")
    else:
        for i, task in enumerate(tasks, 1):
            print(f"  {i}. {task}")
    print("------------------")


def add_task():
    #Ask the user for a new task and add it to the list.
    task = input("Enter task: ").strip()
    if task:
        tasks.append(task)
        print(f"  ✅ Added: '{task}'")
    else:
        print("  ⚠️  Task can't be empty.")


def remove_task():
    #Show tasks and let the user remove one by its number.
    show_tasks()
    try:
        num = int(input("Enter task number to remove: "))
        if 1 <= num <= len(tasks):
            removed = tasks.pop(num - 1)
            print(f"  🗑️  Removed: '{removed}'")
        else:
            print("  ❌ Invalid number.")
    except ValueError:
        print("  ❌ Please enter a valid number.")


def save_tasks():
    #Save the current tasks to a text file.
    with open("my_tasks.txt", "w") as f:
        for task in tasks:
            f.write(task + "\n")
    print("  💾 Tasks saved to my_tasks.txt")


def load_tasks():
    #Load tasks from the file when the program starts, if it exists.
    try:
        with open("my_tasks.txt", "r") as f:
            for line in f:
                tasks.append(line.strip())
        print(f"  📂 Loaded {len(tasks)} task(s) from file.")
    except FileNotFoundError:
        pass  # No file yet, that's fine


# ── Main Program ──

load_tasks()  # Load any saved tasks on startup

while True:
    print("\n=== To-Do List ===")
    print("1. View tasks")
    print("2. Add task")
    print("3. Remove task")
    print("4. Save & Quit")

    choice = input("Choose (1-4): ").strip()

    if choice == "1":
        show_tasks()
    elif choice == "2":
        add_task()
    elif choice == "3":
        remove_task()
    elif choice == "4":
        save_tasks()
        print("\n👋 Bye!\n")
        break
    else:
        print("  ❌ Pick 1, 2, 3, or 4.")
