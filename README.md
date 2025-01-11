# HEXSoftware_C-_Programming
#include <iostream>
#include <vector>
#include <string>
#include <limits> // Required for numeric_limits

using namespace std;

struct Task {
    string description;
    bool completed;
};

void addTask(vector<Task>& tasks) {
    cout << "Enter task description: ";
    cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Clear input buffer
    string description;
    getline(cin, description);
    tasks.push_back({description, false});
    cout << "Task added.\n";
}

void viewTasks(const vector<Task>& tasks) {
    if (tasks.empty()) {
        cout << "No tasks in the list.\n";
        return;
    }

    cout << "\n--- To-Do List ---\n";
    for (size_t i = 0; i < tasks.size(); ++i) {
        cout << i + 1 << ". ";
        if (tasks[i].completed) {
            cout << "[X] ";
        } else {
            cout << "[ ] ";
        }
        cout << tasks[i].description << "\n";
    }
    cout << "------------------\n\n";
}

void markComplete(vector<Task>& tasks) {
    viewTasks(tasks); // Show tasks so the user can choose
    if (tasks.empty()) return;

    int taskNumber;
    cout << "Enter the number of the task to mark as complete: ";
    cin >> taskNumber;

    if (cin.fail() || taskNumber < 1 || taskNumber > tasks.size()) {
        cout << "Invalid task number.\n";
        cin.clear(); // Clear error flags
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Discard bad input
        return;
    }

    tasks[taskNumber - 1].completed = true;
    cout << "Task marked as complete.\n";
}

void removeTask(vector<Task>& tasks) {
    viewTasks(tasks);
    if (tasks.empty()) return;

    int taskNumber;
    cout << "Enter the number of the task to remove: ";
    cin >> taskNumber;

    if (cin.fail() || taskNumber < 1 || taskNumber > tasks.size()) {
        cout << "Invalid task number.\n";
        cin.clear();
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        return;
    }

    tasks.erase(tasks.begin() + taskNumber - 1);
    cout << "Task removed.\n";
}

int main() {
    vector<Task> tasks;
    int choice;

    do {
        cout << "\nTo-Do List Menu:\n";
        cout << "1. Add Task\n";
        cout << "2. View Tasks\n";
        cout << "3. Mark Task as Complete\n";
        cout << "4. Remove Task\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                addTask(tasks);
                break;
            case 2:
                viewTasks(tasks);
                break;
            case 3:
                markComplete(tasks);
                break;
            case 4:
                removeTask(tasks);
                break;
            case 5:
                cout << "Exiting program.\n";
                break;
            default:
                cout << "Invalid choice. Please try again.\n";
                 cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    } while (choice != 5);

    return 0;
}
