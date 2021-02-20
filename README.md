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
