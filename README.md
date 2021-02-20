# React-Official

# Advanced Guides

## Programatically managing focus

to set focus in React, we can use `Refs` to Dom elements.
Using this, we first create a ref to an element in the JSX of a component class:

```js
class CustomText extends React.Component {
  constructor(props) {
    super(props);
    
    this.textInput = React.createRef();
  }
  
  render() {
    return (
      <input
        type="text"
        ref={this.textInput}
      />
    )
  }
}
```

Then we can focus it elsewhere in our component when needed:

```js
focus() {
  this.textInput.current.focus();
}
```

Sometimes a parent component needs to set focus to an element in a child component. We can do this by `exposing DOM refs to parent components` through a special prop on the child component that forwards the parent’s ref to the child’s DOM node.

```js
function CustomTextInput(props) {
  return (
    <input 
      type="text"
      ref={props.inputRef}
    />
  )
}

class Parent extends Component {
  constructor(props) {
    super(props);
    
    this.inputElement = React.createRef();
  }
  
  render() {
    return <CustomTextInput inputRef={this.inputElement} />
  }
}

// Now you can set focus when required
this.inputElement.current.focus();
```


## Mouse and pointer Events

Ensure that all functionality exposed through a mouse or pointer event can also be accessed using the keyboard alone. Depending only on the pointer device will lead to many cases where keyboard users cannot use your application.

To illustrate this, let’s look at a prolific example of broken accessibility caused by click events. This is the outside click pattern, where a user can disable an opened popover by clicking outside the element.

This is typically implemented by attaching a click event to the window object that closes the popover:

```js
class OuterClickExample extends React.Component {
  constructor(props) {
    super(props);
    
    this.state = {
      isOpen: false;
    }
    
    this.toggleContainer = React.createRef();
    
    this.onClickHandler = this.onClickHandler.bind(this);
    this.onClickOutsideHandler = this.onClickOutsideHandler.bind(this);
  }
  
  componentDidMount() {
    window.addEventListener('click', this.onClickOutsideHandler)
  }
  
  componentWillUnmount() {
    window.removeEventListener('click', this.onClickOutsideHandler)
  }
  
  
}
```
