# ⚙️ Intermediate: Level Up Your React Skills

You're doing great! Now let's explore more advanced React features and patterns that make real-world applications possible.

---

## 📚 What You'll Learn

- ✅ Advanced State Management (useReducer)
- ✅ Side Effects (useEffect)
- ✅ Conditional Rendering Patterns
- ✅ API Integration & Data Fetching
- ✅ Component Lifecycle
- ✅ Performance Optimization basics
- ✅ Error Handling

---

## 🎯 Topics

<a id="component-lifecycle-hooks"></a>
### 1️⃣ useEffect Hook (Advanced State) - 60 mins

**What is useEffect?**
> Allows you to perform side effects in functional components
> Side effects = data fetching, subscriptions, timers, etc.

**Three variations:**

```jsx
// 1. Runs after EVERY render
useEffect(() => {
  console.log("Component rendered");
});

// 2. Runs ONCE (on mount)
useEffect(() => {
  console.log("Component mounted");
}, []);

// 3. Runs when dependencies change
useEffect(() => {
  console.log("Count changed:", count);
}, [count]);
```

**Real example - Fetch data:**

```jsx
import { useState, useEffect } from "react";

function Posts() {
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("https://api.example.com/posts")
      .then((res) => res.json())
      .then((data) => {
        setPosts(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err.message);
        setLoading(false);
      });
  }, []); // Runs once

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

**Cleanup function:**

```jsx
useEffect(() => {
  // Setup
  const timer = setInterval(() => {
    console.log("Tick");
  }, 1000);

  // Cleanup (runs before component unmounts)
  return () => clearInterval(timer);
}, []);
```

---

<a id="api-integration-data-fetching"></a>
### 2️⃣ API Integration (75 mins)

**What's an API?**
> A way for your app to talk to a server and get data

**Fetching with Async/Await (Cleaner):**

```jsx
useEffect(() => {
  async function fetchData() {
    try {
      const response = await fetch("https://api.example.com/users");
      const data = await response.json();
      setUsers(data);
    } catch (error) {
      setError(error.message);
    } finally {
      setLoading(false);
    }
  }

  fetchData();
}, []);
```

**Conditional fetching:**

```jsx
useEffect(() => {
  if (!userId) return; // Don't fetch if no userId

  async function fetchUser() {
    const response = await fetch(`/api/users/${userId}`);
    const data = await response.json();
    setUser(data);
  }

  fetchUser();
}, [userId]); // Re-fetch when userId changes
```

**Popular APIs for practice:**
- JSONPlaceholder (fake data)
- OpenWeatherMap (weather)
- GitHub API (repositories)
- OMDb API (movies)

---

### 3️⃣ Advanced Conditional Rendering (45 mins)

**Pattern 1: Ternary Operator**

```jsx
{isLoading ? <Loader /> : <Content />}
```

**Pattern 2: Logical AND (&&)**

```jsx
{hasPermission && <AdminPanel />}
```

**Pattern 3: Switch Statement**

```jsx
function Status({ status }) {
  switch (status) {
    case "loading":
      return <p>Loading...</p>;
    case "error":
      return <p>Error occurred</p>;
    case "success":
      return <p>Success!</p>;
    default:
      return <p>Unknown status</p>;
  }
}
```

**Pattern 4: Multiple conditions**

```jsx
{!isLoading && !error && posts.length > 0 && (
  <PostList posts={posts} />
)}
```

---

### 4️⃣ useReducer (Complex State) - 60 mins

**When to use:** When state logic is complex with multiple related values

```jsx
import { useReducer } from "react";

function Counter() {
  const initialState = { count: 0 };

  function reducer(state, action) {
    switch (action.type) {
      case "INCREMENT":
        return { count: state.count + 1 };
      case "DECREMENT":
        return { count: state.count - 1 };
      case "RESET":
        return { count: 0 };
      default:
        return state;
    }
  }

  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
      <button onClick={() => dispatch({ type: "RESET" })}>Reset</button>
    </div>
  );
}
```

---

### 5️⃣ Performance Optimization (45 mins)

**Problem:** Components re-render unnecessarily

**Solution 1: useMemo**

```jsx
import { useMemo } from "react";

function ExpensiveComponent({ data }) {
  // Only recalculate when 'data' changes
  const processedData = useMemo(() => {
    return expensiveCalculation(data);
  }, [data]);

  return <div>{processedData}</div>;
}
```

**Solution 2: useCallback**

```jsx
import { useCallback } from "react";

function Parent({ items }) {
  // Function stays the same between renders (unless items changes)
  const handleClick = useCallback((id) => {
    deleteItem(id);
  }, []);

  return <Child items={items} onClick={handleClick} />;
}
```

---

### 6️⃣ Error Handling (30 mins)

**Try-catch pattern:**

```jsx
useEffect(() => {
  async function fetchData() {
    try {
      const response = await fetch(url);
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      const data = await response.json();
      setData(data);
    } catch (error) {
      setError(error.message);
    }
  }

  fetchData();
}, []);
```

**Error Boundary (for rendering errors):**

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong</h1>;
    }
    return this.props.children;
  }
}
```

---

## 🎮 Projects

### Project 1: Weather App

Fetch and display weather data:
- Search for city
- Show temperature, humidity, description
- Display weather icon
- Handle loading and error states

**Concepts:** API integration, useEffect, conditional rendering, state management

---

### Project 2: GitHub User Finder

Find GitHub users:
- Search by username
- Display user info (avatar, name, bio, repos)
- Show repositories list
- Error handling for not found users

**Concepts:** API, async/await, complex state, list rendering

---

## 📚 Resources

- [useEffect Guide](https://react.dev/reference/react/useEffect)
- [Fetching Data](https://react.dev/learn/synchronizing-with-effects#fetching-data)
- [useReducer](https://react.dev/reference/react/useReducer)

---

## ✅ Checklist

- [ ] I understand useEffect and its dependencies
- [ ] I can fetch data from APIs
- [ ] I know multiple conditional rendering patterns
- [ ] I can use useReducer for complex state
- [ ] I understand performance optimization basics
- [ ] I can handle errors in async code
- [ ] I completed the practice projects

**You're now ready for real-world React development!** 🎉

---

*Great progress! You're thinking like a React developer now!* 💪
