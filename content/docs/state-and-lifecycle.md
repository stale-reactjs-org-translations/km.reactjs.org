---
id: state-and-lifecycle
title: State និង Lifecycle
permalink: docs/state-and-lifecycle.html
redirect_from:
  - "docs/interactivity-and-dynamic-uis.html"
prev: components-and-props.html
next: handling-events.html
---

ទំព័រនេះបង្ហាញពីគំនិតនៃ state និង lifecycle នៅក្នុង React component. អ្នកអាចរកឃើញ [លំអិត API component លំអិតនៅទីនេះ](/docs/react-component.html).

សូមពិចារណាគំរូនាឡិកាពី [ផ្នែកមួយនៃផ្នែកមុន](/docs/rendering-elements.html#updating-the-rendered-element). នៅក្នុង [ការបង្ហាញធាតុ](/docs/rendering-elements.html#rendering-an-element-into-the-dom),យើងទើបតែរៀនវិធីដើម្បីធ្វើបច្ចុប្បន្នភាព UI តែមួយប៉ុណ្ណោះ. យើង​ហៅ `ReactDOM.render()` ដើម្បីផ្លាស់ប្តូរលទ្ធផលបង្ហាញ:

```js{8-11}
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/gwoJZk?editors=0010)

នៅក្នុងផ្នែកនេះ យើងនឹងរៀនពីរបៀបបង្កើត component `Clock` ដែលអាចប្រើឡើងវិញបាន និង encapsulated. វានឹងបង្កើតកម្មវិធីកំណត់ពេលវេលាផ្ទាល់ខ្លួនរបស់វាហើយធ្វើបច្ចុប្បន្នភាពរៀងរាល់វិនាទី។

យើងអាចចាប់ផ្ដើមដោយ encapsulating របៀបមើលនាឡិកា:

```js{3-6,12}
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/dpdoYR?editors=0010)

ទោះយ៉ាងណា, វានឹកនូវតម្រូវការដ៏សំខាន់មួយ:ការពិតដែលថា `Clock` កំណត់កម្មវិធីកំណត់ពេលវេលាមួយនិងធ្វើបច្ចុប្បន្នភាព UI ជារៀងរាល់វិនាទីគួរតែជាការអនុវត្ដន៍លម្អិតនៃ `Clock`.

ជាគំនិត យើងចង់សរសេរវាម្តងនិងមានការធ្វើឱ្យទាន់សម័យ 'Clock' ខ្លួនវាផ្ទាល់:

```js{2}
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

ដើម្បីអនុវត្ត យើងត្រូវបន្ថែម "state" ទៅcomponent `Clock` ។

State គឺស្រដៀងទៅនឹង props ប៉ុន្តែវាមានលក្ខណៈឯកជនហើយត្រូវបានគ្រប់គ្រងយ៉ាងពេញលេញដោយ component។

យើង [បានរៀបរាប់ពីមុន](/docs/components-and-props.html#functional-and-class-components) components ដែលបានកំណត់ជា classes មានលក្ខណៈពិសេសបន្ថែមមួយចំនួន. Local state គឺពិតប្រាកដណាស់: អាចប្រើបានតែចំពោះ classes.

## បម្លែង Function ទៅ Class {#converting-a-function-to-a-class}

អ្នកអាចបម្លែង function component ដូច `Clock` ទៅ class ក្នុងប្រាំជំហាន:

1. បង្កើត [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes), ជាមួយឈ្មោះដូចគ្នា, នោះ extends `React.Component`.

2. បន្ថែមវិធីសាស្ត្រទទេមួយទៅវា `render()`.

3. ផ្លាស់ទីនៃតួ function ចូលទៅក្នុង `render()`.

4. ជំនួស `props` ជាមួយ `this.props` ក្នុង `render()` body.

5. លុបការប្រកាស function ទទេដែលនៅសល់។

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/zKRGpo?editors=0010)

`Clock` ឥឡូវត្រូវបានកំណត់ជា class ជាជាង function។

វិធីសាស្ត្រ `render` នឹងត្រូវបានហៅរាល់ពេលដែលការធ្វើបច្ចុប្បន្នភាពកើតឡើង, ប៉ុន្តែដរាបណាយើងបង្ហាញ `<Clock />` ចូលទៅក្នុង DOM node ដូចគ្នា, មានតែវត្ថុតែមួយនៃ `Clock` class នឹងត្រូវបានប្រើ. នេះអនុញ្ញាតឱ្យយើងប្រើលក្ខណៈពិសេសបន្ថែមដូចជា local state និង lifecycle methods។

## បន្ថែម Local State ទៅ Class {#adding-local-state-to-a-class}

យើងនឹងផ្លាស់ទី `date` ពី props ទៅ state ក្នុងបីជំហាន:

1) ជំនួស `this.props.date` ជាមួយ `this.state.date` ក្នុង `render()`:

```js{6}
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

2) បន្ថែម [class constructor](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor) ដែលកំណត់ដំបូង `this.state`:

```js{4}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

ចំណាំពីរបៀបដែលយើងហុច `props` ទៅ constructor:

```js{2}
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

Class components គួរតែហៅ constructor ជាមួយ `props`.

3) យក `date` ចេញពីធាតុ `<Clock />`:

```js{2}
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

ក្រោយមកយើងនឹងបន្ថែមកូដកំណត់ពេលវេលាទៅ component ខ្លួនឯងវិញ។

លទ្ធផលមើលទៅដូចនេះ:

```js{2-5,11,18}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/KgQpJd?editors=0010)

បន្ទាប់មក យើងនឹងបង្កើត `Clock` បង្កើតដោយផ្ទាល់ខ្លួនរបស់វាហើយធ្វើបច្ចុប្បន្នភាពរៀងរាល់វិនាទី។

## បន្ថែម វិធីសាស្រ្ត Lifecycle ទៅ Class {#adding-lifecycle-methods-to-a-class}

នៅក្នុងកម្មវិធីដែលមាន components ជាច្រើន វាមានសារៈសំខាន់ខ្លាំងណាស់ក្នុងការធ្វើអោយមានភាពទំនេរ  នៅពេលដែល components បានប្រើប្រាស់ត្រូវបានបំផ្លាញ។

យើង​ចង់ [ធ្វើការកំណត់ពេល(timer)](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) នៅពេលណាដែល `Clock` ត្រូវបានបង្ហាញទៅ DOM ជាលើកដំបូង. នេះត្រូវបានគេហៅ "mounting" នៅ React.

យើងក៏ចង់ [ជម្រះការកំណត់ម៉ោង(timer)](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/clearInterval) នៅពេលណាដែល DOM ដែលបានផលិតដោយ`Clock` បានយកចេញ. នេះត្រូវបានគេហៅ "unmounting" នៅ React.

យើងអាចប្រកាសវិធីសាស្រ្តពិសេសនៅលើ component class ដើម្បីដំណើរការកូដមួយចំនួននៅពេលណា component mounts និង unmounts:

```js{7-9,11-13}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {

  }

  componentWillUnmount() {

  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

វិធីសាស្រ្តទាំងនេះត្រូវបានហៅ "lifecycle methods".

`componentDidMount()` ដំណើរការបន្ទាប់ពីទិន្នផលcomponentត្រូវបានបង្ហាញទៅ DOM។ នេះគឺជាទីកន្លែងល្អដើម្បីធ្វើការកំណត់ពេល(timer):

```js{2-5}
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

Note how we save the timer ID right on `this`.

While `this.props` is set up by React itself and `this.state` has a special meaning, you are free to add additional fields to the class manually if you need to store something that doesn’t participate in the data flow (like a timer ID).

We will tear down the timer in the `componentWillUnmount()` lifecycle method:

```js{2}
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

Finally, we will implement a method called `tick()` that the `Clock` component will run every second.

It will use `this.setState()` to schedule updates to the component local state:

```js{18-22}
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/amqdNA?editors=0010)

Now the clock ticks every second.

Let's quickly recap what's going on and the order in which the methods are called:

1) When `<Clock />` is passed to `ReactDOM.render()`, React calls the constructor of the `Clock` component. Since `Clock` needs to display the current time, it initializes `this.state` with an object including the current time. We will later update this state.

2) React then calls the `Clock` component's `render()` method. This is how React learns what should be displayed on the screen. React then updates the DOM to match the `Clock`'s render output.

3) When the `Clock` output is inserted in the DOM, React calls the `componentDidMount()` lifecycle method. Inside it, the `Clock` component asks the browser to set up a timer to call the component's `tick()` method once a second.

4) Every second the browser calls the `tick()` method. Inside it, the `Clock` component schedules a UI update by calling `setState()` with an object containing the current time. Thanks to the `setState()` call, React knows the state has changed, and calls the `render()` method again to learn what should be on the screen. This time, `this.state.date` in the `render()` method will be different, and so the render output will include the updated time. React updates the DOM accordingly.

5) If the `Clock` component is ever removed from the DOM, React calls the `componentWillUnmount()` lifecycle method so the timer is stopped.

## ការប្រើប្រាស់ State ឲបានត្រឹមត្រូវ {#using-state-correctly}

There are three things you should know about `setState()`.

### កុំកែប្រែ State ដោយផ្ទាល់ {#do-not-modify-state-directly}

For example, this will not re-render a component:

```js
// Wrong
this.state.comment = 'Hello';
```

Instead, use `setState()`:

```js
// Correct
this.setState({comment: 'Hello'});
```

The only place where you can assign `this.state` is the constructor.

### ការបន្ទាន់សម័យរបស់ State អាចជា Asynchronous {#state-updates-may-be-asynchronous}

React may batch multiple `setState()` calls into a single update for performance.

Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

For example, this code may fail to update the counter:

```js
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

To fix it, use a second form of `setState()` that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:

```js
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

We used an [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) above, but it also works with regular functions:

```js
// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### ការបន្ទាន់សម័យ State ត្រូវបានបញ្ចូលគ្នា {#state-updates-are-merged}

When you call `setState()`, React merges the object you provide into the current state.

For example, your state may contain several independent variables:

```js{4,5}
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
```

Then you can update them independently with separate `setState()` calls:

```js{4,10}
  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```

The merging is shallow, so `this.setState({comments})` leaves `this.state.posts` intact, but completely replaces `this.state.comments`.

## ទិន្នន័យ Flows Down {#the-data-flows-down}

Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn't care whether it is defined as a function or a class.

This is why state is often called local or encapsulated. It is not accessible to any component other than the one that owns and sets it.

A component may choose to pass its state down as props to its child components:

```js
<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
```

This also works for user-defined components:

```js
<FormattedDate date={this.state.date} />
```

The `FormattedDate` component would receive the `date` in its props and wouldn't know whether it came from the `Clock`'s state, from the `Clock`'s props, or was typed by hand:

```js
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/zKRqNB?editors=0010)

This is commonly called a "top-down" or "unidirectional" data flow. Any state is always owned by some specific component, and any data or UI derived from that state can only affect components "below" them in the tree.

If you imagine a component tree as a waterfall of props, each component's state is like an additional water source that joins it at an arbitrary point but also flows down.

To show that all components are truly isolated, we can create an `App` component that renders three `<Clock>`s:

```js{4-6}
function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/vXdGmd?editors=0010)

Each `Clock` sets up its own timer and updates independently.

In React apps, whether a component is stateful or stateless is considered an implementation detail of the component that may change over time. You can use stateless components inside stateful components, and vice versa.
