---
id: conditional-rendering
title: Conditional Rendering
permalink: docs/conditional-rendering.html
prev: handling-events.html
next: lists-and-keys.html
redirect_from:
  - "tips/false-in-jsx.html"
---

នៅក្នុង React អ្នកអាចបង្កើត components ខុសៗគ្នាដែល encapsulate ឥរិយាបទ (behavior) ដែលអ្នកត្រូវការ។ បន្ទាប់មកទៀតអ្នកអាច render ពួកវាមួយចំនួនប៉ុណ្ណោះ ដោយអាស្រ័យលើ state នៃ application របស់អ្នក។​

Conditional rendering នៅក្នុង React ធ្វើការដូចគ្នា និង conditions នៅក្នុង JavaScript។ ប្រើ JavaScript operators ដូចជា [`if`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) ឬក៏ [conditional operator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) ដើម្បីបង្កើត elements ដែលតំណាងអោយ current state ហើយអនុញ្ញាតឱ្យ React ធ្វើបច្ចុប្បន្នភាព UI ដែលត្រូវនិង conditions។

ពិចារណា components ទាំងពីរនេះ៖

```js
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
```

យើងនឹងបង្កើត `Greeting` component ដែលបង្ហាញ (displays) components ទាំងនេះដោយអាស្រ័យលើថាអ្នកប្រើប្រាស់បាន logged in ឬក៏អត់៖

```javascript{3-7,11,12}
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/ZpVxNq?editors=0011)

ឧទាហរណ៍នេះ renders greeting ខុសគ្នាដោយអាស្រ័យលើតម្លៃនៃ `isLoggedIn` prop។

### Element Variables {#element-variables}

អ្នកអាចប្រើ variables ដើម្បី​រក្សាទុក elements។ នេះអាចជួយអ្នកក្នុងការដាក់លក្ខខណ្ឌ render ផ្នែក​មួយ​នៃ component ខណៈពេលដែលលទ្ធផល (output) មិនផ្លាស់ប្តូរទេ។

សូមពិចារណាពី components ពីរនេះដែលតំណាងអោយ Logout និង Login 
ប៊ូតុង៖

```js
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}
```

នៅក្នុងឧទាហរណ៍ខាងក្រោម យើងនឹងបង្កើត [stateful component](/docs/state-and-lifecycle.html#adding-local-state-to-a-class) មួយដែលត្រូវបានហៅថា `LoginControl`។

វានឹង render ទាំង `<LoginButton />` ឬក៏ `<LogoutButton />` ដោយអាស្រ័យលើ current state របស់វា។ វានឹង render `<Greeting />` ផងដែរ ដែលតពីឧទាហរណ៍មុន៖

```javascript{20-25,29,30}
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/QKzAgB?editors=0010)

ខណៈពេលកំពុងប្រកាស variable មួយ ការប្រើ `if` statement គឺជាវិធីដ៏ល្អដើម្បីដាក់លក្ខខណ្ឌក្នុងការ​ render component មួយ 
ហើយពេលខ្លះអ្នកប្រហែលជាចង់ប្រើ​ syntax ដែលសរសេរខ្លីជាងនេះ។ មានវិធីមួយចំនួនក្នុងការដាក់លក្ខខណ្ឌលក្ខណះ inline (inline conditions) ក្នុង JSX ហើយត្រូវបានពន្យល់ដូចខាងក្រោម។

### Inline If with Logical && Operator {#inline-if-with-logical--operator}

You may [embed any expressions in JSX](/docs/introducing-jsx.html#embedding-expressions-in-jsx) by wrapping them in curly braces. This includes the JavaScript logical `&&` operator. It can be handy for conditionally including an element:

```js{6-10}
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/ozJddz?editors=0010)

It works because in JavaScript, `true && expression` always evaluates to `expression`, and `false && expression` always evaluates to `false`.

Therefore, if the condition is `true`, the element right after `&&` will appear in the output. If it is `false`, React will ignore and skip it.

### Inline If-Else with Conditional Operator {#inline-if-else-with-conditional-operator}

Another method for conditionally rendering elements inline is to use the JavaScript conditional operator [`condition ? true : false`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator).

In the example below, we use it to conditionally render a small block of text.

```javascript{5}
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```

It can also be used for larger expressions although it is less obvious what's going on:

```js{5,7,9}
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

Just like in JavaScript, it is up to you to choose an appropriate style based on what you and your team consider more readable. Also remember that whenever conditions become too complex, it might be a good time to [extract a component](/docs/components-and-props.html#extracting-components).

### Preventing Component from Rendering {#preventing-component-from-rendering}

In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return `null` instead of its render output.

In the example below, the `<WarningBanner />` is rendered depending on the value of the prop called `warn`. If the value of the prop is `false`, then the component does not render:

```javascript{2-4,29}
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(state => ({
      showWarning: !state.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/Xjoqwm?editors=0010)

Returning `null` from a component's `render` method does not affect the firing of the component's lifecycle methods. For instance `componentDidUpdate` will still be called.
