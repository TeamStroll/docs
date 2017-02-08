# Sass Tips and Tricks

## Table of Contents
- [Variable Naming](#variable-naming)
- [Placeholders](#placeholders)
- [The &](#ampersand)
- [Inline svg](#inline-svg)
- [Sass Tutorials](#sass-tutorials)

## Variable Naming
  
  Variable names shouldn't be vague and should follow the style guide.  For Example:
  
 ```css
  $orange: #ffa600; 
  $grey: #f3f3f3; 
  $blue: #82d2e5;

  $link-primary: $orange;
  $link-secondary: $blue;
  $link-tertiary: $grey;

  $radius-button: 5px;
  $radius-tab: 5px;
```


**[⬆ back to top](#table-of-contents)**

## Placeholders

  Placeholders can be extremely effective at writting DRY Sass and make enforcing style across the site significantly easier.  An example with placeholders:
  
 ```css
  %bg-image {
    width: 100%;
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
  }

  .image-one {
    @extend %bg-image;
    background-image:url(/img/image-one.jpg");
  }

  .image-two {
    @extend %bg-image;
    background-image:url(/img/image-two.jpg");
  }
```

  The resulting CSS:
```css
  .image-one, .image-two {
    width: 100%;
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
  }

  .image-one {
    background-image:url(/img/image-one.jpg");
  }

  .image-two {
    background-image:url(/img/image-two.jpg");
  }
```
  As we can see, the written Sass is significantly reduced and more effective at conveying the intended structure, and is more reusable.
  As and additional note, @extends should always occur first.
  
  
**[⬆ back to top](#table-of-contents)**
 
## Ampersand
 
  These are really power full and offfer some unique effects.  First, they can be used to nest pseudo-selectors.  Second, you are able to nest modifiers!
  
```css
  .weather {
    background: LightCyan;
    &:hover {
      background: DarkCyan;
    }
    &::before {
      content: "";
      display: block;
    }
    
    &.closed {
      display: none;
    }
  }
```

  The resulting CSS:
```css
  .weather {
    background: LightCyan;
  }
  .weather:hover {
    background: DarkCyan;
  }
  .weather::before {
    content: "";
    display: block;
  }
  .weather.closed {
    display: none;
  }
```
  
  As is immediately apparent this makes writting the CSS significantly clearer and reduces the opportunities for mistakses.
  
**[⬆ back to top](#table-of-contents)**

## Inline SVG

  As .svg files are text files anyway, they can easily be inlined, improving performance via reducing server requests.  Using svg-loader is also more efficient than url-loader, as it does not require the svg image to be converted to base64, as is the case for our build process for url-loader. An example:
  
```css
  .user-icon {
      background-image: svg-load('./../../img/icon_username.svg');
  }
```

  As an additional note, if css classes are included in the svg, these can be modified via css selectors.

**[⬆ back to top](#table-of-contents)**

## Sass Tutorials
    
  - [CSS Author](http://www.cssauthor.com/sass-tutorials/)
      
      
**[⬆ back to top](#table-of-contents)**
 
