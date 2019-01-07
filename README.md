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

## HTML

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
<summary>What are the advantages of using React?</summary>

- It is easy to know how a component is rendered, you just need to look at the render function.
- JSX makes it easy to read the code of your components. It is also really easy to see the layout, or how components are plugged/combined with each other.
- You can render React on the server-side. This enables improves SEO and performance.
- It is easy to test.
- You can use React with any framework (Backbone.js, Angular.js) as it is only a view layer.

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
<summary>What is the difference between state and props?</summary>

The state is a data structure that starts with a default value when a Component mounts. It may be mutated across time, mostly as a result of user events.

Props (short for properties) are a Component's configuration. They are received from above and immutable as far as the Component receiving them is concerned. A Component cannot change its props, but it is responsible for putting together the props of its child Components. Props do not have to just be data - callback functions may be passed in as props.

</details>

<details>
<summary>What is the difference of lifecycle methods in React?</summary>

- `componentWillMount`- this is most commonly used for App configuration in your root component. 
- `componentDidMount` - here you want to do all the setup you couldn’t do without a DOM, and start getting all the data you need. Also if you want to set up eventListeners etc. this lifecycle hook is a good place to do that.
- `componentWillReceiveProps` - this lifecyclye acts on particular prop changes to trigger state transitions.
- `shouldComponentUpdate` - if you’re worried about wasted renders `shouldComponentUpdate` is a great place to improve performance as it allows you to prevent a rerender if component receives new `prop`. `shouldComponentUpdate` should always return a boolean and based on what this is will determine if the component is rerendered or not.
- `componentWillUpdate` - rarely used. It can be used instead of `componentWillReceiveProps` on a component that also has `shouldComponentUpdate` (but no access to previous props).
- `componentDidUpdate` - also commonly used to update the DOM in response to prop or state changes.
- `componentWillUnmount` - here you can cancel any outgoing network requests, or remove all event listeners associated with the component.

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

### Redux


## Angular


## Australia IT Professional Community

[Sydney JR Academy | Code bootcamp](https://jiangren.com.au/city/sydney).
[Melbourne JR Academy | Code bootcamp](https://jiangren.com.au/city/melbourne).
[Brisbane JR Academy | Code bootcamp](https://jiangren.com.au/city/brisbane).