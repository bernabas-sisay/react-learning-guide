# 🛠️ Core Concepts: Building React Applications

Now that you understand the basics, let's dive into the actual building blocks of React! This module covers the essentials you'll use in every project.

---

## 📚 What You'll Learn

- ✅ JSX in detail - writing HTML in JavaScript
- ✅ Components - functional and reusable
- ✅ Props - passing data between components
- ✅ State - managing data that changes
- ✅ Events - handling user interactions
- ✅ Lists and rendering - displaying multiple items

---

## 🎯 Learning Path

### 1️⃣ JSX Deep Dive (30 mins)

**What is JSX?**
> JSX = JavaScript XML. It lets you write HTML-like code in JavaScript.

```jsx
// This is JSX
const element = <h1>Hello React!</h1>;

// It becomes this
const element = React.createElement("h1", null, "Hello React!");
```

**JSX Rules:**

❌ **Wrong:**
```jsx
return (
  <h1>Hello</h1>
  <p>World</p>
);
```

✅ **Right:**
```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

**Using variables in JSX:**

```jsx
function Greeting() {
  const name = "Alice";
  const age = 25;
  
  return (
    <div>
      <h1>Hello {name}!</h1>
      <p>You are {age} years old</p>
    </div>
  );
}
```

**Conditional rendering:**

```jsx
function Status({ isLogged }) {
  return (
    <div>
      {isLogged ? <p>Welcome back!</p> : <p>Please login</p>}
    </div>
  );
}
```

---

### 2️⃣ Components (45 mins)

**What are components?**
> Reusable, independent pieces of the UI

**Functional Components (Modern):**

```jsx
function Button() {
  return <button>Click me</button>;
}
```

**Components with arguments (Props):**

```jsx
function Greeting(props) {
  return <h1>Hello {props.name}!</h1>;
}

// Using it:
<Greeting name="Bob" />
<Greeting name="Sarah" />
```

**Destructuring props:**

```jsx
function Greeting({ name, age }) {
  return (
    <div>
      <h1>Hello {name}!</h1>
      <p>Age: {age}</p>
    </div>
  );
}
```

---

### 3️⃣ Props & State (60 mins)

**Props:** Data passed FROM parent TO child

```jsx
function Parent() {
  return <Child message="Hello from Parent!" />;
}

function Child({ message }) {
  return <p>{message}</p>;
}
```

**State:** Data that can change INSIDE a component

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}
```

**Props vs State:**

| Props | State |
|-------|-------|
| Passed from parent | Lives in component |
| Read-only | Can be changed |
| Cannot modify | Use setState to change |

---

### 4️⃣ Events & User Interactions (45 mins)

**Common Events:**

| Event | Triggered When |
|-------|-----------------|
| `onClick` | Element clicked |
| `onChange` | Input value changes |
| `onSubmit` | Form submitted |
| `onHover` | Mouse hovers |

**Event handling:**

```jsx
function Click Counter() {
  const [clicks, setClicks] = useState(0);

  function handleClick() {
    setClicks(clicks + 1);
  }

  return (
    <div>
      <p>Clicks: {clicks}</p>
      <button onClick={handleClick}>Click</button>
    </div>
  );
}
```

**Form example:**

```jsx
function Form() {
  const [name, setName] = useState("");

  const handleChange = (e) => {
    setName(e.target.value);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Submitted:", name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text" 
        value={name} 
        onChange={handleChange}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

### 5️⃣ Lists & Rendering (45 mins)

**Rendering lists:**

```jsx
function TodoList() {
  const todos = ["Learn React", "Build a project", "Deploy"];

  return (
    <ul>
      {todos.map((todo, index) => (
        <li key={index}>{todo}</li>
      ))}
    </ul>
  );
}
```

**Better with objects:**

```jsx
function UserList() {
  const users = [
    { id: 1, name: "Alice", age: 25 },
    { id: 2, name: "Bob", age: 30 },
    { id: 3, name: "Carol", age: 28 }
  ];

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.name} - {user.age} years
        </li>
      ))}
    </ul>
  );
}
```

**Important:** Always use a unique `key` prop when rendering lists!

---

## 🎮 Practice Exercises

### Exercise 1: Simple Counter Component ⭐

Create a component that:
- Displays current count
- Has buttons to increase/decrease

**Starter:**
```jsx
import { useState } from "react";

function Counter() {
  // TODO: Add state and buttons
  return <div></div>;
}

export default Counter;
```

---

### Exercise 2: Todo Item Component ⭐⭐

Create a component that displays a todo with:
- Todo text
- Checkbox to mark complete
- Delete button

---

### Exercise 3: User Profile Component ⭐⭐

Create a component that shows:
- User name (prop)
- User description (prop)
- Edit button that changes name on click

---

## 💡 Best Practices

### ✅ DO:
- ✅ Keep components small and focused
- ✅ Use meaningful names for components
- ✅ Lift state up when multiple children need it
- ✅ Use keys when rendering lists

### ❌ DON'T:
- ❌ Modify state directly: `state = newValue` ❌
- ❌ Modify props
- ❌ Use index as key in lists (if list can change)
- ❌ Create new objects/arrays in every render

---

## 📚 Resources

- [React Main Concepts](https://react.dev/learn)
- [JSX Introduction](https://react.dev/learn/writing-markup-with-jsx)
- [useState Documentation](https://react.dev/reference/react/useState)

---

## ✅ Module Checklist

- [ ] I can write and use JSX
- [ ] I can create function components
- [ ] I understand the difference between props and state
- [ ] I can use useState hook
- [ ] I can handle events and forms
- [ ] I can render lists with .map()
- [ ] I completed all practice exercises

**Ready for the next module?** Let's dive into intermediate concepts! 🚀

---

*Keep going! You're building real React skills now!* 💪
