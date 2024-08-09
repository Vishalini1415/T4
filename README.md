#include <iostream>
#include <vector>
#include <string>

class TodoListManager {
public:
    void addTask(const std::string& task) {
        tasks.push_back({task, false});
        std::cout << "Task '" << task << "' added.\n";
    }

    void viewTasks() const {
        if (tasks.empty()) {
            std::cout << "No tasks in the list.\n";
            return;
        }
        for (size_t i = 0; i < tasks.size(); ++i) {
            std::cout << i + 1 << ". " << tasks[i].task 
                      << " - " << (tasks[i].completed ? "Completed" : "Pending") << "\n";
        }
    }

    void markTaskCompleted(size_t taskNumber) {
        if (taskNumber > 0 && taskNumber <= tasks.size()) {
            tasks[taskNumber - 1].completed = true;
            std::cout << "Task " << taskNumber << " marked as completed.\n";
        } else {
            std::cout << "Invalid task number.\n";
        }
    }

    void removeTask(size_t taskNumber) {
        if (taskNumber > 0 && taskNumber <= tasks.size()) {
            std::cout << "Task '" << tasks[taskNumber - 1].task << "' removed.\n";
            tasks.erase(tasks.begin() + taskNumber - 1);
        } else {
            std::cout << "Invalid task number.\n";
        }
    }

    void run() {
        while (true) {
            std::cout << "\nTo-Do List Manager\n";
            std::cout << "1. Add Task\n";
            std::cout << "2. View Tasks\n";
            std::cout << "3. Mark Task as Completed\n";
            std::cout << "4. Remove Task\n";
            std::cout << "5. Exit\n";
            std::cout << "Enter your choice: ";

            int choice;
            std::cin >> choice;

            std::cin.ignore();  // To ignore the newline character after the integer input

            if (choice == 1) {
                std::cout << "Enter task: ";
                std::string task;
                std::getline(std::cin, task);
                addTask(task);
            } else if (choice == 2) {
                viewTasks();
            } else if (choice == 3) {
                std::cout << "Enter task number to mark as completed: ";
                size_t taskNumber;
                std::cin >> taskNumber;
                markTaskCompleted(taskNumber);
            } else if (choice == 4) {
                std::cout << "Enter task number to remove: ";
                size_t taskNumber;
                std::cin >> taskNumber;
                removeTask(taskNumber);
            } else if (choice == 5) {
                std::cout << "Exiting To-Do List Manager. Goodbye!\n";
                break;
            } else {
                std::cout << "Invalid choice. Please try again.\n";
            }
        }
    }

private:
    struct Task {
        std::string task;
        bool completed;
    };

    std::vector<Task> tasks;
};

int main() {
    TodoListManager manager;
    manager.run();
    return 0;
}
