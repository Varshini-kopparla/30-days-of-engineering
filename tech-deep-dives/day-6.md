# React Fundamentals

## What I Learned

Today I revised important React concepts commonly used in:
- frontend development
- modern web applications
- software engineering interviews

React is one of the most popular frontend libraries for building interactive and reusable user interfaces.

---

# 1. What is React?

React is a JavaScript library used for building user interfaces using reusable components.

It was developed by:
> Meta (Facebook)

React mainly focuses on:
- component-based UI development
- efficient rendering
- dynamic frontend applications

---

# Main Advantages of React

- reusable components
- faster UI updates using Virtual DOM
- clean frontend architecture
- easier frontend-backend integration
- scalable UI development

---

# 2. What is a Component?

A component is:
> a reusable UI block

Examples:
- Navbar
- Login Form
- Product Card
- Sidebar
- Button

Large applications are built by combining multiple components together.

---

# Functional Component Example

```jsx
function Welcome() {
  return <h1>Hello React</h1>;
}

export default Welcome;
```

---

# 3. JSX (JavaScript XML)

JSX allows writing:
> HTML-like code inside JavaScript

Example:

```jsx
const element = <h1>Hello World</h1>;
```

---

# Why JSX is Useful

Benefits:
- cleaner UI code
- easier readability
- simpler frontend development

JSX is eventually converted into:
> normal JavaScript

by React internally.

---

# 4. Props in React

Props are used to:
> pass data from parent component to child component

---

# Example

```jsx
function User(props) {
  return <h1>Hello {props.name}</h1>;
}

export default User;
```

Using component:

```jsx
<User name="Varshini" />
```

Output:

```txt
Hello Varshini
```

---

# Key Learning

Props are:
- read-only
- passed from parent → child

Used for:
- dynamic UI rendering
- reusable components

---

# 5. State in React

State stores:
> component-specific data

When state changes:
> React automatically updates the UI

---

# useState Hook Example

```jsx
import { useState } from "react";

function Counter() {

  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}

export default Counter;
```

---

# Key Learning

```jsx
const [count, setCount]
```

- `count` → current state value
- `setCount` → updates state

State updates automatically trigger:
> component re-rendering

---

# 6. useEffect Hook

Used for:
- API calls
- side effects
- lifecycle events

---

# Example

```jsx
import { useEffect } from "react";

function App() {

  useEffect(() => {
    console.log("Component Loaded");
  }, []);

  return <h1>React App</h1>;
}

export default App;
```

---

# Empty Dependency Array

```jsx
[]
```

means:
> run only once when component loads

Similar to:
> componentDidMount()

in older class components.

---

# 7. Event Handling in React

React handles user interactions using functions.

---

# Example

```jsx
function Button() {

  const handleClick = () => {
    alert("Button Clicked");
  };

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}

export default Button;
```

---

# Common Events

| Event | Usage |
|---|---|
| onClick | button clicks |
| onChange | input changes |
| onSubmit | form submission |
| onMouseOver | hover events |

---

# 8. Form Handling in React

Forms are usually controlled using:
> React State

---

# Example

```jsx
import { useState } from "react";

function LoginForm() {

  const [name, setName] = useState("");

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />

      <h2>{name}</h2>
    </div>
  );
}

export default LoginForm;
```

---

# Key Learning

```jsx
onChange
```

updates state whenever user types.

This creates:
> controlled components

where React controls form data.

---

# 9. Conditional Rendering

Conditional rendering displays UI based on conditions.

---

# Example

```jsx
function App() {

  const isLoggedIn = true;

  return (
    <div>
      {isLoggedIn ? <h1>Welcome</h1> : <h1>Please Login</h1>}
    </div>
  );
}

export default App;
```

---

# Key Learning

React commonly uses:
- ternary operators
- logical operators

for conditional UI rendering.

---

# 10. List Rendering

Used for displaying multiple items dynamically.

---

# Example

```jsx
function App() {

  const users = ["John", "Alice", "Bob"];

  return (
    <div>
      {users.map((user, index) => (
        <p key={index}>{user}</p>
      ))}
    </div>
  );
}

export default App;
```

---

# Why "key" is Important

Keys help React:
- identify elements efficiently
- optimize rerendering
- track updated items

Without keys:
- React rendering becomes inefficient.

---

# 11. API Calls in React

Frontend communicates with backend APIs using:
- fetch
- axios

---

# Example

```jsx
import { useEffect, useState } from "react";

function Users() {

  const [users, setUsers] = useState([]);

  useEffect(() => {

    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setUsers(data));

  }, []);

  return (
    <div>
      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default Users;
```

---

# API Flow

```txt
Frontend
    ↓
API Request
    ↓
Backend Server
    ↓
Database
    ↓
Response Returned
    ↓
React Updates UI
```

---

# 12. React Component Flow

```txt
User Action
     ↓
React State Updates
     ↓
UI Re-renders
     ↓
API Calls (if needed)
     ↓
Backend Server
     ↓
Database
     ↓
Response Returned
     ↓
UI Updated
```

This is one of the most important frontend flows to understand.

---

# 13. Virtual DOM

React uses:
> Virtual DOM

to improve performance.

Instead of updating entire webpage:
- React updates only changed elements

---

# Benefits of Virtual DOM

- faster rendering
- efficient UI updates
- better frontend performance
- reduced DOM operations

---

# 14. React Router Basics

React Router handles:
> frontend page navigation

without reloading the webpage.

---

# Example

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {

  return (
    <BrowserRouter>

      <Routes>

        <Route path="/" element={<Home />} />

        <Route path="/about" element={<About />} />

      </Routes>

    </BrowserRouter>
  );
}

export default App;
```

---

# Key Learning

React Router enables:
- SPA navigation (Single Page Applications)
- dynamic frontend routing
- smoother user experience

---

# 15. React vs Next.js

| Feature | React | Next.js |
|---|---|---|
| Type | UI Library | React Framework |
| Rendering | Client-side | SSR + CSR |
| Routing | Manual | Built-in |
| Setup | More configuration | Production optimized |

---

# Key Understanding

## React
Mainly focuses on:
- building UI components

---

## Next.js
Built on top of React and adds:
- server-side rendering
- routing
- backend capabilities
- production optimizations

---

# Main Takeaways

Important React concepts learned:
- components
- JSX
- props
- state
- hooks
- useEffect
- event handling
- forms
- API calls
- Virtual DOM
- routing

React follows a component-driven architecture where:
- state changes trigger UI updates
- reusable components simplify frontend development
- Virtual DOM improves rendering performance

React is extremely important for:
- frontend engineering
- full-stack development
- modern web applications
- software engineering interviews.
