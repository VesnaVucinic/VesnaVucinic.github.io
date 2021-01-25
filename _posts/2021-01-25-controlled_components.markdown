---
layout: post
title:      "Controlled Components"
date:       2021-01-25 13:34:46 +0000
permalink:  controlled_components
---


The React docs state:

*In most cases, we recommend using controlled components to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.*

Controled component has an input element that has a value attribute bound to state and an event handler to update that state.

With every single key press in input, the value in state is changed - updated. When changes in the input are made, the event handler calls setState() and updates the state. That causes the component to re-render and value of updated satate is displayed in the element. Flow of data is uni-directional, from state to input and the state serves as “the single source of truth” .

Example of controled component is:

```
import React from 'react';
 
class Form extends React.Component {
  state = {
    firstName: "John",
    lastName: "Henry"
  }
 
handleChange = event => {
  this.setState({
    [event.target.name]: event.target.value
  })
}
 
  render() {
    return (
      <form>
        <input type="text" onChange={event => this.handleChange(event)} value={this.state.firstName} />
        <input type="text" onChange={event => this.handleChange(event)} value={this.state.lastName} />
      </form>
    )
  }
}
 
export default Form;
```







