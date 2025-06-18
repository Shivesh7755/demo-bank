#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

// Structure to represent a customer
struct Customer {
    string name;
    string accountNumber;
    double balance;
};

// Function to create a new customer account
void createAccount(vector<Customer>& customers) {
    Customer newCustomer;
    cout << "Enter customer name: ";
    cin >> newCustomer.name;
    cout << "Enter account number: ";
    cin >> newCustomer.accountNumber;
    newCustomer.balance = 0.0;
    customers.push_back(newCustomer);
    cout << "Account created successfully!" << endl;
}

// Function to deposit money into an account
void depositMoney(vector<Customer>& customers) {
    string accountNumber;
    double amount;
    cout << "Enter account number: ";
    cin >> accountNumber;
    cout << "Enter amount to deposit: ";
    cin >> amount;

    for (auto& customer : customers) {
        if (customer.accountNumber == accountNumber) {
            customer.balance += amount;
            cout << "Deposit successful! New balance: " << customer.balance << endl;
            return;
        }
    }
    cout << "Account not found!" << endl;
}

// Function to withdraw money from an account
void withdrawMoney(vector<Customer>& customers) {
    string accountNumber;
    double amount;
    cout << "Enter account number: ";
    cin >> accountNumber;
    cout << "Enter amount to withdraw: ";
    cin >> amount;

    for (auto& customer : customers) {
        if (customer.accountNumber == accountNumber) {
            if (customer.balance >= amount) {
                customer.balance -= amount;
                cout << "Withdrawal successful! New balance: " << customer.balance << endl;
            } else {
                cout << "Insufficient balance!" << endl;
            }
            return;
        }
    }
    cout << "Account not found!" << endl;
}

// Function to display customer details
void displayDetails(const vector<Customer>& customers) {
    string accountNumber;
    cout << "Enter account number: ";
    cin >> accountNumber;

    for (const auto& customer : customers) {
        if (customer.accountNumber == accountNumber) {
            cout << "Customer Name: " << customer.name << endl;
            cout << "Account Number: " << customer.accountNumber << endl;
            cout << "Balance: " << customer.balance << endl;
            return;
        }
    }
    cout << "Account not found!" << endl;
}

int main() {
    vector<Customer> customers;
    int choice;

    while (true) {
        cout << "Bank Management System" << endl;
        cout << "1. Create Account" << endl;
        cout << "2. Deposit Money" << endl;
        cout << "3. Withdraw Money" << endl;
        cout << "4. Display Details" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                createAccount(customers);
                break;
            case 2:
                depositMoney(customers);
                break;
            case 3:
                withdrawMoney(customers);
                break;
            case 4:
                displayDetails(customers);
                break;
            case 5:
                return 0;
            default:
                cout << "Invalid choice!" << endl;
        }
    }

    return 0;
}
