# 🔧 Troubleshooting Guide - Fix Common Issues

Stuck? You're not alone! Here are solutions to common React problems.

---

## Setup Issues

### "npm: command not found"

**Problem:** npm isn't in your system PATH

**Solution:**
1. Install Node.js from [nodejs.org](https://nodejs.org)
2. Restart your terminal
3. Try `npm -v` again

---

### "React is not defined"

**Problem:** Forgot to import React

**Solution:**
```jsx
// Add this at the top of your file
import React from 'react';

// Or if using JSX without React import:
// Create React App 5+ doesn't need it, but Vite might
```

---

## Component Issues

### Component not rendering

**Checklist:**
- [ ] Did you export the component? `export default MyComponent;`
- [ ] Did you import it? `import MyComponent from './components/MyComponent';`
- [ ] Are you using it correctly? `<MyComponent />`
- [ ] Check browser console for errors

---

### "Hooks can only be called at the top level"

**Problem:** You're calling hooks conditionally

```jsx
// WRONG
if (condition) {
  const [state, setState] = useState(0);
}

// RIGHT
const [state, setState] = useState(0);
if (condition) {
  // Use state here
}
```

---

## State Issues

### State not updating

**Problem:** Mutating state directly instead of using setState

```jsx
// WRONG
this.state.count = 5;

// RIGHT
this.setState({ count: 5 });

// RIGHT (hooks)
setCount(5);
```

---

### Infinite re-renders

**Problem:** Missing useEffect dependency array or triggering state changes in render

```jsx
// WRONG - infinite loop
useEffect(() => {
  setCount(count + 1);
}); // No dependency array!

// RIGHT
useEffect(() => {
  // Code that doesn't trigger state changes
}, []); // Runs once
```

---

## Performance Issues

### App running slow

**Checklist:**
- [ ] Is console showing errors?
- [ ] Are you rendering huge lists without keys?
- [ ] Are you creating new objects/arrays in render?
- [ ] Use React DevTools to check what's re-rendering

**Tips:**
```jsx
// Use useMemo for expensive calculations
const result = useMemo(() => expensiveFunc(data), [data]);

// Use useCallback for stable function references
const handleClick = useCallback(() => {}, []);
```

---

## API/Fetching Issues

### Data not loading

**Checklist:**
- [ ] Is your API URL correct?
- [ ] Are you handling errors? (try/catch)
- [ ] Did you set up useEffect dependency array?
- [ ] Check Network tab in DevTools

```jsx
// Check browser DevTools Network tab
// Look for failed requests or wrong responses
```

---

### CORS Error

**Problem:** Browser blocks cross-origin requests

**Solutions:**
1. Use a CORS proxy (temporary):
```jsx
const url = `https://cors-anywhere.herokuapp.com/${apiUrl}`;
```

2. Ask backend to enable CORS

3. Use API that supports CORS

---

## Form Issues

### Form data not updating

**Problem:** Uncontrolled component

```jsx
// WRONG - input value not tied to state
<input onChange={(e) => {}} />

// RIGHT - controlled component
const [value, setValue] = useState("");
<input value={value} onChange={(e) => setValue(e.target.value)} />
```

---

### Form submitting and page reloading

**Problem:** Forgot preventDefault()

```jsx
const handleSubmit = (e) => {
  e.preventDefault(); // Add this!
  // Handle form submission
};
```

---

## Styling Issues

### CSS not applying

**Checklist:**
- [ ] Is the class name spelled correctly?
- [ ] Is the CSS file imported?
- [ ] Check if CSS is in global or component scope
- [ ] Try inline styles to test: `<div style={{ color: 'red' }}>`

```jsx
// RIGHT way to add class
<div className="my-class">Hello</div>

// NOT className="my-class" (like HTML)
```

---

## List Rendering Issues

### Warning about missing keys

**Problem:** Using array index as key

```jsx
// WRONG
{items.map((item, index) => <Item key={index} />)}

// RIGHT
{items.map((item) => <Item key={item.id} />)}
```

---

## Browser Issues

### Page stuck in loading

**Solution:**
1. Check if useEffect is fetching
2. Open DevTools Network tab
3. Is the API endpoint responding?
4. Try refreshing the page

---

## Debugging Steps

**When stuck, try:**

1. **Console Logging**
```jsx
useEffect(() => {
  console.log("State:", count);
  console.log("Props:", props);
}, [count, props]);
```

2. **React DevTools**
- Install browser extension
- Inspect components tree
- Check props and state values

3. **Network Tab**
- Check if API calls are working
- See response status (200, 404, 500, etc.)
- Look for response data

4. **Restart**
```bash
# Restart dev server
npm run dev
```

5. **Delete node_modules and reinstall**
```bash
rm -rf node_modules package-lock.json
npm install
```

---

## Getting Help

**When stuck, ask:**

1. **React Discord Community**
2. **Stack Overflow** - Tag: `reactjs`
3. **GitHub Issues** - If it's a library bug
4. **Reddit** - r/reactjs
5. **Local React Meetups**

**Include when asking:**
- Error message (full text)
- Minimal code example
- What you tried
- Browser/React version

---

*Remember: Every developer gets stuck. Asking for help is a strength!* 💪

---

*Last updated: June 2024*
