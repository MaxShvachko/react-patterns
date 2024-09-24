The Command Pattern is a behavioral design pattern that turns a request into a stand-alone object containing all information about the request. This object can be passed as a parameter, stored, or manipulated.

Here's a simple example of using the Command Pattern in a React component:

```jsx
import React, { useState } from 'react';

// Command Interface
interface Command {
  execute(): void;
}

// Concrete Command
class ToggleCommand implements Command {
  private setState: React.Dispatch<React.SetStateAction<boolean>>;

  constructor(setState: React.Dispatch<React.SetStateAction<boolean>>) {
    this.setState = setState;
  }

  execute(): void {
    this.setState((prev) => !prev);
  }
}

// Invoker
const ToggleButton: React.FC<{ command: Command }> = ({ command }) => (
  <button onClick={() => command.execute()}>Toggle State</button>
);

// Receiver
const ToggleComponent: React.FC = () => {
  const [state, setState] = useState(false);

  const toggleCommand = new ToggleCommand(setState);

  return (
    <div>
      <ToggleButton command={toggleCommand} />
      <p>Current State: {state ? 'On' : 'Off'}</p>
    </div>
  );
};

// Example Usage
const App: React.FC = () => {
  return (
    <div>
      <h1>Command Pattern Example</h1>
      <ToggleComponent />
    </div>
  );
};

export default App;
```

In this example:

- `Command` is the interface that declares the `execute` method.
- `ToggleCommand` is a concrete command that toggles a boolean state in the `ToggleComponent`.
- `ToggleButton` is the invoker that triggers the execution of the command.
- `ToggleComponent` is the receiver that holds the state and defines the operation to be performed.

This is a simplified example, and in a real-world scenario, you might have more complex commands and receivers. The Command Pattern becomes especially useful when you want to decouple the sender and receiver of a request.