# Passing Data in React Router Without Showing in URL

React Router (v6+) provides two powerful methods for passing **temporary, hidden data** between routes:

- `navigate(..., { state })` – programmatic navigation
- `<Link state={...}>` – declarative navigation

This data is **not visible in the URL**, making it ideal for temporary UI logic or private values.

---

## 1. Using `navigate()` (Programmatic Navigation)

```jsx
import { useNavigate } from 'react-router-dom';

const Login = () => {
  const navigate = useNavigate();

  const handleLogin = () => {
    // After login, pass user data without exposing it in the URL
    navigate('/dashboard', {
      state: {
        userId: 101,
        username: 'manu'
      }
    });
  };

  return <button onClick={handleLogin}>Login</button>;
};
```

> Use this when navigating after an event, logic, or form submission.

---

## 2. Using `<Link>` (Declarative Navigation)

```jsx
import { Link } from 'react-router-dom';

const UserList = () => {
  const user = { id: 5, name: 'Manu' };

  return (
    <Link to="/user-details" state={user}>
      View Profile
    </Link>
  );
};
```

> Use this in UI elements like cards, menus, or lists.

---

## Receiving the Data

In the destination component, use `useLocation` to access the passed state:

```jsx
import { useLocation } from 'react-router-dom';

const UserDetails = () => {
  const location = useLocation();
  const { id, name } = location.state || {};

  return (
    <div>
      <h2>{name}</h2>
      <p>ID: {id}</p>
    </div>
  );
};
```

---

## More Examples

### With Form Submission and Redirect:

```jsx
const FormPage = () => {
  const navigate = useNavigate();

  const handleSubmit = (e) => {
    e.preventDefault();
    navigate('/success', {
      state: { message: 'Form submitted successfully!' }
    });
  };

  return <form onSubmit={handleSubmit}>...</form>;
};
```

---

### With Dynamic List of Users:

```jsx
const users = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
];

return (
  <div>
    {users.map(user => (
      <Link
        key={user.id}
        to="/user"
        state={{ user }}
      >
        <p>{user.name}</p>
      </Link>
    ))}
  </div>
);
```

---

## Which One Should You Use?

| Use Case                          | Best Option             | Why?                                       |
|----------------------------------|--------------------------|--------------------------------------------|
| After button clicks or logic     | `navigate(..., { state })` | Gives full control in JS logic             |
| Simple UI link (e.g., card/menu) | `<Link state={...}>`       | Cleaner, declarative in JSX                |
| Form submission or redirect      | `navigate()`              | Works after validation/submission          |
| Dynamic item rendering           | `<Link>` inside `.map()`  | Easily passes data from list items         |

---

## Limitations

- Data passed via `state` is:
  - Hidden from URL
  - **Not persistent** after refresh
  - Lost on full page reload

For persistent data, use:
- `Context API`
- `Redux`
- `localStorage` / `sessionStorage`

---

## Summary

- Use `navigate(..., { state })` for **event-based navigation**.
- Use `<Link state={...}>` for **UI-driven navigation**.
- Both are great for **temporary, hidden data passing** between routes.
- Handle fallback values using `location.state || {}` to prevent crashes.

---

