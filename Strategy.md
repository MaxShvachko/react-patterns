Strategy is a behavioral design pattern that lets you define a family of algorithms, put each of them into a separate class, or function.

This is an example of using the Strategy pattern in React with TypeScript using function components and hooks:

```tsx
import React, { useState } from 'react';

// Define the strategy type
type SortingStrategy = (items: string[]) => string[];

// Concrete strategy implementations

const ascendingSortingStrategy: SortingStrategy = (items) => items.slice().sort();

const descendingSortingStrategy: SortingStrategy = (items) =>
  items.slice().sort((a, b) => b.localeCompare(a));

// SortableList component using the selected strategy

interface SortableListProps {
  strategy: SortingStrategy;
}

const SortableList: React.FC<SortableListProps> = ({ strategy }) => {
  const [items, setItems] = useState<string[]>(['Apple', 'Banana', 'Orange', 'Mango']);

  const handleSort = () => {
    const sortedItems = strategy(items);
    setItems(sortedItems);
  };

  return (
    <div>
      <h2>Sortable List</h2>
      <ul>
        {items.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
      <button onClick={handleSort}>Sort</button>
    </div>
  );
};

// Example usage in App component

const App: React.FC = () => {
  return (
    <div>
      <SortableList strategy={ascendingSortingStrategy} />
      <hr />
      <SortableList strategy={descendingSortingStrategy} />
    </div>
  );
};

export default App;
```

In this example:

- The `SortingStrategy` type represents the strategy function signature, taking an array of strings and returning a sorted array of strings.
- The `ascendingSortingStrategy` and `descendingSortingStrategy` are functions implementing the sorting logic without using classes.
- The `SortableList` component is the context that uses the selected sorting strategy, similar to the previous example.