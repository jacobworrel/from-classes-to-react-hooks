# from-classes-to-react-hooks
A guide to help migrate from ES6 class components to the [React Hooks API](https://reactjs.org/docs/hooks-intro.html).

## State

##### Classes
```javascript
import React from 'react';

class Counter extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      count: 0
    };

    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
  }

  increment() {
    this.setState(prevState => ({ count: (prevState.count += 1) }));
  }

  decrement() {
    this.setState(prevState => ({ count: (prevState.count -= 1) }));
  }

  render() {
    return (
      <div>
        <div>{this.state.count}</div>
        <button onClick={this.increment}>Increment</button>
        <button onClick={this.decrement}>Decrement</button>
      </div>
    );
  }
}
```
[![Edit class-state](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/determined-wiles-1ch81?fontsize=14)

##### React Hooks
```javascript
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <div>{count}</div>
      <button onClick={() => setCount(count => count + 1)}>Increment</button>
      <button onClick={() => setCount(count => count - 1)}>Decrement</button>
    </div>
  );
};
```
[![Edit class-state](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/determined-wiles-1ch81?fontsize=14)

## Event Handlers

##### Classes
```javascript
import React from "react";

class Clicker extends React.Component {
  constructor(props) {
    super(props);

    this.handleClick = this.handleClick.bind(this);
  }

  handleClick(event) {
    alert(`You just clicked ${this.props.id}`);
    event.stopPropagation();
  }

  render() {
    return <div onClick={this.handleClick}>Click me!</div>;
  }
}
```
[![Edit competent-minsky-48s98](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/competent-minsky-48s98?fontsize=14)

##### React Hooks
```javascript
import React, { useCallback } from 'react';

const Clicker = ({ id }) => (
  <div onClick={useCallback(
    (event) => {
      alert(`You just clicked ${id}`);
      event.stopPropagation();
    },
    [id]
  )}>
    Click me!
  </div>
);
```
[![Edit react-windowed-select](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/r4vx9oxmkq)