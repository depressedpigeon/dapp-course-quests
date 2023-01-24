# Chapter 4 - Day 1

### 1. How did we get the address of the user? Please explain in words and then in code.
We added a button to take care of Authentication, that lets the user log in by selected wallet. provided by the configuration file and stores the authenticated account in the *user* variable.
`<button onClick={handleAuthentication}>Log in</button>`
`  function handleAuthentication() {
    if (user.loggenIn) {
      fcl.unauthenticate();
    } else {
      fcl.authenticate();
    }
  }`

### 2. What do fcl.authenticate and fcl.unauthenticate do?
fcl.authenticate used to log in the user
fcl.unauthenticate used to log the user out

### 3. Why did we make a config.js file? What does it do?
config.js connects the Dapp to Flow testnet and manages the options for the log in.

### 4. What does our useEffect do?
useEffect runs the function every time something happens. If there is nothing in the `[]` brackets, it runs everytime the page is refreshed.

### 5. How do we import FCL?
We install the FCL and add `import * as fcl from "@onflow/fcl";` at the top of our file.

### 6. What does fcl.currentUser.subscribe(setUser); do?
It is subscribes to the *user* value and makes sure the variable keeps its value if the page is refreshed.