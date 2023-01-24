# Chapter 3 - Day 2

## Please answer in the language of your choice.

### Explain why we wouldn't call changeGreeting in a script.
Scripts are for viewing or reading data, while to modify anything, like we want in changeGreeting, it requires a transaction.

### What does the AuthAccount mean in the prepare phase of the transaction?
AuthAccount accesses the necessary account info to confirm the transaction. no account = no tokens = no transaction. 

### What is the difference between the prepare phase and the execute phase in the transaction?
Prepare phase authorizes the account to execute the transaction, while execute phase calls the function to change the data. 

## This is the hardest quest so far, so if it takes you some time, do not worry! I can help you in the Discord if you have questions.

### Add two new things inside your contract:

### A variable named myNumber that has type Int (set it to 0 when the contract is deployed)
### A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
``` javascript 
pub contract HelloWorld {

    pub var greeting: String
    pub var myNumber: Int

    pub fun changeGreeting(newGreeting: String) {
      self.greeting = newGreeting
    }

    pub fun updateMyNumber(newNumber: Int) {
    self.myNumber = newNumber
    }

    init() {
      self.greeting = "Hello, world"
      self.myNumber = 0
    }
}
```

### Add a script that reads myNumber from the contract
``` javascript import HelloWorld from 0x01

pub fun main(): Int {
    return HelloWorld.myNumber
}
```

### Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.
``` javascript 
import HelloWorld from 0x01

transaction(myNewNumber: Int) {

  prepare(signer: AuthAccount) {}

  execute {
    HelloNumber.changeNumber(newNumber: myNewNumber)
  }
}
```