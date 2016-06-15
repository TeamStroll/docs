# React

## What is React?

React is a JS library for creating UI components, that are fast and reactive to the changes in the data.  It has spawned an ecosystem of supporting libraries that build upon this initial premise.

## Why React?

React simplifies the handling UI updates in response to data changes, removing the need to manually update elements in response to user input - or async data flows.  When the state or data changes - React rerenders *all* the elements.  It's use of the virtual DOM allows React to change only the elements that require changing, not the entire DOM.  It does this through effectively diffing the virtual DOM where the changes have occurred and the actual DOM to determine the minimum changes necessary to update the DOM to reflect the virtual DOM.

## The Offical Docs

![alt text](http://imgs.xkcd.com/comics/like_im_five.png "So easy...")

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

## Component Lifecycle Methods

Sometimes you want to update a component based on user interaction or receiving new data from the server.  For this you use component lifecycle methods.  I would write more here but [the Facebook documentation](https://facebook.github.io/react/docs/component-specs.html#lifecycle-methods) in this is very good.

## Listwise Diffing and Keys

To reconcile children, React takes a naive approach.   It goes over the two lists of children at the same time and generates a mutation when there's a difference.  This works well when adding an element to the end of a list, but inserting at the beginning of a list is more problematic - as it will see the nodes as different will mutate all nodes with similar elements, eg. `span`s.

There are many algorithms that attempt to find the minimum sets of operations to transform a list of elements. [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) can find the minimum using single element insertion, deletion and substitution in O(n<sup>2</sup>). Even if we were to use Levenshtein, this doesn't find when a node has moved into another position and algorithms to do that have much worse complexity.

```jsx
renderA: <div><span key="first">first</span></div>
renderB: <div><span key="second">second</span><span key="first">first</span></div>
=> [insertNode <span>second</span>]
```

Thus, React uses keys.  This allows React to find insertion, deletion, substitutions, and moves in O(n) time! - via a hash table.  Most of the time, the element you are using already has a unique id.  This key only has to be unique among its siblings - not globally.

More info at the [React Docs](https://facebook.github.io/react/docs/reconciliation.html#list-wise-diff).

## Input Sanitization

In React, except for two cases React will sanitize the innerHTML of inputs for you.

- CSS styles - are not sanitized which is known IE8 won't fix issue.
- You use `dangerouslySetInnerHTML` - which removes this sanitization step.

## More Resources

- [React.js Tutorial Guide Gotchas](https://zapier.com/engineering/react-js-tutorial-guide-gotchas/)
