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

const root = ReactDOM.createRoot(document.getElementById('root')); 
// Try changing to isLoggedIn={true}:
root.render(<Greeting isLoggedIn={false} />);
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

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render(<LoginControl />);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/QKzAgB?editors=0010)

ខណៈពេលកំពុងប្រកាស variable មួយ ការប្រើ `if` statement គឺជាវិធីដ៏ល្អដើម្បីដាក់លក្ខខណ្ឌក្នុងការ​ render component មួយ 
ហើយពេលខ្លះអ្នកប្រហែលជាចង់ប្រើ​ syntax ដែលសរសេរខ្លីជាងនេះ។ មានវិធីមួយចំនួនក្នុងការដាក់លក្ខខណ្ឌលក្ខណះ inline (inline conditions) ក្នុង JSX ហើយត្រូវបានពន្យល់ដូចខាងក្រោម។

### Inline If ជាមួយ  Logical && Operator {#inline-if-with-logical--operator}

<<<<<<< HEAD
អ្នកប្រហែល [បង្កប់ (embed) expressions មួយចំនួននៅក្នុង JSX](/docs/introducing-jsx.html#embedding-expressions-in-jsx) ដោយការដាក់រុំពួកវានៅក្នុងដង្កៀប​អង្កាញ់ (curly braces)។ នេះរួមបញ្ចូលទាំង JavaScript logical `&&` operator។ វាអាចងាយស្រួលសម្រាប់ការដាក់លក្ខខណ្ឌរួមជាមួយ element មួយ៖
=======
You may [embed expressions in JSX](/docs/introducing-jsx.html#embedding-expressions-in-jsx) by wrapping them in curly braces. This includes the JavaScript logical `&&` operator. It can be handy for conditionally including an element:
>>>>>>> 4808a469fa782cead9802619b0341b27b342e2d3

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

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render(<Mailbox unreadMessages={messages} />);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/ozJddz?editors=0010)

វាដំណើរការដោយសារតែ JavaScript `true & expression` តែងតែវាយតម្លៃទៅជា `expression` និង `false && expression` តែងតែវាយតម្លៃទៅជា `false`។

ដូច្នេះប្រសិនបើលក្ខខណ្ឌគឺ `true` នេាះ element នៅខាងស្តាំបន្ទាប់ពី `&&` 
នឹងបង្ហាញនៅក្នុងលទ្ធផល (output)។ ប្រសិនបើវាគឺ `false` នេាះ React នឹងមិនអើពើ (ignore) ហើយរំលងវា។

<<<<<<< HEAD
### Inline If-Else ជាមួយ  Conditional Operator {#inline-if-else-with-conditional-operator}
=======
Note that returning a falsy expression will still cause the element after `&&` to be skipped but will return the falsy expression. In the example below, `<div>0</div>` will be returned by the render method.

```javascript{2,5}
render() {
  const count = 0;
  return (
    <div>
      {count && <h1>Messages: {count}</h1>}
    </div>
  );
}
```

### Inline If-Else with Conditional Operator {#inline-if-else-with-conditional-operator}
>>>>>>> 4808a469fa782cead9802619b0341b27b342e2d3

Method ផ្សេងទៀតសម្រាប់ដាក់លក្ខខណ្ឌក្នុងការ render elements ជាលក្ខណះ inline គឺប្រើ JavaScript conditional operator [`condition ? true : false`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)។

នៅក្នុងឧទាហរណ៍ខាងក្រោម យើងប្រើវាដើម្បីដាក់លក្ខខណ្ឌក្នុងការ render នូវ small block មួយរបស់ text។

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

វាក៏អាចត្រូវបានប្រើសម្រាប់ expressions ធំជាងនេះ បើទោះបីជាវាមិនសូវច្បាស់ពីអ្វីដែលនឹងកើតឡើង៖

```js{5,7,9}
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn
        ? <LogoutButton onClick={this.handleLogoutClick} />
        : <LoginButton onClick={this.handleLoginClick} />
      }
    </div>
  );
}
```

ដូចនៅក្នុង JavaScrip វាអាស្រ័យទៅលើអ្នកក្នុងការជ្រើសរើស style ដែលសមរម្យមួយដោយផ្អែកលើអ្វីដែលអ្នកនិងក្រុមរបស់អ្នកពិចារណាថាកូដគឺ more readable។ ចងចាំផងដែរថានៅពេលណាដែលលក្ខខណ្ឌប្រែជាស្មុគស្មាញ វាអាចជាពេលវេលាដ៏ល្អមួយដើម្បី [extract a component](/docs/components-and-props.html#extracting-components)។

### បង្ការ Component ពីការ Render {#preventing-component-from-rendering}

ក្នុងករណីកម្រអ្នកប្រហែលជាចង់អោយ​ component មួយ លាក់ខ្លួនវា (hide itself) ទោះបីជាវាត្រូវបាន render ដោយ component ផ្សេង។ ដើម្បីធ្វើដូចនេះអ្នកត្រូវ return `null` ជំនួសអោយលទ្ធផល (output) render របស់វា។

នៅក្នុងឧទាហរណ៍ខាងក្រោម `<WarningBanner />` ត្រូវបាន render ដោយអាស្រ័យ​លើតម្លៃរបស់ props ដែលត្រូវបានហៅថា `warn`។ ប្រសិនបើតម្លៃរបស់ props គឺ `false` អញ្ជឹង component នឹងមិន render។

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

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render(<Page />);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/Xjoqwm?editors=0010)

ការ return `null` ពី `render` method របស់ component មួយមិនប៉ះពាល់ដល់ការ firing នៃ lifecycle methods របស់ component ទេ។ ឧទាហរណ៍ `componentDidUpdate` នឹងនៅតែត្រូវបាន call។
