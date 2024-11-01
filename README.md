#include <iostream>
#include <string>

class BankAccount {
protected:
    std::string accountHolder;
    float balance;

public:
    void setAccountHolder(std::string name) {
        accountHolder = name;
    }

    std::string getAccountHolder() {
        return accountHolder;
    }

    float getBalance() {
        return balance;
    }

    BankAccount(std::string name, float initialBalance) {
        accountHolder = name;
        balance = initialBalance;
    }
};

class SavingAccount : public BankAccount {
private:
    float interestRate;

public:
    SavingAccount(std::string name, float initialBalance, float rate) 
        : BankAccount(name, initialBalance), interestRate(rate) {}

    float calculateInterest() {
        return balance * interestRate;
    }
};

class CheckingAccount : public BankAccount {
private:
    float transactionFee;

public:
    CheckingAccount(std::string name, float initialBalance, float fee) 
        : BankAccount(name, initialBalance), transactionFee(fee) {}

    void deductFee() {
        balance -= transactionFee;
    }
};

int main() {
    SavingAccount savings("Alice", 1000, 0.03);
    CheckingAccount checking("Bob", 500, 2.5);

    std::cout << "Savings Account Holder: " << savings.getAccountHolder() << std::endl;
    std::cout << "Balance: " << savings.getBalance() << std::endl;
    std::cout << "Calculated Interest: " << savings.calculateInterest() << std::endl;

    std::cout << "Checking Account Holder: " << checking.getAccountHolder() << std::endl;
    std::cout << "Balance: " << checking.getBalance() << std::endl;
    checking.deductFee();
    std::cout << "Updated Balance after deducting fee: " << checking.getBalance() << std::endl;

    return 0;
}
