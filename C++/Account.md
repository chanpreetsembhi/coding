#### Account Program

```cpp
#include<iostream>  
#include<string>  
using namespace std;  
  
class Account {  
    int accountNo = 0, choose = 0;  
    string name, type;  
    float balanceAmount = 0;  
  
public:  
    void accountDetails() {  
        cout << "Enter your name: ";  
        cin >> name;  
  
        cout << "Enter your account no: ";  
        cin >> accountNo;  
  
        cout << "Enter account type :- 1 for current or 2 for saving: ";  
        cin >> choose;  
  
        if (choose == 1) {  
            type = "Current";  
        } else if (choose == 2) {  
            type = "Saving";  
        } else {  
            type = "Invalid";  
            cout << "Invalid choice: Account type set to 'Unknown'." << endl;  
        }  
    };  
  
    void deposit() {  
        float amount;  
        cout << "Enter deposit amount:" << endl;  
        cin >> amount;  
  
        if (amount > 0) {  
            balanceAmount += amount;  
            cout << "Amount deposited successfully.\n";  
        } else {  
            cout << "Deposit failed.\n";  
        }  
    }  
  
    void withdraw() {  
        float amount;  
        cout << "Enter withdraw amount:" << endl;  
        cin >> amount;  
  
        if (amount <= 0) {  
            cout << "Invalid withdraw amount.\n";  
        } else if (amount > balanceAmount) {  
            cout << "Insufficient balance.\n";  
        } else {  
            balanceAmount -= amount;  
            cout << "Withdrawal successful.\n";  
        }  
    }  
  
    void displayData() const {  
        cout << "\n--- Account Summary ---\n";  
        cout << "Name          : " << name << endl;  
        cout << "Account No    : " << accountNo << endl;  
        cout << "Account Type  : " << type << endl;  
        cout << "Balance       : " << balanceAmount << endl;  
    }  
};  
  
int main() {  
    Account myAccount;  
    myAccount.accountDetails();  
  
    char choice;  
    do {  
        cout << "\nChoose an operation:\n";  
        cout << "1. Deposit\n";  
        cout << "2. Withdraw\n";  
        cout << "3. Display Account Info\n";  
        cout << "4. Exit\n";  
        cout << "Enter your choice: ";  
        cin >> choice;  
  
        switch (choice) {  
            case '1':  
                myAccount.deposit();  
                break;  
            case '2':  
                myAccount.withdraw();  
                break;  
            case '3':  
                myAccount.displayData();  
                break;  
            case '4':  
                cout << "Thank you!\n";  
                break;  
            default:  
                cout << "Invalid option. Try again.\n";  
        }  
    } while (choice != '4');  
  
    return 0;  
}
```