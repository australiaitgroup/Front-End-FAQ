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


