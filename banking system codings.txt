import java.util.Scanner;
/* Interface */
interface Transaction {
void deposit(double amount);
void withdraw(double amount);
}
/* Abstract Class */
abstract class BankAccount implements Transaction {
private double balance;
BankAccount(double balance) {
this.balance = balance;
}
double getBalance() {
return balance;
}
protected void setBalance(double balance) {
this.balance = balance;
}
public void deposit(double amount) {
if (amount > 0) {
balance += amount;
System.out.println("Deposited: " + amount);
System.out.println("Balance: " + balance);
} else {
System.out.println("Invalid deposit amount");
}
}
public abstract void withdraw(double amount);
}
/* Savings Account */
class SavingsAccount extends BankAccount {
SavingsAccount(double balance) {
super(balance);
}
public void withdraw(double amount) {
if (amount > 5000) {
System.out.println("Savings: Cannot withdraw more than 5000");
} else if (amount <= getBalance()) {
setBalance(getBalance() - amount);
System.out.println("Withdrawn: " + amount);
System.out.println("Balance: " + getBalance());
} else {
System.out.println("Savings: Insufficient balance");
}
}
}
/* Current Account */
class CurrentAccount extends BankAccount {
CurrentAccount(double balance) {
super(balance);
}
public void withdraw(double amount) {
if (amount <= getBalance()) {
setBalance(getBalance() - amount);
System.out.println("Withdrawn: " + amount);
System.out.println("Balance: " + getBalance());
} else {
System.out.println("Current: Insufficient balance");
}
}
}
/* Main Class */
public class Main {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
SavingsAccount savings = new SavingsAccount(10000);
CurrentAccount current = new CurrentAccount(20000);
while (true) {
System.out.println("\n--- BANK MENU ---");
System.out.println("1. Deposit Savings");
System.out.println("2. Withdraw Savings");
System.out.println("3. Deposit Current");
System.out.println("4. Withdraw Current");
System.out.println("5. Check Balance");
System.out.println("6. Exit");
System.out.print("Enter choice: ");
int choice = sc.nextInt();
switch (choice) {
case 1:
System.out.print("Enter amount: ");
savings.deposit(sc.nextDouble());
break;
case 2:
System.out.print("Enter amount: ");
savings.withdraw(sc.nextDouble());
break;
case 3:
System.out.print("Enter amount: ");
current.deposit(sc.nextDouble());
break;
case 4:
System.out.print("Enter amount: ");
current.withdraw(sc.nextDouble());
break;
case 5:
System.out.println("Savings Balance: " + savings.getBalance());
System.out.println("Current Balance: " + current.getBalance());
break;
case 6:
System.out.println("Thank you!");
sc.close();
System.exit(0);
default:
System.out.println("Invalid choice");
}
}
}
}