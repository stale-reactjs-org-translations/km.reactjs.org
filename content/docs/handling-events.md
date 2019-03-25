---
id: handling-events
title: Handling Events
permalink: docs/handling-events.html
prev: state-and-lifecycle.html
next: conditional-rendering.html
redirect_from:
  - "docs/events-ko-KR.html"
---

ការ Handle event ជាមួយReact elements គឺមានការស្រដៀងគ្នាទៅនឹងការ​Handle events ជាមួយ​DOM elemments ដែរ។ វាមានការខុសគ្នាមួយចំនួនដូចជា៖ 

* ឈ្មោះរបស់ events ក្នុងReact ត្រូវប្រើជាទម្រង់ camelCast ដោយមិនប្រើទម្រង់ lowercase ទេ។
* ក្នុង JSX អ្នកត្រូវ pass function ជា​ event handler ដោយគេមិនប្រើ​ String នោះទេ​។

ឧទាហរណ៍​ នៅក្នុង HTML៖

```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

មានភាពខុសគ្នាបន្តិចបន្តួចនៅក្នុង React:

```js{1}
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

ចំនុចដែលខុសគ្នាមួយទៀតគឺអ្នកមិនអាច return `false` ដើម្បីការពារ default behavior នៅក្នុង React បានឡើយ។ អ្នកត្រូវតែហៅ `preventDefault`។ ឧទាហរណ៍​ ជាទម្រង់ HTML ដើម្បីការពារ​ កុំអោយ browser បើកទំព័រថ្មីនៅពេលគេចុចលើ​​តំណភ្ជាប់ អ្នកអាចសរសេរដូចខាងក្រោម៖ 

```html
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```

នៅក្នុង React គួរតែត្រូវបានជំនួសដូចខាងក្រោម៖ 

```js{2-5,8}
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

`e`នៅត្រង់ចំនុចនេះគឺជា synthetic event។ React កំណត់​​ synthetic events ទាំងនោះអាស្រ័យទៅតាម​​ [W3C spec](https://www.w3.org/TR/DOM-Level-3-Events/)ដូចនេះអ្នកកុំបារម្ភពី cross-browser compatibility។ មើលឯកសារអំពី [`SyntheticEvent`](/docs/events.html) ដើម្បីរៀនបន្ថែមទៀត។

នៅពេលអ្នកប្រើ React អ្នកពុំគួរហៅ `addEventListener` ដើម្បី add listeners ទៅកាន់ DOM element បន្ទាប់ពេលវាត្រូវបានបង្តើត។ ជំនួសមកវិញ អ្នកគ្រាន់តែដាក់ listener នៅពេលដែល element render ដំបូង។

នៅពេលអ្នកបង្កើត component ដោយប្រើ [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)អ្នកអាចប្រើ event handler ជា method នៅក្នុង​ class។​​ ឧទាហរណ៍​៖ `Toggle` component​ នឹង renders button មួយដែលអនុញ្ញាតិអោយ user ប្តូរstatesពី "ON" ទៅ "OFF" :

```js{6,7,10-14,18}
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/xEmzGg?editors=0010)

You have to be careful about the meaning of `this` in JSX callbacks. In JavaScript, class methods are not [bound](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind) by default. If you forget to bind `this.handleClick` and pass it to `onClick`, `this` will be `undefined` when the function is actually called.

This is not React-specific behavior; it is a part of [how functions work in JavaScript](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/). Generally, if you refer to a method without `()` after it, such as `onClick={this.handleClick}`, you should bind that method.

If calling `bind` annoys you, there are two ways you can get around this. If you are using the experimental [public class fields syntax](https://babeljs.io/docs/plugins/transform-class-properties/), you can use class fields to correctly bind callbacks:

```js{2-6}
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

This syntax is enabled by default in [Create React App](https://github.com/facebookincubator/create-react-app).

If you aren't using class fields syntax, you can use an [arrow function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) in the callback:

```js{7-9}
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```

The problem with this syntax is that a different callback is created each time the `LoggingButton` renders. In most cases, this is fine. However, if this callback is passed as a prop to lower components, those components might do an extra re-rendering. We generally recommend binding in the constructor or using the class fields syntax, to avoid this sort of performance problem.

## Passing Arguments to Event Handlers {#passing-arguments-to-event-handlers}

Inside a loop it is common to want to pass an extra parameter to an event handler. For example, if `id` is the row ID, either of the following would work:

```js
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

The above two lines are equivalent, and use [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) and [`Function.prototype.bind`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) respectively.

In both cases, the `e` argument representing the React event will be passed as a second argument after the ID. With an arrow function, we have to pass it explicitly, but with `bind` any further arguments are automatically forwarded.
