class Account:
    def __init__(self, name, balance=0):
        self.name = name
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
        return self.balance

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient funds!")
            return None
        else:
            self.balance -= amount
            return self.balance


class HouseholdAccount(Account):
    def __init__(self, name, balance=0):
        super().__init__(name, balance)
        self.categories = {
            "Healthcare": Account("Healthcare"),
            "Education": Account("Education"),
            "Cleaning Supplies": Account("Cleaning Supplies"),
            "Child Care": Account("Child Care"),
            "Entertainment": Account("Entertainment")
        }

    def deposit(self, category, amount):
        if category in self.categories:
            self.categories[category].deposit(amount)
            self.balance += amount
            return self.balance
        else:
            print("Invalid category!")
            return None

    def withdraw(self, category, amount):
        if category in self.categories:
            if self.categories[category].withdraw(amount):
                self.balance -= amount
                return self.balance
            else:
                print("Insufficient funds in category!")
                return None
        else:
            print("Invalid category!")
            return None


if __name__ == "__main__":
    household = HouseholdAccount("Household Account")
    household.deposit("Salary", 5000)
    household.deposit("Healthcare", 200)
    household.withdraw("Healthcare", 50)
    household.withdraw("Groceries", 100)  # Invalid category
    print(household.balance)
