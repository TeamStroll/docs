# React

## What is React?

React is a JS library for creating UI components, that are fast and reactive to the changes in the data.  It has spawned an ecosystem of supporting libraries that build upon this initial premise.

## Why React?

React simplifies the handling UI updates in response to data changes, removing the need to manually update elements in response to user input - or async data flows.  When the state or data changes - React rerenders *all* the elements.  It's use of the virtual DOM allows React to change only the elements that require changing, not the entire DOM.  It does this through effectively diffing the virtual DOM where the changes have occurred and the actual DOM to determine the minimum changes necessary to update the DOM to reflect the virtual DOM.

## The Offical Docs

The [offical documenation](https://facebook.github.io/react/docs/getting-started.html) on the Facebook github is a great place to start learning react. The [tutorial](https://facebook.github.io/react/docs/tutorial.html) provided is particularly good.

## Architecture of a React Webapp

React apps can be decomposed into constituent components. The use of components allows for greater maintainability, reuse, and ease of testing.  Indeed when making a React component, it should be tailored to be reuseable.  Most components should also be 'dumb', listening for props to be passed to it and rerendering based upon these props (though there are times when a lower level component might want to track parts of its own state - for example when a dropdown menu is open/closed).  We typically write our react component renders in [JSX](./jsx.md).

An example component:

```jsx
var ClickCounter = React.createClass({

  getInitialState: function () {
    return ({
      clickCount: 0
    });
  },

  click: function (e) {
    e.preventDefault();
    this.setState({
      clickCount: this.state.clickCount + 1
    });
  },

  render: function () {
    return (
      <div>
        <div>
          {this.state.clickCount}
        </div>
        <div
          onClick={this.click}
        >
          Click Me!
        </div>
      </div>
    );
  }
});
```
