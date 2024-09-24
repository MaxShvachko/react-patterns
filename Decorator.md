The Decorator pattern is a structural design pattern that allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class. In React, it can be implemented using `Higher Order Components (HOCs)` to add additional features or behaviors to components. Here's an example of using the Decorator pattern in React:

```jsx
import React from 'react';

// Original Component
function BasicComponent({ text }) {
  return <div>{text}</div>;
}

// Decorator Component: Adds extra functionality (e.g., a border)
function withBorder(Component) {
  return function WithBorder({ ...props }) {
    return <div style={{ border: '2px solid black' }}><Component {...props} /></div>;
  };
}

// Decorator Component: Adds extra functionality (e.g., background color)
function withBackgroundColor(Component) {
  return function WithBackgroundColor({ ...props }) {
    return <div style={{ backgroundColor: 'lightgray' }}><Component {...props} /></div>;
  };
}

// Applying decorators to the original component
const ComponentWithBorder = withBorder(BasicComponent);
const ComponentWithBackgroundColor = withBackgroundColor(BasicComponent);

// App component that uses decorated components
function App() {
  return (
    <div>
      <h1>Decorator Pattern Example</h1>
      <BasicComponent text="Basic Component" />
      <ComponentWithBorder text="Component with Border" />
      <ComponentWithBackgroundColor text="Component with Background" />
    </div>
  );
}

export default App;
```

In this example:

- `BasicComponent` is the original component that you want to enhance with decorators.

- `withBorder` and `withBackgroundColor` are decorator functions that take a component as input and return a new component with additional styles.

- We create new components like `ComponentWithBorder` and `ComponentWithBackgroundColor` by applying the decorator functions to the `BasicComponent`.

- The `App` component demonstrates how you can use the decorated components in your application. It includes the original `BasicComponent` and two decorated components, each with different styles.

#### The implementation with React Hook API.

### Breakdown:

1. **BasicComponent:**
   - A simple, stateless React component that receives a `text` prop and renders it inside a `<div>`.
   ```jsx
   function BasicComponent({ text }) {
     return <div>{text}</div>;
   }
   ```

2. **BasicStoreComponent:**
   - This is a **decorator component**. It enhances the original `BasicComponent` by adding additional functionality (in this case, text retrieved from a store).
   - It uses a hook `useTextStore()` (not defined here) to fetch the `text` value from a store or a context, then passes this text as a prop to the `BasicComponent`.
   - The decorator pattern allows you to wrap the original component (`BasicComponent`) with extra behavior without altering the original component's logic.
   ```jsx
   function BasicStoreComponent({ ...props }) {
     const text = useTextStore();

     return <BasicComponent { ...props } text={text} />;
   }
   ```

3. **App Component:**
   - The `App` component demonstrates how to use both the original `BasicComponent` and the enhanced `BasicStoreComponent`.
   - It renders:
     - A regular `BasicComponent` with hardcoded text `"Basic Component"`.
     - A `BasicStoreComponent`, which dynamically gets the `text` from a store using the `useTextStore` hook and passes it to `BasicComponent`.
   ```jsx
   function App() {
     return (
       <div>
         <h1>Decorator Pattern Example</h1>
         <BasicComponent text="Basic Component" />
         <BasicStoreComponent />
       </div>
     );
   }
   ```

### Key Points:
- **BasicComponent** is the original component, which receives `text` as a prop.
- **BasicStoreComponent** is a wrapper (decorator) that retrieves additional information (`text`) and passes it to `BasicComponent`.

---

The Decorator pattern allows you to add features or behavior to components in a flexible and reusable way without modifying their source code. This can be especially useful in situations where you want to apply enhancements or modifications to components while keeping their core functionality intact.