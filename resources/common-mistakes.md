# ⚠️ Common React Mistakes (And How to Avoid Them)

Learn from others' mistakes so you don't make them yourself!

---

## Mistake 1: Mutating State Directly ❌

```jsx
// WRONG
this.state.count = this.state.count + 1;

// WRONG (even with hooks)
state.name = "New Name";

// RIGHT
setState(state => ({...state, count: state.count + 1}));

// RIGHT (with hooks)
setName("New Name");
```

**Why?** React won't detect the change and won't re-render.

---

## Mistake 2: Using Index as Key in Lists ❌

```jsx
// WRONG
{items.map((item, index) => <Item key={index}>{item}</Item>)}

// RIGHT
{items.map((item) => <Item key={item.id}>{item}</Item>)}
```

**Why?** If list order changes, React gets confused about which item is which.

---

## Mistake 3: Missing Dependencies in useEffect ❌

```jsx
// WRONG - infinite loop!
useEffect(() => {
  fetchData();
}, ); // No dependency array

// RIGHT
useEffect(() => {
  fetchData();
}, []); // Runs once

// RIGHT
useEffect(() => {
  fetchData(userId);
}, [userId]); // Runs when userId changes
```

---

## Mistake 4: Not Cleaning Up Effects ❌

```jsx
// WRONG - memory leak!
useEffect(() => {
  window.addEventListener("resize", handleResize);
  // Never removes listener!
});

// RIGHT
useEffect(() => {
  window.addEventListener("resize", handleResize);
  
  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);
```

---

## Mistake 5: Calling Hooks Conditionally ❌

```jsx
// WRONG
if (someCondition) {
  const [state, setState] = useState(0);
}

// RIGHT
const [state, setState] = useState(0);
if (someCondition) {
  // Use the state here
}
```

**Why?** React relies on hook call order staying the same.

---

## Mistake 6: Not Handling Async/Await Errors ❌

```jsx
// WRONG
useEffect(() => {
  async function fetchData() {
    const data = await fetch(url); // What if it fails?
    setData(data);
  }
  fetchData();
}, []);

// RIGHT
useEffect(() => {
  async function fetchData() {
    try {
      const res = await fetch(url);
      const data = await res.json();
      setData(data);
    } catch (error) {
      setError(error.message);
    }
  }
  fetchData();
}, []);
```

---

## Mistake 7: Rendering Functions Instead of Components ❌

```jsx
// WRONG
<MyComponent render={() => <div>Hello</div>} />

// Use render props or children instead
<MyComponent>{() => <div>Hello</div>}</MyComponent>

// Or just pass content as children
<MyComponent><div>Hello</div></MyComponent>
```

---

## Mistake 8: Creating New Objects/Arrays in Render ❌

```jsx
// WRONG - creates new object every render
function MyComponent() {
  const styles = { color: "red" }; // New object each time!
  return <div style={styles}>Hello</div>;
}

// RIGHT
const styles = { color: "red" }; // Outside component

function MyComponent() {
  return <div style={styles}>Hello</div>;
}
```

---

## Mistake 9: Forgetting e.preventDefault() in Forms ❌

```jsx
// WRONG - page reloads!
function Form() {
  const handleSubmit = (e) => {
    // POST request goes here
  };
  return <form onSubmit={handleSubmit}></form>;
}

// RIGHT
function Form() {
  const handleSubmit = (e) => {
    e.preventDefault();
    // POST request goes here
  };
  return <form onSubmit={handleSubmit}></form>;
}
```

---

## Mistake 10: Comparing Objects/Arrays with === ❌

```jsx
// WRONG
const newState = { ...oldState };
if (newState === oldState) { // Always false!
  // Even though content is the same
}

// RIGHT - check content instead
if (JSON.stringify(newState) === JSON.stringify(oldState)) {
  // Or use deep comparison library
}
```

---

## Mistake 11: Not Unsubscribing from Subscriptions ❌

```jsx
// WRONG - subscription never ends
useEffect(() => {
  const subscription = observable.subscribe(data => {
    setData(data);
  });
});

// RIGHT
useEffect(() => {
  const subscription = observable.subscribe(data => {
    setData(data);
  });
  
  return () => subscription.unsubscribe();
}, []);
```

---

## Mistake 12: Modifying Props ❌

```jsx
// WRONG
function MyComponent(props) {
  props.name = "New Name"; // Never do this!
  return <div>{props.name}</div>;
}

// RIGHT
function MyComponent({ name }) {
  // Read-only
  return <div>{name}</div>;
}
```

---

## 🧠 Quick Checklist

- [ ] Are you mutating state directly?
- [ ] Are you using array index as key?
- [ ] Do your useEffects have proper dependencies?
- [ ] Are you handling errors in async code?
- [ ] Are you calling hooks conditionally?
- [ ] Are you cleaning up effects?
- [ ] Are you preventing default form behavior?

**Check these and you'll avoid 80% of React bugs!** ✨

---

*Learn from mistakes = Become a better developer* 🚀
