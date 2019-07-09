# Front-End-FAQ
Get questions and answers from JR IT professional community

## Why we do this?
Collect high-quality ansers from hot questions when immigrate to Australia and work in Australia.

## General

## CSS

<details>
<summary>What is the difference between absolute and fixed positioning?</summary>

_Absolute positioning allows you to place any page element exactly where you want it._ You use the positioning attributes `top`, `left`, `bottom`, and `right` to set the location. Eg. `position: absolute; top: 40px; left: 40px;`. These values are relative to the closest parent element that is **not** set to `position: static` (the default value for the `position` property). When you absolute position an element you treat it as an independent element on the page, which means it  will not be affected by other elements and it won't affect other elements.

_A fixed position element is positioned relative to the viewport, or the browser window itself._ This is often used for navigation or sidebars because the viewport does not change at scrolling. So your fixed element will remain at the exact position you set it at. Ex. `position: fixed; top: 80px; left: 10px;`  

</details>

<details>
<summary>What is CSS BEM?</summary>

The BEM methodology is a naming convention for CSS classes in order to keep CSS more maintainable by defining namespaces to solve scoping issues. BEM stands for Block Element Modifier which is an explanation for its structure. A Block is a standalone component that is reusable across projects and acts as a "namespace" for sub components (Elements). Modifiers are used as flags when a Block or Element is in a certain state or is different in structure or style.

```css
/* block component */
.block {
}

/* element */
.block__element {
}

/* modifier */
.block__element--modifier {
}
```

Here is an example with the class names on markup:

```html
<nav class="navbar">
  <a href="/" class="navbar__link navbar__link--active"></a>
  <a href="/" class="navbar__link"></a>
  <a href="/" class="navbar__link"></a>
</nav>
```

In this case, `navbar` is the Block, `navbar__link` is an Element that makes no sense outside of the `navbar` component, and `navbar__link--active` is a Modifier that indicates a different state for the `navbar__link` Element.

Since Modifiers are verbose, many opt to use `is-*` flags instead as modifiers.

```html
<a href="/" class="navbar__link is-active"></a>
```

These must be chained to the Element and never alone however, or there will be scope issues.

```css
.navbar__link.is-active {
}
```

</details>

<details>
<summary>What are the advantages of using CSS preprocessors?</summary>

CSS preprocessors add useful functionality that native CSS does not have, and generally make CSS neater and more maintainable by enabling DRY (Don't Repeat Yourself) principles. Their terse syntax for nested selectors cuts down on repeated code. They provide variables for consistent theming (however, CSS variables have largely replaced this functionality) and additional tools like color functions (`lighten`, `darken`, `transparentize`, etc), mixins, and loops that make CSS more like a real programming language and gives the developer more power to generate complex CSS.


#### Good to hear


* They allow us to write more maintainable and scalable CSS
* Some disadvantages of using CSS preprocessors (setup, re-compilation time can be slow etc.)


##### Additional Links


* [CSS Preprocessors](https://medium.com/@garyfagan/css-preprocessors-6f226fa16f27)

</details>

<details>
<summary>What is the difference between `em` and `rem` units?</summary>

Both `em` and `rem` units are based on the `font-size` CSS property. The only difference is where they inherit their values from.

* `em` units inherit their value from the `font-size` of the parent element
* `rem` units inherit their value from the `font-size` of the root element (`html`)

In most browsers, the `font-size` of the root element is set to `16px` by default.


#### Good to hear


* Benefits of using `em` and `rem` units


##### Additional Links


* [CSS units for font-size: px | em | rem](https://medium.com/code-better/css-units-for-font-size-px-em-rem-79f7e592bb97)

</details>

<details>
<summary>What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?</summary>

* **Resetting** - Resetting is meant to strip all default browser styling on elements. For e.g. `margin`s, `padding`s, `font-size`s of all elements are reset to be the same. You will have to redeclare styling for common typographic elements.
* **Normalizing** - Normalizing preserves useful default styles rather than "unstyling" everything. It also corrects bugs for common browser dependencies.

I would choose resetting when I have a very customized or unconventional site design such that I need to do a lot of my own styling and do not need any default styling to be preserved.

</details>

<details>
<summary> Describe `float`s and how they work.</summary>
Float is a CSS positioning property. Floated elements remain a part of the flow of the page, and will affect the positioning of other elements (e.g. text will flow around floated elements), unlike `position: absolute` elements, which are removed from the flow of the page.

The CSS `clear` property can be used to be positioned below `left`/`right`/`both` floated elements.

If a parent element contains nothing but floated elements, its height will be collapsed to nothing. It can be fixed by clearing the float after the floated elements in the container but before the close of the container.

The `.clearfix` hack uses a clever CSS pseudo selector (`:after`) to clear floats. Rather than setting the overflow on the parent, you apply an additional class `clearfix` to it. Then apply this CSS:

```css
.clearfix:after {
  content: ' ';
  visibility: hidden;
  display: block;
  height: 0;
  clear: both;
}
```

Alternatively, give `overflow: auto` or `overflow: hidden` property to the parent element which will establish a new block formatting context inside the children and it will expand to contain its children.

</details>

<details>
<summary>Explain CSS sprites, and how you would implement them on a page or site.</summary>

CSS sprites combine multiple images into one single larger image. It is a commonly-used technique for icons (Gmail uses it). How to implement it:

1. Use a sprite generator that packs multiple images into one and generate the appropriate CSS for it.
1. Each image would have a corresponding CSS class with `background-image`, `background-position` and `background-size` properties defined.
1. To use that image, add the corresponding class to your element.

**Advantages:**

* Reduce the number of HTTP requests for multiple images (only one single request is required per spritesheet). But with HTTP2, loading multiple images is no longer much of an issue.
* Advance downloading of assets that won't be downloaded until needed, such as images that only appear upon `:hover` pseudo-states. Blinking wouldn't be seen.


</details>

<details>
<summary>What are the different ways to visually hide content (and make it available only for screen readers)?</summary>

These techniques are related to accessibility (a11y).

* `visibility: hidden`. However, the element is still in the flow of the page, and still takes up space.
* `width: 0; height: 0`. Make the element not take up any space on the screen at all, resulting in not showing it.
* `position: absolute; left: -99999px`. Position it outside of the screen.
* `text-indent: -9999px`. This only works on text within the `block` elements.
* Metadata. For example by using Schema.org, RDF, and JSON-LD.
* WAI-ARIA. A W3C technical specification that specifies how to increase the accessibility of web pages.

Even if WAI-ARIA is the ideal solution, I would go with the `absolute` positioning approach, as it has the least caveats, works for most elements and it's an easy technique.

</details>

<details>
<summary>Are you familiar with styling SVG?
</summary>

Yes, there are several ways to color shapes (including specifying attributes on the object) using inline CSS, an embedded CSS section, or an external CSS file. Most SVG you'll find around the web use inline CSS, but there are advantages and disadvantages associated with each type.

Basic coloring can be done by setting two attributes on the node: `fill` and `stroke`. `fill` sets the color inside the object and `stroke` sets the color of the line drawn around the object. You can use the same CSS color naming schemes that you use in HTML, whether that's color names (that is `red`), RGB values (that is `rgb(255,0,0)`), Hex values, RGBA values, etc.

```html
<rect x="10" y="10" width="100" height="100" stroke="blue" 
  fill="purple" fill-opacity="0.5" stroke-opacity="0.8"/>
```

</details>


<details>
<summary>Can you give an example of an @media property other than screen?</summary>

Yes, there are four types of @media properties (including _screen_):

* `all` - for all media type devices
* `print` - for printers
* `speech` - for screenreaders that "reads" the page out loud
* `screen` - for computer screens, tablets, smart-phones etc.

Here is an example of `print` media type's usage:

```css
@media print {
  body {
    color: black;
  }
}
```

</details>


<details>
<summary>What are the advantages/disadvantages of using CSS preprocessors?</summary>

**Advantages:**

* CSS is made more maintainable.
* Easy to write nested selectors.
* Variables for consistent theming. Can share theme files across different projects.
* Mixins to generate repeated CSS.
* Splitting your code into multiple files. CSS files can be split up too but doing so will require an HTTP request to download each CSS file.

**Disadvantages:**

* Requires tools for preprocessing. Re-compilation time can be slow.

</details>

<details>
<summary>Explain how a browser determines what elements match a CSS selector.</summary>

This part is related to the above about writing efficient CSS. Browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.

For example with this selector `p span`, browsers firstly find all the `<span>` elements and traverse up its parent all the way up to the root to find the `<p>` element. For a particular `<span>`, as soon as it finds a `<p>`, it knows that the `<span>` matches and can stop its matching.

</details>

<details>
<summary>Describe pseudo-elements and discuss what they are used for.</summary>

A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s). They can be used for decoration (`:first-line`, `:first-letter`) or adding elements to the markup (combined with `content: ...`) without having to modify the markup (`:before`, `:after`).

* `:first-line` and `:first-letter` can be used to decorate text.
* Used in the `.clearfix` hack as shown above to add a zero-space element with `clear: both`.
* Triangular arrows in tooltips use `:before` and `:after`. Encourages separation of concerns because the triangle is considered part of styling and not really the DOM. It's not really possible to draw a triangle with just CSS styles without using an additional HTML element.
* 
</details>

<details>
<summary>What's the difference between `inline` and `inline-block`?</summary>

I shall throw in a comparison with `block` for good measure.

|                                      | `block`                                                                                     | `inline-block`                                                      | `inline`                                                                                                                                                                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size                                 | Fills up the width of its parent container.                                                 | Depends on content.                                                 | Depends on content.                                                                                                                                                                                                  |
| Positioning                          | Start on a new line and tolerates no HTML elements next to it (except when you add `float`) | Flows along with other content and allows other elements beside it. | Flows along with other content and allows other elements beside it.                                                                                                                                                  |
| Can specify `width` and `height`     | Yes                                                                                         | Yes                                                                 | No. Will ignore if being set.                                                                                                                                                                                        |
| Can be aligned with `vertical-align` | No                                                                                          | Yes                                                                 | Yes                                                                                                                                                                                                                  |
| Margins and paddings                 | All sides respected.                                                                        | All sides respected.                                                | Only horizontal sides respected. Vertical sides, if specified, do not affect layout. Vertical space it takes up depends on `line-height`, even though the `border` and `padding` appear visually around the content. |
| Float                                | -                                                                                           | -                                                                   | Becomes like a `block` element where you can set vertical margins and paddings.                                                                                                                                      |
</details>


<details>
<summary>Have you played around with the new CSS Flexbox or Grid specs?</summary>

Yes. Flexbox is mainly meant for 1-dimensional layouts while Grid is meant for 2-dimensional layouts.

Flexbox solves many common problems in CSS, such as vertical centering of elements within a container, sticky footer, etc. Bootstrap and Bulma are based on Flexbox, and it is probably the recommended way to create layouts these days. Have tried Flexbox before but ran into some browser incompatibility issues (Safari) in using `flex-grow`, and I had to rewrite my code using `inline-blocks` and math to calculate the widths in percentages, it wasn't a nice experience.

Grid is by far the most intuitive approach for creating grid-based layouts (it better be!) but browser support is not wide at the moment.

</details>

## HTML

<details>
<summary>What does a DOCTYPE do?</summary>

**DOCTYPE** is an abbreviation for **DOCument TYPE**.  
A DOCTYPE is always associated to a **DTD** - for **Document Type Definition**.  

A DTD defines how documents of a certain type should be structured (i.e. a `button` can contain a `span` but not a `div`), whereas a DOCTYPE declares what DTD a document *supposedly* respects (i.e. this document respects the HTML DTD).  

For webpages, the DOCTYPE declaration is required. It is used to tell user agents what version of the HTML specifications your document respects.  
Once a user agent has recognized a correct DOCTYPE, it will trigger the **no-quirks mode** matching this DOCTYPE for reading the document.  
If a user agent doesn't recognize a correct DOCTYPE, it will trigger the **quirks mode**.

The DOCTYPE declaration for the HTML5 standards is `<!DOCTYPE html>`.

</details>

<details>
<summary>What kind of things must you be wary of when designing or developing for multilingual sites?</summary>

* Use `lang` attribute in your HTML.
* Directing users to their native language - Allow a user to change his country/language easily without hassle.
* Text in images is not a scalable approach - Placing text in an image is still a popular way to get good-looking, non-system fonts to display on any computer. However, to translate image text, each string of text will need to have it's a separate image created for each language. Anything more than a handful of replacements like this can quickly get out of control.
* Restrictive words/sentence length - Some content can be longer when written in another language. Be wary of layout or overflow issues in the design. It's best to avoid designing where the amount of text would make or break a design. Character counts come into play with things like headlines, labels, and buttons. They are less of an issue with free-flowing text such as body text or comments.
* Be mindful of how colors are perceived - Colors are perceived differently across languages and cultures. The design should use color appropriately.
* Formatting dates and currencies - Calendar dates are sometimes presented in different ways. Eg. "May 31, 2012" in the U.S. vs. "31 May 2012" in parts of Europe.
* Do not concatenate translated strings - Do not do anything like `"The date today is " + date`. It will break in languages with different word order. Use a template string with parameters substitution for each language instead. For example, look at the following two sentences in English and Chinese respectively: `I will travel on {% date %}` and `{% date %} 我会出发`. Note that the position of the variable is different due to grammar rules of the language.
* Language reading direction - In English, we read from left-to-right, top-to-bottom, in traditional Japanese, text is read up-to-down, right-to-left.

</details>

<details>
<summary>What are `data-` attributes good for?</summary>

Before JavaScript frameworks became popular, front end developers used `data-` attributes to store extra data within the DOM itself, without other hacks such as non-standard attributes, extra properties on the DOM. It is intended to store custom data private to the page or application, for which there are no more appropriate attributes or elements.

These days, using `data-` attributes is not encouraged. One reason is that users can modify the data attribute easily by using inspect element in the browser. The data model is better stored within JavaScript itself and stay updated with the DOM via data binding possibly through a library or a framework.

</details>

<details>
<summary>Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.</summary>

All the above-mentioned technologies are key-value storage mechanisms on the client side. They are only able to store values as strings.

|                                        | `cookie`                                                 | `localStorage` | `sessionStorage` |
| -------------------------------------- | -------------------------------------------------------- | -------------- | ---------------- |
| Initiator                              | Client or server. Server can use `Set-Cookie` header     | Client         | Client           |
| Expiry                                 | Manually set                                             | Forever        | On tab close     |
| Persistent across browser sessions     | Depends on whether expiration is set                     | Yes            | No               |
| Sent to server with every HTTP request | Cookies are automatically being sent via `Cookie` header | No             | No               |
| Capacity (per domain)                  | 4kb                                                      | 5MB            | 5MB              |
| Accessibility                          | Any window                                               | Any window     | Same tab         |
</details>

<details>

<summary>Describe the difference between script , script async and script defer. </summary>

* Scope safety: Until arrow functions, every new function defined its own this value (a new object in the case of a constructor, undefined in strict mode function calls, the base object if the function is called as an "object method", etc.). An arrow function does not create its own this, the this value of the enclosing execution context is used. 
* Compactness: Arrow functions are easier to read and write.
* Clarity: When almost everything is an arrow function, any regular function immediately sticks out for defining the scope. A developer can always look up the next-higher function statement to see what the thisObject is.

</details>


<details>
<summary>Have you used different HTML templating languages before?</summary>

Yes, Pug (formerly Jade), ERB, Slim, Handlebars, Jinja, Liquid, just to name a few. In my opinion, they are more or less the same and provide similar functionality of escaping content and helpful filters for manipulating the data to be displayed. Most templating engines will also allow you to inject your own filters in the event you need custom processing before display.

</details>

## Javascript

<details>
<summary>What advantages are there in using arrow functions?</summary>

* Scope safety: Until arrow functions, every new function defined its own this value (a new object in the case of a constructor, undefined in strict mode function calls, the base object if the function is called as an "object method", etc.). An arrow function does not create its own this, the this value of the enclosing execution context is used. 
* Compactness: Arrow functions are easier to read and write.
* Clarity: When almost everything is an arrow function, any regular function immediately sticks out for defining the scope. A developer can always look up the next-higher function statement to see what the thisObject is.

</details>

<details>
<summary>What is a pure function?</summary>

A pure function is a function that doesn't depend on and doesn't modify the states of variables out of its scope. Essentially, this means that a pure function will always return the same result given same parameters.

</details>

## Node

<details>
<summary>What is the event loop in Node.js?</summary>

The event loop handles all async callbacks. Callbacks are queued in a loop, while other code runs, and will run one by one when the response for each one has been received.

#### Good to hear

* The event loop allows Node.js to perform non-blocking I/O operations, despite the fact that JavaScript is single-threaded

##### Additional Links

* [Node.js docs on event loop, timers and process.nextTick()](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)

</details>


## React

<details>
<summary>How does React work?</summary>

React creates a virtual DOM. When state changes in a component it firstly runs a "diffing" algorithm, which identifies what has changed in the virtual DOM. The second step is reconciliation, where it updates the DOM with the results of diff.

</details>

<details>
<summary>What are the major features of React?</summary>

The major features of React are:

* It uses **VirtualDOM** instead RealDOM considering that RealDOM manipulations are expensive.
* Supports **server-side rendering**.
* Follows *Unidirectional** data flow or data binding.
* Uses **reusable/composable** UI components to develop the view.

</details>

<details>
<summary>What are the advantages of using React?</summary>

- It is easy to know how a component is rendered, you just need to look at the render function.
- JSX makes it easy to read the code of your components. It is also really easy to see the layout, or how components are plugged/combined with each other.
- You can render React on the server-side. This enables improves SEO and performance.
- It is easy to test.
- You can use React with any framework (Backbone.js, Angular.js) as it is only a view layer.

</details>

<details>
<summary>What is the difference between HTML and React event handling?</summary>

1. In HTML, the event name should be in *lowercase*:

 ```html
 <button onclick='activateLasers()'>
 ```

 Whereas in React it follows *camelCase* convention:

 ```jsx harmony
 <button onClick={activateLasers}>
 ```

 1. In HTML, you can return `false` to prevent default behavior:

 ```html
 <a href='#' onclick='console.log("The link was clicked."); return false;' />
 ```

 Whereas in React you must call `preventDefault()` explicitly:

 ```javascript
 function handleClick(event) {
   event.preventDefault()
   console.log('The link was clicked.')
 }
 ```


</details>

<details>
<summary>How to create components in React?</summary>


There are two possible ways to create a component.

1. **Function Components:** This is the simplest way to create a component. Those are pure JavaScript functions that accept props object as first parameter and return React elements:

    ```jsx harmony
    function Greeting({ message }) {
      return <h1>{`Hello, ${message}`}</h1> 
    }
    ```

2. **Class Components:** You can also use ES6 class to define a component. The above function component can be written as:

    ```jsx harmony
    class Greeting extends React.Component {
      render() {
        return <h1>{`Hello, ${this.props.message}`}</h1>
      }
    }
    ```

</details>

<details>
<summary>What is the difference between a Presentational component and a Container component?</summary>

Presentational components are concerned with how things look. They generally receive data and callbacks exclusively via props. These components rarely have their own state, but when they do it generally concerns UI state, as opposed to data state.

Container components are more concerned with how things work. These components provide the data and behavior to presentational or other container components. They call Flux actions and provide these as callbacks to the presentational components. They are also often stateful as they serve as data sources. 

</details>

<details>
<summary>What are the differences between a class component and functional component?</summary>

- Class components allows you to use additional features such as local state and lifecycle hooks. Also, to enable your component to have direct access to your store and thus holds state.

- When your component just receives props and renders them to the page, this is a 'stateless component', for which a pure function can be used. These are also called dumb components or presentational components.

</details>

<details>
<summary>What are Pure Components?</summary>

 *`React.PureComponent`* is exactly the same as *`React.Component`* except that it handles the `shouldComponentUpdate()` method for you. When props or state changes, *PureComponent* will do a shallow comparison on both props and state. *Component* on the other hand won't compare current props and state to next out of the box. Thus, the component will re-render by default whenever `shouldComponentUpdate` is called.

</details>

<details>
<summary>Why should we not update the state directly?</summary>

If you try to update state directly then it won't re-render the component.

```javascript
//Wrong
this.state.message = 'Hello world'
```

Instead use `setState()` method. It schedules an update to a component's state object. When state changes, the component responds by re-rendering.

```javascript
//Correct
this.setState({ message: 'Hello World' })
```

**Note:** You can directly assign to the state object either in *constructor* or using latest javascript's class field declaration syntax.

</details>

<details>
<summary>What is the difference between state and props?</summary>

The state is a data structure that starts with a default value when a Component mounts. It may be mutated across time, mostly as a result of user events.

Props (short for properties) are a Component's configuration. They are received from above and immutable as far as the Component receiving them is concerned. A Component cannot change its props, but it is responsible for putting together the props of its child Components. Props do not have to just be data - callback functions may be passed in as props.

</details>

<details>
<summary>What is the difference of lifecycle methods in React?</summary>
React 16.3+

- **getDerivedStateFromProps:** Invoked right before calling `render()` and is invoked on *every* render. This exists for rare use cases where you need derived state. Worth reading [if you need derived state](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html).
- **componentDidMount:** Executed after first rendering and here all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default it returns `true`. If you are sure that the component doesn't need to render after state or props are updated, you can return false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives new prop.
- **getSnapshotBeforeUpdate:** Executed right before rendered output is committed to the DOM. Any value returned by this will be passed into `componentDidUpdate()`. This is useful to capture information from the DOM i.e. scroll position.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes. This will not fire if `shouldComponentUpdate()` returns `false`.
- **componentWillUnmount** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

Before 16.3

- **componentWillMount:** Executed before rendering and is used for App level configuration in your root component.
- **componentDidMount:** Executed after first rendering and here all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **componentWillReceiveProps:** Executed when particular prop updates to trigger state transitions.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default it returns `true`. If you are sure that the component doesn't need to render after state or props are updated, you can return false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives new prop.
- **componentWillUpdate:** Executed before re-rendering the component when there are props & state changes confirmed by `shouldComponentUpdate()` which returns true.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes.
- **componentWillUnmount:** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

</details>

<details>
<summary>Where in a React component should you make an AJAX request?</summary>

`componentDidMount` is where an AJAX request should be made in a React component. This method will be executed when the component “mounts” (is added to the DOM) for the first time. This method is only executed once during the component’s life. Importantly, you can’t guarantee the AJAX request will have resolved before the component mounts. If it doesn't, that would mean that you’d be trying to setState on an unmounted component, which would not work. Making your AJAX request in `componentDidMount` will guarantee that there’s a component to update.

</details>

<details>
<summary>What are refs used for in React?</summary>

Refs are used to get reference to a DOM node or an instance of a component in React. Good examples of when to use refs are for managing focus/text selection, triggering imperative animations, or integrating with third-party DOM libraries. You should avoid using string refs and inline ref callbacks. Callback refs are advised by React.

</details>

<details>
<summary>What is the alternative of binding `this` in the constructor?</summary>

You can use property initializers to correctly bind callbacks. This is enabled by default in create react app.
You can use an arrow function in the callback. The problem here is that a new callback is created each time the component renders.

</details>

<details>
<summary>What is the purpose of super(props)?</summary>

A child class constructor cannot make use of `this` until `super()` has been called. Also, ES2015 class constructors have to call `super()` if they are subclasses. The reason for passing `props` to `super()` is to enable you to access `this.props` in the constructor.

</details>

<details>
<summary>How would you prevent a component from rendering?</summary>

Returning null from a component's render method does not affect the firing of the component's lifecycle methods.

</details>

<details>
<summary>Why is it advised to pass a callback function to setState as opposed to an object?</summary>

Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

</details>

<details>
<summary>What is the alternative of binding `this` in the constructor?</summary>

You can use property initializers to correctly bind callbacks. This is enabled by default in create react app.
you can use an arrow function in the callback. The problem here is that a new callback is created each time the component renders.

</details>

<details>
<summary>What are stateless components?</summary>

If the behaviour is independent of its state then it can be a stateless component. You can use either a function or a class for creating stateless components. But unless you need to use a lifecycle hook in your components, you should go for function components. There are a lot of benefits if you decide to use function components here; they are easy to write, understand, and test, a little faster, and you can avoid the `this` keyword altogether.

</details>

<details>
<summary>What are stateful components?</summary>

If the behaviour of a component is dependent on the *state* of the component then it can be termed as stateful component. These *stateful components* are always *class components* and have a state that gets initialized in the `constructor`.

```javascript
class App extends Component {
  constructor(props) {
    super(props)
    this.state = { count: 0 }
  }

  render() {
    // ...
  }
}
```

</details>

<details>
<summary>How would you prevent a component from rendering?</summary>

Returning null from a component's render method means nothing will be displayed, but it does not affect the firing of the component's lifecycle methods. 

If the amount of times the component re-renders is an issue, there are two options available. Manually implementing a check in the `shouldComponentUpdate` lifecycle method hook. 
```
shouldComponentUpdate(nextProps, nextState){
  // Do some check here
  return resultOFCheckAsBoolean
}
```

Or using React.PureComponent instead of React.Component
React.PureComponent implements `shouldComponentUpdate()` with a shallow prop and state comparison. This enables you to avoid re-rendering the component with the same props and state.

</details>

<details>
<summary>When rendering a list what is a key and what is it's purpose?</summary>

Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity. The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys. When you don't have stable IDs for rendered items, you may use the item index as a key as a last resort. It is not recommend to use indexes for keys if the items can reorder, as that would be slow. 

</details>

<details>
<summary>What is JSX?</summary>

JSX is a syntax extension to JavaScript and comes with the full power of JavaScript. JSX produces React "elements". You can embed any JavaScript expression in JSX by wrapping it in curly braces. After compilation, JSX expressions become regular JavaScript objects. This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions:

</details>

### Redux

<details>
<summary>What is redux?</summary>

The basic idea of redux is that the entire application state is kept in a single store. The store is simply a javascript object. The only way to change the state is by sending actions from your application and then writing reducers for these actions that modify the state. The entire state transition is kept inside reducers and should not have any side-effects.

</details>

<details>
<summary>What is a store in redux?</summary>

The store is a javascript object that holds application state. Along with this it also has the following responsibilities:
- Allows access to state via `getState()`;
- Allows state to be updated via `dispatch(action)`;
- Registers listeners via `subscribe(listener)`;
- Handles unregistering of listeners via the function returned by `subscribe(listener)`.

</details>

<details>
<summary>What is an action?</summary>

Actions are plain javascript objects. They must have a type indicating the type of action being performed. In essence, actions are payloads of information that send data from your application to your store. 

</details>

<details>
<summary>What is a reducer?</summary>

A reducer is simply a pure function that takes the previous state and an action, and returns the next state.

</details>

<details>
<summary>What is Redux Thunk used for?</summary>

Redux thunk is middleware that allows you to write action creators that return a function instead of an action. The thunk can then be used to delay the dispatch of an action if a certain condition is met. This allows you to handle the asynchronous dispatching of actions.

</details>



## Angular


## Australia IT Professional Community

[Sydney JR Academy | Code bootcamp](https://jiangren.com.au/city/sydney).
[Melbourne JR Academy | Code bootcamp](https://jiangren.com.au/city/melbourne).
[Brisbane JR Academy | Code bootcamp](https://jiangren.com.au/city/brisbane).