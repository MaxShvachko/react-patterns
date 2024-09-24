The Composite pattern is a structural design pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. In React, this pattern is useful for building components that can represent both individual elements and collections of elements. Here's an example of using the Composite pattern in React:

```jsx
import React from 'react';

// Component: Leaf (represents an individual element)
function MenuItem({ label }) {
  return <li>{label}</li>;
}

// Component: Composite (represents a collection of elements)
function Menu({ label, children }) {
  return (
    <div>
      <h3>{label}</h3>
      <ul>{children}</ul>
    </div>
  );
}

// App component that uses the Composite pattern
function App() {
  return (
    <div>
      <h1>Composite Pattern Example</h1>
      <Menu label="Main Menu">
        <MenuItem label="Home" />
        <MenuItem label="About" />
        <MenuItem label="Services" />
        <Menu label="Submenu">
          <MenuItem label="Submenu Item 1" />
          <MenuItem label="Submenu Item 2" />
        </Menu>
      </Menu>
    </div>
  );
}

export default App;
```

In this example:

- `MenuItem` represents an individual item in the menu. It's a leaf component as it doesn't have children.

- `Menu` represents a collection of items. It's a composite component because it can have child elements, including other `MenuItem` components and nested `Menu` components.

- The `App` component demonstrates the use of the Composite pattern. It creates a structured menu that can contain both individual items and submenus. This allows you to build complex tree structures in your application's UI.

The Composite pattern simplifies the client code by treating individual objects and compositions of objects uniformly. It's especially useful when you need to work with tree structures, such as menus, file systems, or nested components in your React application.