# Stroll React/JSX Style Guide

*A somewhat reasonable-ish approach to React and JSX*

## Table of Contents

  1. [Basic Rules](#basic-rules)
  2. [Naming](#naming)
  3. [Declaration](#declaration)
  4. [Alignment](#alignment)
  5. [Quotes](#quotes)
  6. [Spacing](#spacing)
  7. [Props](#props)
  8. [Parentheses](#parentheses)
  9. [Tag](#tags)
  10. [Methods](#methods)
  11. [Ordering](#ordering)
  12. [`isMounted`](#ismounted)
  13. [License](#license)

![alt text](http://imgs.xkcd.com/comics/code_quality.png "Why we care")

## Basic Rules

  - Only include one React component per file.
    - However, multiple [Stateless, or Pure, Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) are allowed per file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
  - Always use JSX syntax.
  - Do not use `React.createElement` unless you're initializing the app from a file that is not JSX.

**[⬆ back to top](#table-of-contents)**

## Naming

  - **Extensions**: Use `.jsx` extension for React components.
  - **Filename**: Use PascalCase for filenames. E.g., `ReservationCard.jsx`.
  - **Reference Naming**: Use PascalCase for React components. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

    ```jsx
    // bad
    var reservationCard = require('./ReservationCard');

    // good
    var ReservationCard = require('./ReservationCard');
    ```

    - **Component Naming**: Use the filename as the component name. For example, `ReservationCard.jsx` should have a reference name of `ReservationCard`. However, for root components of a directory, use `index.jsx` as the filename and use the directory name as the component name:

        ```jsx
        // bad
        var Footer = require('./Footer/Footer');

        // bad
        var Footer = require('./Footer/index');

        // good
        var Footer = require('./Footer');
        ```

**[⬆ back to top](#table-of-contents)**

## Declaration

  - Do not use `displayName` for naming components. Instead, name the component by reference.

    ```jsx
    // bad
    module.exports = React.createClass({
      displayName: 'ReservationCard',
      // stuff goes here
    });

    // good
    module.exports = ReservationCard;
    ```

**[⬆ back to top](#table-of-contents)**

## Alignment

  - Follow these alignment styles for JSX syntax. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

    ```jsx
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // if props fit in one line then keep it on the same line
    <Foo bar="bar" />

    // children get indented normally
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>
    ```

**[⬆ back to top](#table-of-contents)**

## Quotes

  - Always use double quotes (`"`) for JSX attributes. eslint: [`jsx-quotes`](http://eslint.org/docs/rules/jsx-quotes)

  > Why? JSX attributes [can't contain escaped quotes](http://eslint.org/docs/rules/jsx-quotes), so double quotes make conjunctions like `"don't"` easier to type.
  > Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.

    ```jsx
    // bad
    <Foo bar='bar' />

    // good
    <Foo bar="bar" />

    // bad
    <Foo style={{ left: "20px" }} />

    // good
    <Foo style={{ left: '20px' }} />
    ```

**[⬆ back to top](#table-of-contents)**

## Spacing

  - Always include a single space in your self-closing tag.

    ```jsx
    // bad
    <Foo/>

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

  - Do not pad JSX curly braces with spaces. eslint: [`react/jsx-curly-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)

    ```jsx
    // bad
    <Foo bar={ baz } />

    // good
    <Foo bar={baz} />
    ```

**[⬆ back to top](#table-of-contents)**

## Props

  - Always use camelCase for prop names.

    ```jsx
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```

  - Omit the value of the prop when it is explicitly `true`. eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

    ```jsx
    // bad
    <Foo
      hidden={true}
    />

    // good
    <Foo
      hidden
    />
    ```

  - Always include an `alt` prop on `<img>` tags. If the image is presentational, `alt` can be an empty string or the `<img>` must have `role="presentation"`. eslint: [`jsx-a11y/img-has-alt`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-has-alt.md)

    ```jsx
    // bad
    <img src="hello.jpg" />

    // good
    <img src="hello.jpg" alt="Me waving hello" />

    // good
    <img src="hello.jpg" alt="" />

    // good
    <img src="hello.jpg" role="presentation" />
    ```

  - Do not use words like "image", "photo", or "picture" in `<img>` `alt` props. eslint: [`jsx-a11y/img-redundant-alt`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-redundant-alt.md)

  > Why? Screenreaders already announce `img` elements as images, so there is no need to include this information in the alt text.

    ```jsx
    // bad
    <img src="hello.jpg" alt="Picture of me waving hello" />

    // good
    <img src="hello.jpg" alt="Me waving hello" />
    ```

  - Use only valid, non-abstract [ARIA roles](https://www.w3.org/TR/wai-aria/roles#role_definitions). eslint: [`jsx-a11y/aria-role`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/aria-role.md)

    ```jsx
    // bad - not an ARIA role
    <div role="datepicker" />

    // bad - abstract ARIA role
    <div role="range" />

    // good
    <div role="button" />
    ```

  - Do not use `accessKey` on elements. eslint: [`jsx-a11y/no-access-key`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/no-access-key.md)

  > Why? Inconsistencies between keyboard shortcuts and keyboard commands used by people using screenreaders and keyboards complicate accessibility.

  ```jsx
  // bad
  <div accessKey="h" />

  // good
  <div />
  ```

  - Avoid using an array index as `key` prop, prefer a unique ID. ([why?](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318))

  ```jsx
  // bad
  todos.map(function (todo, index) {
    return (
      <Todo
      {...todo}
      key={index}
      />
    );
  });

  // good
  todos.map(function (todo) {
    return (
      <Todo
      {...todo}
      key={todo.id}
      />
    );
  });
  ```

**[⬆ back to top](#table-of-contents)**

## Parentheses

  - Wrap JSX tags in parentheses when they span more than one line. eslint: [`react/wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/wrap-multilines.md)

    ```jsx
    // bad
    render() {
      return <MyComponent className="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    };

    // good
    render() {
      return (
        <MyComponent className="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    };

    // good, when single line
    render() {
      var body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    };
    ```


  - Always self-close tags that have no children. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

    ```jsx
    // bad
    <Foo className="stuff"></Foo>

    // good
    <Foo className="stuff" />
    ```

  - If your component has multi-line properties, close its tag on a new line. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

    ```jsx
    // bad
    <Foo
      bar="bar"
      baz="baz" />

    // good
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

**[⬆ back to top](#table-of-contents)**

## Methods

  - Bind event handlers for the render method in the constructor. eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

  > Why? A bind call in the render path creates a brand new function on every single render.

    ```jsx
    // bad
    var RadiologyDashboard = React.createClass({
      onClickDiv() {
        // do stuff
      },

      render() {
        return <div onClick={this.onClickDiv.bind(this)} />
      }
    });

    // good
  var RadiologyDashboard = React.createClass({
      constructor(props) {
        super(props);

        this.onClickDiv = this.onClickDiv.bind(this);
      },

      onClickDiv() {
        // do stuff
      },

      render() {
        return <div onClick={this.onClickDiv} />
      }
    });
    ```

  - Do not use underscore prefix for internal methods of a React component.

    ```jsx
    // bad
    React.createClass({
      _onClickSubmit() {
        // do stuff
      },

      // other stuff
    });

    // good
    React.createClass({
      onClickSubmit() {
        // do stuff
      }

      // other stuff
    });
    ```

  - Be sure to return a value in your `render` methods. eslint: [`require-render-return`](https://github.com/yannickcr/eslint-plugin-react/pull/502)

    ```jsx
    // bad
    render() {
      (<div />);
    }

    // good
    render() {
      return (<div />);
    }
    ```

**[⬆ back to top](#table-of-contents)**

## Ordering

  - Ordering for `React.createClass`: eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

    1. `displayName`
    1. `propTypes`
    1. `contextTypes`
    1. `childContextTypes`
    1. `mixins`
    1. `statics`
    1. `defaultProps`
    1. `getDefaultProps`
    1. `getInitialState`
    1. `getChildContext`
    1. `componentWillMount`
    1. `componentDidMount`
    1. `componentWillReceiveProps`
    1. `shouldComponentUpdate`
    1. `componentWillUpdate`
    1. `componentDidUpdate`
    1. `componentWillUnmount`
    1. *clickHandlers or eventHandlers* like `onClickSubmit()` or `onChangeDescription()`
    1. *getter methods for `render`* like `getSelectReason()` or `getFooterContent()`
    1. *Optional render methods* like `renderNavigation()` or `renderProfilePicture()`
    1. `render`

**[⬆ back to top](#table-of-contents)**

## `isMounted`

  - Do not use `isMounted`. eslint: [`react/no-is-mounted`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-is-mounted.md)

  > Why? [`isMounted` is an anti-pattern][anti-pattern], is not available when using ES6 classes, and is on its way to being officially deprecated.

  [anti-pattern]: https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html

**[⬆ back to top](#table-of-contents)**

## License

(The MIT License)

Copyright (c) 2016 Stroll

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**
