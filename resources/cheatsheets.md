# 📋 React Cheatsheet - Quick Reference

Your pocket guide to React syntax and patterns!

---

## Imports

```jsx
import React from 'react';
import { useState, useEffect } from 'react';
```

---

## Creating Components

```jsx
// Function Component
function MyComponent() {
  return <div>Hello</div>;
}

// Or with arrow function
const MyComponent = () => {
  return <div>Hello</div>;
};

// With props
function Welcome({ name }) {
  return <h1>Hello {name}</h1>;
}
```

---

## JSX Rules

```jsx
// Must return single root element
return (
  <div>
    <h1>Title</h1>
    <p>Content</p>
  </div>
);

// Use curly braces for expressions
const name = "Alice";
<h1>Hello {name}</h1>

// Use className (not class)
<div className="container">

// Conditional rendering
{condition && <Content />}
{condition ? <A /> : <B />}

// Lists
{items.map(item => <li key={item.id}>{item.name}</li>)}

// Event handlers
<button onClick={handleClick}>Click</button>
<input onChange={handleChange} />
```

---

## Hooks

### useState

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

### useEffect

```jsx
import { useEffect } from 'react';

// Run once on mount
useEffect(() => {
  console.log("Component mounted");
}, []);

// Run when dependency changes
useEffect(() => {
  console.log("Count changed:", count);
}, [count]);

// Cleanup
useEffect(() => {
  const timer = setInterval(() => console.log("tick"), 1000);
  return () => clearInterval(timer);
}, []);
```

### useReducer

```jsx
import { useReducer } from 'react';

const [state, dispatch] = useReducer(reducer, initialState);

dispatch({ type: 'ACTION_TYPE', payload: data });
```

### useContext

```jsx
import { useContext } from 'react';

const value = useContext(MyContext);
```

### useRef

```jsx
import { useRef } from 'react';

const inputRef = useRef(null);
inputRef.current.focus();
```

### useMemo

```jsx
import { useMemo } from 'react';

const memoizedValue = useMemo(() => {
  return expensiveCalculation(a, b);
}, [a, b]);
```

### useCallback

```jsx
import { useCallback } from 'react';

const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

---

## Props

```jsx
// Passing props
<Welcome name="Alice" age={25} />

// Receiving props
function Welcome({ name, age }) {
  return <div>{name}, {age}</div>;
}

// Default props
function Button({ label = "Click me" }) {
  return <button>{label}</button>;
}

// Spread operator
<Component {...props} />
```

---

## Forms

```jsx
function Form() {
  const [formData, setFormData] = useState({
    name: "",
    email: ""
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({
      ...formData,
      [name]: value
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="name"
        value={formData.name}
        onChange={handleChange}
      />
      <input
        type="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Common Patterns

### Conditional Rendering

```jsx
// Option 1
{isLoading ? <Loader /> : <Content />}

// Option 2
{isLoading && <Loader />}

// Option 3
{status === 'loading' && <Loader />}
{status === 'error' && <Error />}
{status === 'success' && <Content />}
```

### Rendering Lists

```jsx
{items.map((item) => (
  <div key={item.id}>
    <h2>{item.name}</h2>
  </div>
))}
```

### Handling API Calls

```jsx
useEffect(() => {
  const fetchData = async () => {
    try {
      const response = await fetch(url);
      const data = await response.json();
      setData(data);
    } catch (error) {
      setError(error.message);
    } finally {
      setLoading(false);
    }
  };

  fetchData();
}, []);
```

### Lifting State

```jsx
// Parent component
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Child1 count={count} setCount={setCount} />
      <Child2 count={count} />
    </div>
  );
}

// Child component
function Child1({ count, setCount }) {
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}

function Child2({ count }) {
  return <p>Count: {count}</p>;
}
```

---

## Styling

```jsx
// Inline styles
<div style={{ color: 'red', fontSize: '16px' }}>Hello</div>

// CSS classes
<div className="my-class">Hello</div>

// Conditional classes
<div className={`card ${isActive ? 'active' : ''}`}>

// Using classnames package
<div className={classNames('card', { active: isActive })}>
```

---

## Common Commands

```bash
# Create new React app
npm create vite@latest my-app -- --template react

# Start development server
npm run dev

# Build for production
npm run build

# Install package
npm install package-name

# Run tests
npm test
```

---

## File Structure

```
src/
├── components/
│   ├── Header.jsx
│   ├── Footer.jsx
│   └── Button.jsx
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   └── Contact.jsx
├── hooks/
│   ├── useCustom.js
│   └── useFetch.js
├── services/
│   └── api.js
├── styles/
│   └── App.css
├── App.jsx
└── index.js
```

---

## Debugging

```jsx
// Console logging
console.log("Value:", value);
console.table(array);
console.error("Error:", error);

// React DevTools
// Install browser extension to inspect components

// Network tab
// Check API requests and responses
```

---

## Common Errors & Fixes

| Error | Fix |
|-------|-----|
| `React is not defined` | Import React |
| `Hooks can only be at top level` | Don't call hooks conditionally |
| `Key prop is required in list` | Add unique key to list items |
| `Cannot update component from another component` | Lift state up |
| `Infinite re-renders` | Check useEffect dependencies |

---

*Keep this handy while coding!* 📚

---

*Last updated: June 2024*
