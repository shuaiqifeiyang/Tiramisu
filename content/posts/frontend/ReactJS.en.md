---
title: "ReactJS"
date: 2020-01-03T22:28:15-08:00
draft: false
tags: [React]
---
Notes of ReactJS document
`<!--more-->`

## 2. JSX

* Embedding Expressions in JSX using curly braces

  ```jsx
  const name = 'Josh Perez';
  const element = <h1>Hello, {name}</h1>;
  ```
* We split JSX over multiple lines for readability. While it isn’t required, when doing this, we also recommend wrapping it in parentheses to avoid the pitfalls of [automatic semicolon insertion](https://stackoverflow.com/q/2846283).
* JSX is an expression too
* Specifying Attributes with JSX

  ```jsx
  const element = <div tabIndex="0"></div>;
  const element = <img src={user.avatarUrl}></img>;
  ```
* Empty tag ends in `/>`

  ```jsx
  const element = <img src={user.avatarUrl} />;
  ```
* JSX Prevents Injection Attacks: Everything is converted to a string before being rendered.
* JSX represents objects.

## 3. Rendering Elements

* Elements are the smallest building blocks of React apps.

## 4. Components and Props

* Always start component names with a capital letter.
* All React components must act like pure functions with respect to their props.

## 5. State and Lifecycle

* There things about `setState()`

  * Do not modify state directly
  * State updates may be asynchronous

    * use function to update state that relies on previous state

    ```jsx
    this.setState((state, props) => ({
      counter: state.counter + props.increment
    }));
    ```
  * State updated are merged

## 6. Handling Events

* camelCase
* pass a function as the event handler

```jsx
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

* call `preventDefault` explicitly to prevent default behavior
* Three ways to handle this in React

  * use bind in constructor

  ```jsx
  constructor(props) {
      super(props);
      this.state = {isToggleOn: true};

      // This binding is necessary to make `this` work in the callback
      this.handleClick = this.handleClick.bind(this);
    }
  ```

  * use array function

  ```jsx
    handleClick = () => {
      console.log('this is:', this);
    }
  ```

  * use array function in the callback. The potential drawback is `if this callback is passed as a prop to lower components, those components might do an extra re-rendering.`

  ```jsx
    render() {
      // This syntax ensures `this` is bound within handleClick
      return (
        <button onClick={() => this.handleClick()}>
          Click me
        </button>
      );
    }
  ```

## 7. Conditional Rendering

* Element Variables
* Inline If with logical && operator

  ```jsx
  {unreadMessages.length > 0 &&
    <h2>
      You have {unreadMessages.length} unread messages.
    </h2>
  }
  ```
* Inline if-else with conditional operator

  ```jsx
  {isLoggedIn
    ? <LogoutButton onClick={this.handleLogoutClick} />
    : <LoginButton onClick={this.handleLoginClick} />
  }
  ```
* Preventing component from rendering: return null

## 8. Lists and Keys

* Rendering multiple components

  ```jsx
  const numbers = [1, 2, 3, 4, 5];
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  ```
* Basic list components

  ```C++
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <li key={number.toString()}>
        {number}
      </li>
    );
    return (
      <ul>{listItems}</ul>
    );
  }
  ```
* We don’t recommend using indexes for keys if the order of items may change.
* if you [extract](https://reactjs.org/docs/components-and-props.html#extracting-components) a `ListItem` component, you should keep the key on the `<ListItem />` elements in the array rather than on the `<li>` element in the `ListItem` itself.

  ```jsx
  function ListItem(props) {
    // Correct! There is no need to specify the key here:
    return <li>{props.value}</li>;
  }

  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      // Correct! Key should be specified inside the array.
      <ListItem key={number.toString()} value={number} />
    );
    return (
      <ul>
        {listItems}
      </ul>
    );
  }
  ```
* Keys must only be unique among siblings

## 9. Forms

* Input something

  ```jsx
  class NameForm extends React.Component {
    constructor(props) {
      super(props);
      this.state = {value: ''};

      this.handleChange = this.handleChange.bind(this);
      this.handleSubmit = this.handleSubmit.bind(this);
    }

    handleChange(event) {
      this.setState({value: event.target.value});
    }

    handleSubmit(event) {
      alert('A name was submitted: ' + this.state.value);
      event.preventDefault();
    }

    render() {
      return (
        <form onSubmit={this.handleSubmit}>
          <label>
            Name:
            <input type="text" value={this.state.value} onChange={this.handleChange} />
          </label>
          <input type="submit" value="Submit" />
        </form>
      );
    }
  }
  ```
