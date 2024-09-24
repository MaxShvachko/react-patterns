The Mediator pattern is used to centralize communication between multiple components. It promotes loose coupling by having components communicate through a mediator rather than directly with each other. Here's a simple example in React:

```tsx
import React, { createContext, useContext, useState, ReactNode } from 'react';

// Mediator Context
interface MediatorContextProps {
  state: Record<string, string>;
  notify: (id: string, message: string) => void;
}

const MediatorContext = createContext<MediatorContextProps | undefined>(undefined);

// Mediator Provider
interface MediatorProviderProps {
  children: ReactNode;
}

const MediatorProvider: React.FC<MediatorProviderProps> = ({ children }) => {
  const [state, setState] = useState<Record<string, string>>({});

  const notify = (id: string, message: string) => {
    setState((prevState) => ({ ...prevState, [id]: message }));
  };

  return (
    <MediatorContext.Provider value={{ state, notify }}>
      {children}
    </MediatorContext.Provider>
  );
};

// Mediated Component
interface ComponentAProps {
  id: string;
}

const ComponentA: React.FC<ComponentAProps> = ({ id }) => {
  const { notify } = useContext(MediatorContext)!;

  const handleClick = () => {
    notify(id, 'Hello from Component A!');
  };

  return (
    <div>
      <h2>Component A</h2>
      <button onClick={handleClick}>Send Message</button>
    </div>
  );
};

// Mediated Component
interface ComponentBProps {
  id: string;
}

const ComponentB: React.FC<ComponentBProps> = ({ id }) => {
  const { state } = useContext(MediatorContext)!;

  return (
    <div>
      <h2>Component B</h2>
      <p>Received Message: {state[id]}</p>
    </div>
  );
};

// Parent Component
const MediatorExample: React.FC = () => {
  return (
    <MediatorProvider>
      <div>
        <ComponentA id="A" />
        <ComponentB id="A" />
      </div>
      <div>
        <ComponentA id="B" />
        <ComponentB id="B" />
      </div>
    </MediatorProvider>
  );
};

export default MediatorExample;
```

In this example:

- `MediatorProvider` provides a context for communication.
- `ComponentA` and `ComponentB` can communicate through the mediator (`MediatorContext`).
- `ComponentA` notifies the mediator when a button is clicked.
- `ComponentB` can access the shared state from the mediator.

This pattern becomes more useful as the number of components and complexity of communication increases, as it helps manage interactions more effectively.