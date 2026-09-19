import java.util.Scanner;

// Abstraction
abstract class Bank {

    public String name;
    public int accountNumber;
    private int pin;
    protected double balance;

    // Constructor
    Bank(String name, int accountNumber, int pin, double balance) {
        this.name = name;
        this.accountNumber = accountNumber;
        this.pin = pin;
        this.balance = balance;
    }

    // Encapsulation: private PIN accessed through method
    public boolean checkPin(int enteredPin) {
        return pin == enteredPin;
    }

    // Abstract method
    abstract void bankType();

    // Method Overloading
    void credit(double amount) {
        if (amount > 0) {
            balance = balance + amount;
            System.out.println("Amount credited: " + amount);
        } else {
            System.out.println("Invalid amount.");
        }
    }

    void credit(double amount, String mode) {
        if (amount > 0) {
            balance = balance + amount;
            System.out.println("Amount credited: " + amount);
            System.out.println("Mode: " + mode);
        } else {
            System.out.println("Invalid amount.");
        }
    }

    // Debit method
    void debit(double amount) {
        if (amount <= 0) {
            System.out.println("Invalid amount.");
        } else if (amount > balance) {
            System.out.println("Insufficient balance.");
        } else {
            balance = balance - amount;
            System.out.println("Amount debited: " + amount);
        }
    }

    // Check balance
    void checkBalance() {
        System.out.println("Current Balance: " + balance);
    }
}

// Inheritance
class SavingsAccount extends Bank {

    SavingsAccount(String name, int accountNumber, int pin, double balance) {
        super(name, accountNumber, pin, balance);
    }

    // Method Overriding
    @Override
    void bankType() {
        System.out.println("Account Type: Savings Account");
    }
}

// Another child class
class CurrentAccount extends Bank {

    CurrentAccount(String name, int accountNumber, int pin, double balance) {
        super(name, accountNumber, pin, balance);
    }

    // Method Overriding
    @Override
    void bankType() {
        System.out.println("Account Type: Current Account");
    }
}

// Main class
public class BankApplication {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // Object creation
        Bank b = new SavingsAccount("Thanishka", 101, 1234, 5000);

        System.out.println("===== BANK APPLICATION =====");

        System.out.println("Name: " + b.name);
        System.out.println("Account Number: " + b.accountNumber);

        System.out.print("Enter PIN: ");
        int enteredPin = sc.nextInt();

        if (b.checkPin(enteredPin)) {

            System.out.println("Login successful.");

            b.bankType();

            int choice;
            double amount;

            do {
                System.out.println("\n1. Credit");
                System.out.println("2. Credit with Mode");
                System.out.println("3. Debit");
                System.out.println("4. Check Balance");
                System.out.println("5. Exit");

                System.out.print("Enter choice: ");
                choice = sc.nextInt();

                switch (choice) {

                    case 1:
                        System.out.print("Enter amount: ");
                        amount = sc.nextDouble();
                        b.credit(amount);
                        break;

                    case 2:
                        System.out.print("Enter amount: ");
                        amount = sc.nextDouble();

                        System.out.print("Enter mode: ");
                        String mode = sc.next();

                        b.credit(amount, mode);
                        break;

                    case 3:
                        System.out.print("Enter amount: ");
                        amount = sc.nextDouble();
                        b.debit(amount);
                        break;

                    case 4:
                        b.checkBalance();
                        break;

                    case 5:
                        System.out.println("Thank you!");
                        break;

                    default:
                        System.out.println("Invalid choice.");
                }

            } while (choice != 5);

        } else {
            System.out.println("Wrong PIN.");
        }

        sc.close();
    }
}