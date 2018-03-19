# React Concepts
* An element is a plain object describing a component instance or a DOM node and its desired property. It is a object representation of what is rendered on the browser.

* A React component is a function that returns an element or a class that has a render function that returns an element. This element is a like a component instance.

* The props property of a component should never be modified by itself. It is a read only property of the component. It's the parent component that can change its props.

* The `render()` method of a component tells React what should be displayed in the DOM. React then updates the DOM to match the virtual DOM.

* A component class can maintain a local state as a class variable, called `state`. This state can be used along with the props property to define the render return. If something is not to be used in the render but you want to keep the information, it shouldn't be in the state. Rather use a class property.  

* The lifecycle methods of a class component is `componentDidMount` and `componentWillUnmount`

* React.Component class, which extends a custom react component, has a method called `setState()`. This method is called by react asynchronously. Sometime, it may be called in a batch. Because `this.state` and `this.props` may be updated async, we can't rely on their value to be coherent.

* `setState()` method is the way to tell react that the state has changed. React, asynchronously, updates the state and based on that new state calls the `render()` method to figure out what has changed in the virtual DOM i.e. what should be on the screen.

* `setState` method takes an object argument which is added to the state object as a property next time `setState` is called. We can never assign a value to state directly like so `this.state.comments = {}`. Direct assignment to state can only happen when the class in instanciated.

* `setState` also takes a function argument `(prevState, props) => {}`. This can be used to update the state by returning an object with new properties based on the current props and previous state. `props` is the value at the time the update is applied by react.

* React merges the properties provided in the object retuned by the closure or directly passed to the `setState` function with the current state to get the new state.

* The state and props of parent can be used to set `props` of the children.

* This is commonly called a “top-down” or “unidirectional” data flow. Any state is always owned by some specific component, and any data or UI derived from that state can only affect components “below” them in the tree.

* Bind all the class methods to `this` in the constructor to be safe. It makes sure that even though the method is called by React in a different context (as a response to an onClick event for instance), it is able to access the class `this`.  

## Lifecycle methods

### `constructor()`
Constructor method is used to initialize the local state, if you need any, and to bind the methods to `this`. One can initialize the state based on the value of props, but the value would be *forked*, and it won't keep a reference to the `props`. To keep the state up to date with `props`, use `componentWillReceiveProps(props)` method.
Also, avoid using any subscriptions or any side-effects in the constructor.

### `componentWillMount()`
It is called right before `render()`. Setting `setState()` synchronously in this method will not trigger extra rendering.
Also, avoid using any subscriptions or any side-effects in the constructor. 

### `componentDidMount()`
Use this for network request, subscriptions, and `setState()`. Note that the browser window is displayed the new component yet. Any `setState()` called here might call render again. Even though `render` is called twice, the user won't see the intermediate state. Use it with cautin as it may cause performance issues. This is similar to `viewDidLoad()` in iOS. You can access DOM properties like size etc.

### `componentWillReceiveProps(nextProps)`
This method is called whenever the parent wants to re-render the component. It will receive the new `props`, nextProps. The `props` doesn't have to change just because the parent is re-rendering the component.
Use `setState` to change the state based on current `props` and `nextProps`.

### `shouldComponentUpdate()`
This method is invoked before rendering when new props or state are being received. This method is not called for the initial render or when  `forceUpdate()` is used.
Use this for optimization
