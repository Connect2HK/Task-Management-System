# Task-Management-System
A task management system comes with functionality of user management , task management, user interface and with search and filtering options.
import tkinter as tk
from tkinter import ttk, messagebox


class Task:
    def _init_(self, title, description, due_date, assigned_to, status):
        self.title = title
        self.description = description
        self.due_date = due_date
        self.assigned_to = assigned_to
        self.status = status

    def _str_(self):
        return f"Title: {self.title}\nDescription: {self.description}\nDue Date: {self.due_date}\nAssigned To: {self.assigned_to}\nStatus: {self.status}"


def main():
    tasks = []

    # Create the GUI
    root = tk.Tk()
    root.title("Task Management System")
    root.geometry("600x500")  # Set the width and height of the window

    # Create the task treeview
    task_tree = ttk.Treeview(root, columns=(
        "title", "description", "due_date", "assigned_to", "status"))
    task_tree.heading("title", text="Title")
    task_tree.heading("description", text="Description")
    task_tree.heading("due_date", text="Due Date")
    task_tree.heading("assigned_to", text="Assigned To")
    task_tree.heading("status", text="Status")
    task_tree.pack(fill=tk.BOTH, expand=True)

    # Create the buttons frame
    button_frame = tk.Frame(root)
    button_frame.pack()

    # Create the buttons
    add_button = tk.Button(button_frame, text="Add Task",
                           command=lambda: add_task(root, task_tree, tasks))
    view_button = tk.Button(button_frame, text="View Task",
                            command=lambda: view_task(root, task_tree, tasks))
    edit_button = tk.Button(button_frame, text="Edit Task",
                            command=lambda: edit_task(root, task_tree, tasks))
    delete_button = tk.Button(button_frame, text="Delete Task",
                              command=lambda: delete_task(root, task_tree, tasks))

    # Pack the buttons
    add_button.pack(side=tk.LEFT, padx=5, pady=5)
    view_button.pack(side=tk.LEFT, padx=5, pady=5)
    edit_button.pack(side=tk.LEFT, padx=5, pady=5)
    delete_button.pack(side=tk.LEFT, padx=5, pady=5)

    root.mainloop()

class Task:
    def __init__(self, title, description, due_date, assigned_to, status):
        self.title = title
        self.description = description
        self.due_date = due_date
        self.assigned_to = assigned_to
        self.status = status

    def __str__(self):
        return f"Title: {self.title}\nDescription: {self.description}\nDue Date: {self.due_date}\nAssigned To: {self.assigned_to}\nStatus: {self.status}"
def add_task(root, task_tree, tasks):
    # Create a new window for adding a task
    add_window = tk.Toplevel(root)

    # Create label widgets for each task attribute
    title_label = tk.Label(add_window, text="Title:")
    description_label = tk.Label(add_window, text="Description:")
    due_date_label = tk.Label(add_window, text="Due Date:")
    assigned_to_label = tk.Label(add_window, text="Assigned To:")
    status_label = tk.Label(add_window, text="Status:")

    # Create entry widgets for each task attribute
    title_entry = tk.Entry(add_window)
    description_entry = tk.Entry(add_window)
    due_date_entry = tk.Entry(add_window)
    assigned_to_entry = tk.Entry(add_window)
    status_entry = tk.Entry(add_window)

    # Pack the labels and entry fields
    title_label.pack()
    title_entry.pack()
    description_label.pack()
    description_entry.pack()
    due_date_label.pack()
    due_date_entry.pack()
    assigned_to_label.pack()
    assigned_to_entry.pack()
    status_label.pack()
    status_entry.pack()

    # Create a frame for the button
    button_frame = tk.Frame(add_window)
    button_frame.pack()

    # Function to handle the "Add" button click event
    def add_button_click():
        title = title_entry.get()
        description = description_entry.get()
        due_date = due_date_entry.get()
        assigned_to = assigned_to_entry.get()
        status = status_entry.get()

        task = Task(title, description, due_date, assigned_to, status)
        tasks.append(task)

        task_tree.insert("", tk.END, values=(
            task.title, task.description, task.due_date, task.assigned_to, task.status))
        add_window.destroy()  # Close the add window

    # Create the "Add" button inside the frame
    add_button = tk.Button(button_frame, text="Add", command=add_button_click)
    add_button.pack()


def view_task(root, task_tree, tasks):
    selected_item = task_tree.selection()
    if selected_item:
        item = task_tree.item(selected_item)
        # Retrieve the task object from the tasks list
        task = tasks[selected_item[0]]

        messagebox.showinfo("Task Details", str(task))
    else:
        messagebox.showinfo("No Task Selected",
                            "Please select a task from the list.")


def edit_task(root, task_tree, tasks):
    selected_item = task_tree.selection()
    if selected_item:
        item = task_tree.item(selected_item)
        # Retrieve the task object from the tasks list
        task = tasks[selected_item[0]]

        edit_window = tk.Toplevel(root)

        # Create label widgets for each task attribute
        title_label = tk.Label(edit_window, text="Title:")
        description_label = tk.Label(edit_window, text="Description:")
        due_date_label = tk.Label(edit_window, text="Due Date:")
        assigned_to_label = tk.Label(edit_window, text="Assigned To:")
        status_label = tk.Label(edit_window, text="Status:")

        # Create entry widgets for each task attribute and set their initial values
        title_entry = tk.Entry(edit_window)
        title_entry.insert(tk.END, task.title)
        description_entry = tk.Entry(edit_window)
        description_entry.insert(tk.END, task.description)
        due_date_entry = tk.Entry(edit_window)
        due_date_entry.insert(tk.END, task.due_date)
        assigned_to_entry = tk.Entry(edit_window)
        assigned_to_entry.insert(tk.END, task.assigned_to)
        status_entry = tk.Entry(edit_window)
        status_entry.insert(tk.END, task.status)
        # Pack the labels and entry fields
        title_label.pack()
        title_entry.pack()
        description_label.pack()
        description_entry.pack()
        due_date_label.pack()
        due_date_entry.pack()
        assigned_to_label.pack()
        assigned_to_entry.pack()
        status_label.pack()
        status_entry.pack()
        # Create a frame for the button
        button_frame = tk.Frame(edit_window)
        button_frame.pack()
        # Function to handle the "Save" button click event
        def save_button_click():
            task.title = title_entry.get()
            task.description = description_entry.get()
            task.due_date = due_date_entry.get()
            task.assigned_to = assigned_to_entry.get()
            task.status = status_entry.get()
            task_tree.item(selected_item, values=(
                task.title, task.description, task.due_date, task.assigned_to, task.status))
            edit_window.destroy()  # Close the edit window

        # Create the "Save" button inside the frame
        save_button = tk.Button(button_frame, text="Save",
                                command=save_button_click)
        save_button.pack()
    else:
        messagebox.showinfo("No Task Selected",
                            "Please select a task from the list.")
def delete_task(root, task_tree, tasks):
    selected_item = task_tree.selection()
    if selected_item:
        confirmation = messagebox.askyesno(
            "Confirmation", "Are you sure you want to delete this task?")
        if confirmation:
            task_tree.delete(selected_item)
            # Remove the task object from the tasks list
            del tasks[selected_item[0]]
    else:
        messagebox.showinfo("No Task Selected",
                            "Please select a task from the list.")
class User:
    def __init__(self, username, password):
        self.username = username
        self.password = password
def add_user(root, user_tree, users):
    # Create a new window for adding a user
    add_window = tk.Toplevel(root)
    # Create label widgets for each user attribute
    username_label = tk.Label(add_window, text="Username:")
    password_label = tk.Label(add_window, text="Password:")
    # Create entry widgets for each user attribute
    username_entry = tk.Entry(add_window)
    password_entry = tk.Entry(add_window, show="*")
    # Pack the labels and entry fields
    username_label.pack()
    username_entry.pack()
    password_label.pack()
    password_entry.pack()
    # Create a frame for the button
    button_frame = tk.Frame(add_window)
    button_frame.pack()
    # Function to handle the "Add" button click event
    def add_button_click():
        username = username_entry.get()
        password = password_entry.get()
        user = User(username, password)
        users.append(user)
        user_tree.insert("", tk.END, values=(user.username, user.password))
        add_window.destroy()  # Close the add window

    # Create the "Add" button inside the frame
    add_button = tk.Button(button_frame, text="Add", command=add_button_click)
    add_button.pack()
def view_user(root, user_tree, users):
    selected_item = user_tree.selection()
    if selected_item:
        item = user_tree.item(selected_item)
        # Retrieve the user object from the users list
        user = users[selected_item[0]]
        messagebox.showinfo("User Details", str(user))
    else:
        messagebox.showinfo("No User Selected", "Please select a user from the list.")
def edit_user(root, user_tree, users):
    selected_item = user_tree.selection()
    if selected_item:
        item = user_tree.item(selected_item)
        # Retrieve the user object from the users list
        user = users[selected_item[0]]
        edit_window = tk.Toplevel(root)
        # Create label widgets for each user attribute
        username_label = tk.Label(edit_window, text="Username:")
        password_label = tk.Label(edit_window, text="Password:")
        # Create entry widgets for each user attribute and set their initial values
        username_entry = tk.Entry(edit_window)
        username_entry.insert(tk.END, user.username)
        password_entry = tk.Entry(edit_window, show="*")
        password_entry.insert(tk.END, user.password)
        # Pack the labels and entry fields
        username_label.pack()
        username_entry.pack()
        password_label.pack()
        password_entry.pack()
        # Create a frame for the button
        button_frame = tk.Frame(edit_window)
        button_frame.pack()
        # Function to handle the "Save" button click event
        def save_button_click():
            username = username_entry.get()
            password = password_entry.get()
            user.username = username
            user.password = password
            user_tree.item(selected_item, values=(user.username, user.password))
            edit_window.destroy()  # Close the edit window
        # Create the "Save" button inside the frame
        save_button = tk.Button(button_frame, text="Save", command=save_button_click)
def search_users(user_tree, search_entry):
    search_keyword = search_entry.get().lower()
    # Clear the user tree
    user_tree.delete(*user_tree.get_children())
    # Filter users based on the search keyword
    for user in users:
        if search_keyword in user.username.lower():
            user_tree.insert("", tk.END, values=(user.username, user.password))
def filter_users(user_tree, filter_var):
    selected_filter = filter_var.get()
    # Clear the user tree
    user_tree.delete(*user_tree.get_children())
    # Filter users based on the selected filter
    for user in users:
        if selected_filter == "All" or selected_filter == user.password:
            user_tree.insert("", tk.END, values=(user.username, user.password))
root = tk.Tk()
# Create a treeview to display users
user_tree = ttk.Treeview(root, columns=("Username", "Password"))
user_tree.heading("#0", text="ID")
user_tree.heading("Username", text="Username")
user_tree.heading("Password", text="Password")
user_tree.pack()

# Create a frame for search and filter components
search_filter_frame = tk.Frame(root)
search_filter_frame.pack()

# Create a search entry
search_entry = tk.Entry(search_filter_frame)
search_entry.pack(side=tk.LEFT)
search_button = tk.Button(search_filter_frame, text="Search", command=lambda: search_users(user_tree, search_entry))
search_button.pack(side=tk.LEFT)

# Create a filter dropdown
filter_var = tk.StringVar()
filter_var.set("All")
filter_dropdown = tk.OptionMenu(search_filter_frame, filter_var, "All", "Password1", "Password2", "Password3", command=lambda _: filter_users(user_tree, filter_var))
filter_dropdown.pack(side=tk.LEFT)

# Create a list of users
users = [
    User("User1", "Password1"),
    User("User2", "Password2"),
    User("User3", "Password3"),
]

# Insert users into the treeview
for i, user in enumerate(users, start=1):
    user_tree.insert("", tk.END, text=str(i), values=(user.username, user.password))

root.mainloop()

if __name__ == "__main__":
    main()
