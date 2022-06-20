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

<<<<<<< HEAD
សូមពិចារណាគំរូនាឡិកាពី [ផ្នែកមួយនៃផ្នែកមុន](/docs/rendering-elements.html#updating-the-rendered-element). នៅក្នុង [ការបង្ហាញធាតុ](/docs/rendering-elements.html#rendering-an-element-into-the-dom),យើងទើបតែរៀនវិធីដើម្បីធ្វើបច្ចុប្បន្នភាព UI តែមួយប៉ុណ្ណោះ. យើង​ហៅ `ReactDOM.render()` ដើម្បីផ្លាស់ប្តូរលទ្ធផលបង្ហាញ:
=======
Consider the ticking clock example from [one of the previous sections](/docs/rendering-elements.html#updating-the-rendered-element). In [Rendering Elements](/docs/rendering-elements.html#rendering-an-element-into-the-dom), we have only learned one way to update the UI. We call `root.render()` to change the rendered output:
>>>>>>> df2673d1b6ec0cc6657fd58690bbf30fa1e6e0e6

```js{10}
const root = ReactDOM.createRoot(document.getElementById('root'));
  
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/gwoJZk?editors=0010)

នៅក្នុងផ្នែកនេះ យើងនឹងរៀនពីរបៀបបង្កើត component `Clock` ដែលអាចប្រើឡើងវិញបាន និង encapsulated. វានឹងបង្កើតកម្មវិធីកំណត់ពេលវេលាផ្ទាល់ខ្លួនរបស់វាហើយធ្វើបច្ចុប្បន្នភាពរៀងរាល់វិនាទី។

យើងអាចចាប់ផ្ដើមដោយ encapsulating របៀបមើលនាឡិកា:

```js{5-8,13}
const root = ReactDOM.createRoot(document.getElementById('root'));

function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  root.render(<Clock date={new Date()} />);
}

setInterval(tick, 1000);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/dpdoYR?editors=0010)

ទោះយ៉ាងណា, វានឹកនូវតម្រូវការដ៏សំខាន់មួយ:ការពិតដែលថា `Clock` កំណត់កម្មវិធីកំណត់ពេលវេលាមួយនិងធ្វើបច្ចុប្បន្នភាព UI ជារៀងរាល់វិនាទីគួរតែជាការអនុវត្ដន៍លម្អិតនៃ `Clock`.

ជាគំនិត យើងចង់សរសេរវាម្តងនិងមានការធ្វើឱ្យទាន់សម័យ 'Clock' ខ្លួនវាផ្ទាល់:

```js{2}
root.render(<Clock />);
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
root.render(<Clock />);
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

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
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

ចំណាំ របៀបដែលយើងរក្សាទុក timer ID អោយបានត្រឹមត្រូវលើ `this` (`this.timerID`)។

ខណៈពេល `this.props` ត្រូវបានបង្កើតឡើងដោយ React ខ្លួនឯង និង `this.state` មានអត្ថន័យពិសេស, អ្នកមានសិទ្ធិបន្ថែម fields ទៅ class ដោយខ្លួនឯង ប្រសិនបើអ្នកត្រូវការរក្សាទុកអ្វីមួយដែលមិនចូលរួមនៅក្នុង data flow (ដូចជា timer ID).

យើងនឹងលុបចេញនូវកម្មវិធីកំណត់ម៉ោងក្នុង `componentWillUnmount()` lifecycle method:

```js{2}
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

ទីបំផុត យើងនឹងអនុវត្តវិធីសាស្ត្រមួយដែលហៅថា `tick()` ដែលថា `Clock` component នឹងដំណើរការរាល់វិនាទី។

វានឹងប្រើ `this.setState()` ដើម្បីកំណត់ពេលធ្វើឱ្យទាន់សម័យទៅ component local state៖

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

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/amqdNA?editors=0010)

ឥឡូវនេះនាឡិកាដំណើរការរាល់វិនាទី។

តោះសង្ខេបឡើងវិញ អ្វីដែលកើតឡើងនិងលំដាប់ដែលវិធីសាស្រ្តត្រូវបានគេហៅថា:

<<<<<<< HEAD
1) ពេលណា​ `<Clock />` ត្រូវបានបញ្ជូនទៅ `ReactDOM.render()`, React ហៅ constructor នៃ `Clock` component. ចាប់តាំងពី `Clock` ត្រូវការបង្ហាញពេលវេលាបច្ចុប្បន្ន, វាចាប់ផ្ដើម `this.state` ជាមួយ object រួមទាំងពេលបច្ចុប្បន្ន។ ក្រោយមកយើងនឹងធ្វើបច្ចុប្បន្នភាព state។
=======
1) When `<Clock />` is passed to `root.render()`, React calls the constructor of the `Clock` component. Since `Clock` needs to display the current time, it initializes `this.state` with an object including the current time. We will later update this state.
>>>>>>> df2673d1b6ec0cc6657fd58690bbf30fa1e6e0e6

2) React បន្ទាប់មកហៅ `Clock` component's `render()` method. នេះ​គឺជា​របៀបដែល React រៀនអ្វីដែលគួរត្រូវបានបង្ហាញនៅលើអេក្រង់។ React បន្ទាប់មកធ្វើឱ្យទាន់សម័យ DOM ដើម្បីផ្គូផ្គងទៅការបង្ហាញរបស់ `Clock`។

3) នៅពេល​ដែល `Clock` លទ្ធផលត្រូវបានបញ្ចូលក្នុង DOM, React ហៅទៅ `componentDidMount()` lifecycle method. នៅខាងក្នុង, `Clock` សួរកម្មវិធីរុករកដើម្បីបង្កើតកម្មវិធីកំណត់ពេលវេលា ដែលអាចធ្វើការហៅទៅ `tick()` method ម្តងក្នុងមួយវិនាទី។

4) រៀងរាល់វិនាទី កម្មវិធីរុករក ធ្វើការហៅទៅកាន់ `tick()` method. នៅខាងក្នុង, the `Clock` component កំណត់ពេលវេលាធ្វើបច្ចុប្បន្នភាព UI តាមការហៅ `setState()` ជាមួយ object ដែលមានពេលបច្ចុប្បន្ន. សូមអរគុណដល់ការហៅទៅកាន់ `setState()`, React ដឹងថា state បានផ្លាស់ប្តូរ, ហើយធ្វើការហៅទៅកាន់ `render()` method ជាថ្មីម្តងទៀតដើម្បសិក្សាថាអ្វីដែលគួរនៅលើអេក្រង់. ពេលនេះ, `this.state.date` ក្នុង `render()` method នឹងខុសគ្នា, ដូច្នេះការបង្ហាញទិន្នផលនឹងរួមបញ្ចូលពេលវេលាដែលបានធ្វើឱ្យទាន់សម័យ។ React ធ្វើបច្ចុប្បន្នភាពតាម DOM។

5) ប្រសិនបើ `Clock` component ត្រូវបានយកចេញពី DOM, React ហៅទៅកាន់ `componentWillUnmount()` lifecycle method ដូច្នេះកម្មវិធីកំណត់ពេលវេលាត្រូវបានបញ្ឈប់។

## ការប្រើប្រាស់ State ឲបានត្រឹមត្រូវ {#using-state-correctly}

មានរឿងបីដែលអ្នកគួរដឹងពី `setState()`.

### កុំកែប្រែ State ដោយផ្ទាល់ {#do-not-modify-state-directly}

ឧទាហរណ៍, នេះនឹងមិន re-render a component:

```js
// Wrong
this.state.comment = 'Hello';
```

ជំនួសដោយ, ការប្រើ `setState()`:

```js
// Correct
this.setState({comment: 'Hello'});
```

ជាកន្លែងតែមួយគត់ដែលអ្នកអាចចាត់តាំង(assign) `this.state` គឺជា constructor.

### ការបន្ទាន់សម័យរបស់ State អាចជា Asynchronous {#state-updates-may-be-asynchronous}

React អាចមានច្រើន batch `setState()` ហៅចូលទៅក្នុងការធ្វើបច្ចុប្បន្នភាពតែមួយសម្រាប់ performance។

ពីព្រោះ `this.props` និង `this.state` អាចត្រូវបានធ្វើបច្ចុប្បន្នភាព asynchronously,អ្នកមិនគួរពឹងផ្អែកលើតម្លៃរបស់វាសម្រាប់ការគណនាបន្ទាប់ពី state នោះទេ។

ឧទាហរណ៍, code នេះ អាចបរាជ័យក្នុងការធ្វើបច្ចុប្បន្នភាពនៃ counter:

```js
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

ដើម្បីធ្វើការកែតម្រូវ, ប្រើសំណុំបែបបទទីពីរនៃ `setState()` ដែលទទួលយក function ជាជាងមួយ object. function នោះ នឹងទទួលបាន state ពីមុនជាតម្លៃដំបូង និង props នៅពេលដែលការ update ត្រូវបានអនុវត្តជាតម្លៃបន្ទាប់:

```js
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

យើង​បានប្រើ [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) ខាងលើ, ប៉ុន្តែវាក៏ធ្វើការជាមួយ regular functions ផងដែរ:

```js
// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### ការបន្ទាន់សម័យ State ត្រូវបានបញ្ចូលគ្នា {#state-updates-are-merged}

នៅពេលអ្នកហៅ `setState()`, React ធ្វើការបញ្ចូល object ដែលអ្នកបានផ្តល់ជូននៅក្នុង state បច្ចុប្បន្ន។

ឧទាហរណ៍, state របស់អ្នក អាចមានអថេរ(variables) ឯករាជ្យជាច្រើន:

```js{4,5}
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
```

បន្ទាប់មកអ្នកអាចធ្វើការ update ពួកវាដាច់ដោយឡែកពីគ្នា `setState()` ដោយការហៅ:

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

ការរួមបញ្ចូលគ្នាគឺ shallow, ដូច្នេះ `this.setState({comments})` leaves `this.state.posts` intact, ប៉ុន្តែជំនួសទាំងស្រុងដោយ `this.state.comments`.

## ទិន្នន័យ Flows Down {#the-data-flows-down}

ទាំងparentនិង child components មិនអាចដឹងថាវាមាន component ជាក់លាក់មួយគឺ stateful or stateless, ហើយពួកគេមិនគួរខ្វល់ថា តើវាត្រូវបានគេកំណត់ថាជា function ឬ a class នោះទេ.

នេះ​ជាមូលហេតុដែល state គឺជាញឹកញាប់ហៅ local ឬ encapsulated។ វាមិនអាចប្រើបាន វាមិនអាចចូលទៅដល់ component ណាមួយក្រៅពី object ដែលមាននិងកំណត់ដោយខ្លួនវាទេ។

Component អាចជ្រើសរើសដើម្បី pass state down ដូច props ទៅ child components:

```js
<<<<<<< HEAD
<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
```

នេះក៏ដំណើរការសម្រាប់ user-defined components:

```js
=======
>>>>>>> df2673d1b6ec0cc6657fd58690bbf30fa1e6e0e6
<FormattedDate date={this.state.date} />
```

`FormattedDate` component នឹងទទួលបាន `date` នៅក្នុង props របស់ខ្លួន ហើយនឹងមិនដឹងថាតើវាមកពី `Clock`state ណាមួយនោះទេ, ពី `Clock` props, ឬត្រូវបានវាយដោយដៃ:

```js
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/zKRqNB?editors=0010)

នេះត្រូវបានគេហៅជាទូទៅថា "top-down" ឬ "unidirectional" data flow. ណាមួយ state គឺតែងតែជាកម្មសិទ្ធិរបស់ជាក់លាក់របស់ component, និងណាមួយ data ឬ UI derived ពី state នោះ អាចប៉ះពាល់តែ components "below" វាតែប៉ុណ្ណោះនៅក្នុង tree.

ប្រសិនបើអ្នកស្រមៃថា component tree ដូចជា waterfall នៃ props, គ្រប់ component's state គឺដូចជាប្រភពទឹកបន្ថែម ដែលចូលរួមជាមួយវានៅចំណុចមួយដែលបំពានប៉ុន្តែវាហូរចុះក្រោមផងដែរ.

ដើម្បីបង្ហាញថា components ទាំងអស់ ពិតជា isolated, យើងអាចបង្កើត `App` component ដែល renders `<Clock>` បីដង:

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
```

[**សាកល្បងនៅលើ CodePen**](https://codepen.io/gaearon/pen/vXdGmd?editors=0010)

`Clock` មួយៗបង្កើត Timer ផ្ទាល់ខ្លួនវាហើយធ្វើបច្ចុប្បន្នភាពដោយឯករាជ្យ។

នៅក្នុងកម្មវិធី React, ថាតើ component គឺ stateful ឬ stateless គឺ ចាត់ទុកថាជាការអនុវត្ដន៍លម្អិតនៃទី component ដែលអាចផ្លាស់ប្តូរតាមពេលវេលា. លោក​អ្នក​អាច​ប្រើប្រាស់ stateless components នៅក្នុង stateful components, និងផ្ទុយមកវិញ។
