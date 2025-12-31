# REACT FORMAL SPECIFICATION 

## 12 PRIMARY REACT KEYWORDS

### 1. **COMPONENT** - React Components
```jsx
// Functional component
function UserCard({ name, email }) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>{email}</p>
    </div>
  );
}

// Component with TypeScript
interface UserProps {
  name: string;
  email: string;
}

function UserCard({ name, email }: UserProps) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>{email}</p>
    </div>
  );
}
```

### 2. **STATE** - State Management (useState)
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  
  const increment = () => setCount(count + 1);
  const updateName = (e) => setName(e.target.value);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
      <input value={name} onChange={updateName} />
    </div>
  );
}
```

### 3. **EFFECT** - Side Effects (useEffect)
```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    const fetchUser = async () => {
      try {
        const response = await fetch(`/api/users/${userId}`);
        const data = await response.json();
        setUser(data);
      } finally {
        setLoading(false);
      }
    };
    
    fetchUser();
  }, [userId]); // Dependency array
  
  if (loading) return <p>Loading...</p>;
  return <div>{user?.name}</div>;
}
```

### 4. **CONTEXT** - Context API
```jsx
const UserContext = createContext();

function UserProvider({ children }) {
  const [user, setUser] = useState(null);
  
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}

function useUser() {
  const context = useContext(UserContext);
  if (!context) {
    throw new Error('useUser must be used within UserProvider');
  }
  return context;
}
```

### 5. **REDUCER** - useReducer for Complex State
```jsx
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
    </div>
  );
}
```

### 6. **HOOK** - Custom Hooks
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(data => { setData(data); setLoading(false); })
      .catch(err => { setError(err); setLoading(false); });
  }, [url]);
  
  return { data, loading, error };
}

// Usage
function App() {
  const { data: users, loading } = useFetch('/api/users');
  return loading ? <p>Loading...</p> : <UserList users={users} />;
}
```

### 7. **PROPS** - Props Handling & Validation
```jsx
function UserList({ users, onUserSelect }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id} onClick={() => onUserSelect(user)}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}

// PropTypes validation
UserList.propTypes = {
  users: PropTypes.arrayOf(
    PropTypes.shape({
      id: PropTypes.number.isRequired,
      name: PropTypes.string.isRequired
    })
  ).isRequired,
  onUserSelect: PropTypes.func.isRequired
};

// Default props
UserList.defaultProps = {
  users: []
};
```

### 8. **FORM** - Form Handling
```jsx
function UserForm({ onSubmit }) {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    age: ''
  });
  const [errors, setErrors] = useState({});
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };
  
  const validate = () => {
    const newErrors = {};
    if (!formData.name) newErrors.name = 'Name required';
    if (!formData.email) newErrors.email = 'Email required';
    return newErrors;
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    const newErrors = validate();
    if (Object.keys(newErrors).length === 0) {
      onSubmit(formData);
    } else {
      setErrors(newErrors);
    }
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        name="name"
        value={formData.name}
        onChange={handleChange}
        placeholder="Name"
      />
      {errors.name && <span>{errors.name}</span>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 9. **LIST** - List & Key Rendering
```jsx
function UserList({ users, onDelete }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          <span>{user.name}</span>
          <button onClick={() => onDelete(user.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}

// Rules: Always use key prop, don't use index as key
```

### 10. **MEMO** - Performance Optimization
```jsx
// Memoized component
const UserCard = React.memo(({ user, onSelect }) => {
  return (
    <div onClick={() => onSelect(user)}>
      {user.name}
    </div>
  );
});

// useCallback for memoized functions
function UserList({ users }) {
  const [selectedId, setSelectedId] = useState(null);
  
  const handleSelect = useCallback(user => {
    setSelectedId(user.id);
  }, []);
  
  return (
    <ul>
      {users.map(user => (
        <UserCard
          key={user.id}
          user={user}
          onSelect={handleSelect}
        />
      ))}
    </ul>
  );
}
```

### 11. **ROUTER** - React Router Navigation
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/users">Users</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<UserList />} />
        <Route path="/users/:id" element={<UserDetail />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### 12. **TESTING** - Component Testing
```jsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

describe('UserCard', () => {
  it('renders user information', () => {
    render(<UserCard name="John" email="john@example.com" />);
    expect(screen.getByText('John')).toBeInTheDocument();
  });
  
  it('calls onClick when clicked', async () => {
    const handleClick = jest.fn();
    render(<UserCard {...props} onClick={handleClick} />);
    await userEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalled();
  });
});
```

## BEST PRACTICES
1. Use functional components
2. Lift state up when needed
3. Memoize expensive components
4. Use useCallback for callbacks
5. Implement error boundaries
6. Code split with lazy loading
7. Test components thoroughly
8. Use proper key props
9. Avoid inline object props
10. Monitor performance with React DevTools

