# JSX

## Table of Contents

1. [What is JSX?](#what-is-jsx)
2. [What is the point of JSX?](#what-is-the-point-of-jsx)
3. [JSX "Interpolation"](#jsx-interpolation)
4. [Including Components](#including-components)

## What is JSX?

JSX is syntactic sugar for defining tree structures or attributes in JavaScript.  Though it looks like HTML/XML, it is not.  Instead they are tokens that are meant to be used by various preprocessors (we use [Babel](https://babeljs.io/)) to transpile these tokens into standard ECMAScript.  It might seem a bit odd looking at first, with what appears to be HMTL or XML in the middle of JavaScript code.  For example:

```jsx
var movies =(
  <Movies>
    <StarWars>
      <MovieItem>A New Hope</MovieItem>
      <MovieItem>The Empire Strikes Back</MovieItem>
      <MovieItem>Return of the Jedi</MovieItem>
    </StarWars>
    <Matrix>
      <MovieItem>The Matrix</Matrix>
    <Matrix>
  </Movies>
);

render(movies);
```

## What is the point of JSX?

To help make our code clearer, cleaner, and more intuitive. It provides us with a shorthand for some boilerplate code that would otherwise be required.  It also makes HTML markup look like HTML. The following two pieces of code are equivalent:

A:
```jsx
ReactDOM.render(
    <div className="true-statements">I love Stroll!</div>,
    document.body
);
```

B:
```jsx
ReactDOM.render(
  React.createElement(
    'div',
    { className: 'true-statements' },
    'I love Stroll!'
  ),
  document.body
);
```

## JSX "Interpolation"

JSX supports interpolation-like syntax by wrapping JS code in curly braces `{ }`.  It is not a templating language, nor is it technically interpolation.  It's actually just more syntactic sugar for passing arguments to a function.  As such, within these braces there is no `if`/`else` statements, loops, or semicolons - though you can use simple ternary statements.  Everything within the braces must resolve to a single value.

How JSX transforms into JS:

```jsx
<div className={myClass} onClick={this.onClick}>
  {this.state.clickCount}
</div>
```

Translates into:
```javascript
React.createElement("div",
  {
    className: myClass,
    onClick: onClick
  },
  this.state.clickCount
)
```

Thus of we wrote: `className={myClass;}`.  It would transpile into: `{className: myClass;, onClick: onClick}`.  Can you spot the syntax error?

But what if we need to use multiline constructs when rendering components?  There are several strategies for accomplishing this.

### Do the claculations outside of JSX

```jsx
render: function () {
  var contents;

  if (this.state.sleep) {
    contents = 'zzzzzz'
  }

  return (
    <p>
      {contents}
    </p>
  );
}
```

### Use a ternary:

```jsx
<p>
  {this.state.sleep ? 'zzzzzzz' : ''}
</p>
```

### Call a function and interpolate its result:

```jsx
<ul>
  {items.map(function (item) {
    return (
      <li key={item.id}>
        {item.name}
      </li>
    );
  })}
</ul>
```

## Including Components

JSX is simply a syntax for expressing nested data structures.  It does not use *real* HTML elements, but keeps track of tree structures and their nodes properties.  As such we can use the following syntax.

```jsx
ReactDOM.render(
    <Widget />,
    document.body
);
```

`Widget` is not a valid HTML tag name.  Instead `<Widget>` is an instance of `Widget` that should be created and rendered with no properties or children.  This really just syntactic sugar for `React.createElement(Widget, {})`.

## Differences between JSX and HTML
