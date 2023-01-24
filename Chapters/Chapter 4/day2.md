# Chapter 4 - Day 2

## 1. Instead of console logging the result after the script executes, I want you to:
- Make a new variable named greeting using useState
- Set the greeting variable to the response of the script call
- Create a `<p>` tag after the `<div className={styles.flex}>` tag
- Put the greeting variable inside of that `<p>` tag. This will make the result of your script show on your webpage! It should look something like this.

## 2a. I deployed a contract called SimpleTest to an account with an address of 0x6c0d53c676256e8c. I want you to make a button that, when clicked, executes a script to read the number variable from that contract. If you're curious, you can see the contract here: https://flow-view-source.com/testnet/account/0x6c0d53c676256e8c/contract/SimpleTest

## Submit all the code you used to call the script, and the result of the script.

## 2b. Then, I want you to remove the button, and make the script execute every time the page refreshes.

## Submit all the code you used to do this.

### 1. code:
`
import Head from 'next/head'
import styles from '@/styles/Home.module.css'
import Nav from '@/components/Nav.jsx'
import { useState, useEffect } from 'react'
import * as fcl from "@onflow/fcl"

export default function Home() {
  const [newGreeting, setNewGreeting] = useState('')
  const [greeting, setGreeting] = useState('')

  function runTransaction() {
    console.log(newGreeting)
  }

  async function executeScript() {
    const response = await fcl.query({
      cadence: `
      import HelloWorld from 0x78117cc207f6457a

      pub fun main(): String {
          return HelloWorld.greeting
      }
      `,
      args: (arg, t) => [] // ARGUMENTS GO IN HERE
    })

    console.log("Response from our script: " + response);
    setGreeting(response);
  }

  useEffect(() => {
    executeScript()
  }, [])

  return (
    <div className={styles.container}>
      <Head>
        <title>Emerald DApp</title>
        <meta name="description" content="Created by Emerald Academy" />
        <link rel="icon" href="https://i.imgur.com/hvNtbgD.png" />
      </Head>
      <Nav></Nav>

      <main className={styles.main}>
        <h1 className={styles.title}>
          Welcome to my <a href="https://www.youtube.com/watch?v=E80BlAEVwRA&list=PLvcQxi9WyGdGUx-a4rCsLWn_WKlA9YAXP" target="_blank" rel='noreferrer'>Emerald DApp!</a>
        </h1>
        <p>
          This is whatever text
        </p>
        <div className={styles.flex}>
          <button onClick={runTransaction}>Run Transaction</button>
          <input onChange={(e) => setNewGreeting(e.target.value)} placeholder='Hello, bitches' />
        </div>
        <p>
          {greeting}
        </p>

      </main>
    </div>
  )
}
`

### 2a. code: 
`
import Head from 'next/head'
import styles from '@/styles/Home.module.css'
import Nav from '@/components/Nav.jsx'
import { useState, useEffect } from 'react'
import * as fcl from "@onflow/fcl"

export default function Home() {
  const [newGreeting, setNewGreeting] = useState('')
  const [greeting, setGreeting] = useState('')

  function runTransaction() {
    console.log(newGreeting)
  }

  async function executeScript() {
    const response = await fcl.query({
      cadence: `
      import HelloWorld from 0x78117cc207f6457a

      pub fun main(): String {
          return HelloWorld.greeting
      }
      `,
      args: (arg, t) => [] // ARGUMENTS GO IN HERE
    })

    console.log("Response from our script: " + response);
    setGreeting(response);
  }

  useEffect(() => {
    executeScript()
  }, [])

  async function executeSimpleTest() {
    const response = await fcl.query({
      cadence: `
      import SimpleTest from 0x6c0d53c676256e8c

      pub fun main(): Int {
          return SimpleTest.number
      }
      `,
      args: (arg, t) => [] // ARGUMENTS GO IN HERE
    })

    console.log("Response from Simple Test: " + response);
  }

  return (
    <div className={styles.container}>
      <Head>
        <title>Emerald DApp</title>
        <meta name="description" content="Created by Emerald Academy" />
        <link rel="icon" href="https://i.imgur.com/hvNtbgD.png" />
      </Head>
      <Nav></Nav>

      <main className={styles.main}>
        <h1 className={styles.title}>
          Welcome to my <a href="https://www.youtube.com/watch?v=E80BlAEVwRA&list=PLvcQxi9WyGdGUx-a4rCsLWn_WKlA9YAXP" target="_blank" rel='noreferrer'>Emerald DApp!</a>
        </h1>
        <p>
          This is whatever text
        </p>
        <div className={styles.flex}>
          <button onClick={runTransaction}>Run Transaction</button>
          <input onChange={(e) => setNewGreeting(e.target.value)} placeholder='Hello, bitches' />
        </div>
        <p>
          {greeting}
        </p>
        <br />
        <button onClick={executeSimpleTest}>Simple Test</button>

      </main>
    </div>
  )
} 
`

### 2b. code:
`import Head from 'next/head'
import styles from '@/styles/Home.module.css'
import Nav from '@/components/Nav.jsx'
import { useState, useEffect } from 'react'
import * as fcl from "@onflow/fcl"

export default function Home() {
  const [newGreeting, setNewGreeting] = useState('')
  const [greeting, setGreeting] = useState('')

  function runTransaction() {
    console.log(newGreeting)
  }

  async function executeScript() {
    const response = await fcl.query({
      cadence: `
      import HelloWorld from 0x78117cc207f6457a

      pub fun main(): String {
          return HelloWorld.greeting
      }
      `,
      args: (arg, t) => [] // ARGUMENTS GO IN HERE
    })

    console.log("Response from our script: " + response);
    setGreeting(response);
  }

  useEffect(() => {
    executeScript()
  }, [])

  async function executeSimpleTest() {
    const response = await fcl.query({
      cadence: `
      import SimpleTest from 0x6c0d53c676256e8c

      pub fun main(): Int {
          return SimpleTest.number
      }
      `,
      args: (arg, t) => [] // ARGUMENTS GO IN HERE
    })

    console.log("Response from Simple Test: " + response);
  }


  useEffect(() => {
    executeSimpleTest()
  }, [])

  return (
    <div className={styles.container}>
      <Head>
        <title>Emerald DApp</title>
        <meta name="description" content="Created by Emerald Academy" />
        <link rel="icon" href="https://i.imgur.com/hvNtbgD.png" />
      </Head>
      <Nav></Nav>

      <main className={styles.main}>
        <h1 className={styles.title}>
          Welcome to my <a href="https://www.youtube.com/watch?v=E80BlAEVwRA&list=PLvcQxi9WyGdGUx-a4rCsLWn_WKlA9YAXP" target="_blank" rel='noreferrer'>Emerald DApp!</a>
        </h1>
        <p>
          This is whatever text
        </p>
        <div className={styles.flex}>
          <button onClick={runTransaction}>Run Transaction</button>
          <input onChange={(e) => setNewGreeting(e.target.value)} placeholder='Hello, bitches' />
        </div>
        <p>
          {greeting}
        </p>
      </main>
    </div>
  )
}

`