# Throttling and Debouncing in JavaScript

Throttling and Debouncing are two key performance optimization techniques used in JavaScript to control how often a function is executed, especially for events that trigger rapidly (like scroll, resize, keypress, or input).

## 1. Debouncing

### Concept

Wait for a pause in the input before running the function.

### How it works

- The function is delayed until after a certain period of inactivity.
- If the event keeps firing, the timer resets.

### Example Use Case

Search input: Wait until the user stops typing to trigger the API call.

### Code Example

```javascript
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

const handleSearch = debounce((query) => {
  console.log("Searching for:", query);
}, 300);

document.getElementById("search").addEventListener("input", (e) => {
  handleSearch(e.target.value);
});
```

**Note**: Only fires after the user has stopped typing for 300ms.

## 2. Throttling

### Concept

Allow the function to run only once every X milliseconds, no matter how many times the event fires.

### How it works

Function runs once and then waits for the cooldown before it can run again.

### Example Use Case

Scroll events: Only update something every 200ms while scrolling.

### Code Example

```javascript
function throttle(fn, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}

const handleScroll = throttle(() => {
  console.log("Scroll event fired!");
}, 200);

window.addEventListener("scroll", handleScroll);
```

**Note**: Even if user scrolls continuously, `handleScroll` fires only once every 200ms.

## Summary Table

| Feature | Debouncing | Throttling |
| --- | --- | --- |
| **Definition** | Delay execution until input stops | Execute at most once per time interval |
| **Use Case** | Search input, validation | Scroll, resize, drag events |
| **Behavior** | Runs after delay | Runs at regular intervals |
| **Example** | API call after typing stops | Event handler while scrolling |

## Which to Use When?

| Scenario | Use |
| --- | --- |
| Search/autocomplete | Debounce |
| Resize/scroll events | Throttle |
| Button spam clicks | Throttle or Debounce |

# Debouncing and Throttling in React with Custom Hooks

Reusable, clean, and optimized custom hooks for debouncing and throttling in React.

## useDebounce Hook

### Use Case
Wait for the user to stop typing before triggering an API call.

### Code
```tsx
import { useEffect, useState } from "react";

export function useDebounce<T>(value: T, delay: number): T {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => setDebouncedValue(value), delay);

    return () => clearTimeout(timer); // Cleanup on value or delay change
  }, [value, delay]);

  return debouncedValue;
}
```

### How to Use It
```tsx
import React, { useState } from "react";
import { useDebounce } from "./useDebounce";

function SearchInput() {
  const [search, setSearch] = useState("");
  const debouncedSearch = useDebounce(search, 500); // Wait 500ms

  useEffect(() => {
    if (debouncedSearch) {
      // Call your API here
      console.log("Searching for:", debouncedSearch);
    }
  }, [debouncedSearch]);

  return <input value={search} onChange={(e) => setSearch(e.target.value)} />;
}
```

## useThrottle Hook

### Use Case
Run a function at most once every X milliseconds (e.g., on scroll).

### Code
```tsx
import { useEffect, useRef, useState } from "react";

export function useThrottle<T>(value: T, limit: number): T {
  const [throttledValue, setThrottledValue] = useState(value);
  const lastRan = useRef(Date.now());

  useEffect(() => {
    const handler = setTimeout(() => {
      if (Date.now() - lastRan.current >= limit) {
        setThrottledValue(value);
        lastRan.current = Date.now();
      }
    }, limit - (Date.now() - lastRan.current));

    return () => clearTimeout(handler);
  }, [value, limit]);

  return throttledValue;
}
```

### How to Use It
```tsx
import React, { useState, useEffect } from "react";
import { useThrottle } from "./useThrottle";

function ScrollTracker() {
  const [scrollY, setScrollY] = useState(window.scrollY);
  const throttledScrollY = useThrottle(scrollY, 200); // Throttle to every 200ms

  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    window.addEventListener("scroll", handleScroll);
    return () => window.removeEventListener("scroll", handleScroll);
  }, []);

  useEffect(() => {
    console.log("Throttled scroll position:", throttledScrollY);
  }, [throttledScrollY]);

  return <div>Scroll Y: {throttledScrollY}</div>;
}
```

## Summary

| Hook | Use When |
| --- | --- |
| `useDebounce` | Wait for user to pause input |
| `useThrottle` | Limit function to run every X ms |
