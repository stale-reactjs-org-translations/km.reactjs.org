---
id: components-and-props
title: Components និង Props
permalink: docs/components-and-props.html
redirect_from:
  - "docs/reusable-components.html"
  - "docs/reusable-components-zh-CN.html"
  - "docs/transferring-props.html"
  - "docs/transferring-props-it-IT.html"
  - "docs/transferring-props-ja-JP.html"
  - "docs/transferring-props-ko-KR.html"
  - "docs/transferring-props-zh-CN.html"
  - "tips/props-in-getInitialState-as-anti-pattern.html"
  - "tips/communicate-between-components.html"
prev: rendering-elements.html
next: state-and-lifecycle.html
---

Componentsអនុញ្ញាតឱ្យអ្នកបំបែក UI ទៅជាបំណែកឯករាជ្យ ដែលអាចប្រើឡើងវិញបាន ហើយគិតអំពីបំណែកនីមួយៗនៅក្នុងភាពឯកោ(isolation)។ ទំព័រនេះផ្តល់ការណែនាំអំពីគំនិតនៃcomponents. អ្នកអាចរក [លំអិត component API លំអិតនៅទីនេះ](/docs/react-component.html).

គំនិត, components គឺដូចមុខងារ JavaScript. ពួកគេទទួលយកធាតុចូល (ហៅថា "props") ហើយត្រឡប់ធាតុ React ពិពណ៌នាអំពីអ្វីដែលគួរលេចឡើងនៅលើអេក្រង់។

## Function និង Class Components {#function-and-class-components}

វិធីសាមញ្ញបំផុតដើម្បីកំណត់ component គឺត្រូវសរសេរមុខងារ JavaScript:

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

មុខងារនេះគឺជា React component ត្រឹមត្រូវ ដោយសារតែវាទទួលយក "props" តែមួយ(ដែលតំណាងឱ្យអចលនទ្រព្យ) objectជាមួយទិន្នន័យនិងត្រឡប់ធាតុReact ។ យើងហៅcomponentsដូចជា "function components" ដោយសារតែពួកគេគឺជាមុខងារព្យញ្ជនៈ JavaScript ។
អ្នកក៏អាចប្រើ[ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) ដើម្បីកំណត់component:

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

componentsខាងលើនេះគឺសមមូលនឹងចំនុច React ។

Classesមានលក្ខណៈពិសេសបន្ថែមមួយចំនួនដែលយើងនឹងពិភាក្សានៅក្នុង[ផ្នែកបន្ទាប់](/docs/state-and-lifecycle.html). រហូតមកដល់ពេលនេះយើងនឹងប្រើមុខងារ components សម្រាប់ភាពស៊ីជំរៅរបស់វា។

## ការបង្កើតComponent {#rendering-a-component}

កាលពីមុនយើងទើបតែជួបReactធាតុដែលតំណាងឱ្យស្លាក(tags) DOM:

```js
const element = <div />;
```

ទោះយ៉ាងណាធាតុក៏អាចតំណាងឱ្យcomponentsដែលកំណត់ដោយអ្នកប្រើ:

```js
const element = <Welcome name="Sara" />;
```

នៅពេលដែលមាន React មឃើញធាតុតំណាងឱ្យcomponentកំណត់ដោយអ្នកប្រើ, វាបញ្ជូនគុណលក្ខណៈ JSX ទៅcomponentនេះជាវត្ថុតែមួយ. យើងហៅវត្ថុនេះថា "props" ។

ឧទាហរណ៏, កូដនេះធ្វើការមំលែងទៅជា "Hello, Sara" នៅលើទំព័រ:

```js{1,5}
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[សាកល្បងនៅលើ CodePen](codepen://components-and-props/rendering-a-component)

ចូរយើងសង្ខេបនូវអ្វីដែលកើតឡើងនៅក្នុងឧទាហរណ៍នេះ:

1. យើង​ហៅ `ReactDOM.render()` ជាមួយនឹង `<Welcome name="Sara" />` ធាតុ។
2. React ហៅ `Welcome` component ជាមួយ `{name: 'Sara'}` ជា props។
3. `Welcome` component របស់យើង ត្រឡប់ជាមួយ `<h1>Hello, Sara</h1>` ជាលទ្ធផល។
4. React DOM ធ្វើឱ្យទាន់សម័យមានប្រសិទ្ធិភាព DOM ដើម្បីផ្គូផ្គង `<h1>Hello, Sara</h1>`.

>**ចំណាំ:** តែងតែចាប់ផ្ដើមឈ្មោះ component ជាមួយអក្សរធំ។
>
>Reactទាក់ទងនឹងcomponentsដែលចាប់ផ្ដើមដោយអក្សរតូចជាស្លាក DOM។ ឧទាហរណ៍ `<div />` តំណាងឱ្យស្លាក HTML div ប៉ុន្តែ `<Welcome />` តំណាងឱ្យcomponentនិងតម្រូវ `Welcome` នៅក្នុង scope។
>
>ដើម្បីរៀនថែមទៀតអំពីហេតុផលដែលនៅពីក្រោយអនុសញ្ញានេះ, សូម​អាន [JSX In Depth](/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized).

## Composing Components {#composing-components}

Components can refer to other components in their output. This lets us use the same component abstraction for any level of detail. A button, a form, a dialog, a screen: in React apps, all those are commonly expressed as components.

For example, we can create an `App` component that renders `Welcome` many times:

```js{8-10}
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

[សាកល្បងនៅលើ CodePen](codepen://components-and-props/composing-components)

Typically, new React apps have a single `App` component at the very top. However, if you integrate React into an existing app, you might start bottom-up with a small component like `Button` and gradually work your way to the top of the view hierarchy.

## Extracting Components {#extracting-components}

Don't be afraid to split components into smaller components.

For example, consider this `Comment` component:

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

[សាកល្បងនៅលើ CodePen](codepen://components-and-props/extracting-components)

It accepts `author` (an object), `text` (a string), and `date` (a date) as props, and describes a comment on a social media website.

This component can be tricky to change because of all the nesting, and it is also hard to reuse individual parts of it. Let's extract a few components from it.

First, we will extract `Avatar`:

```js{3-6}
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

The `Avatar` doesn't need to know that it is being rendered inside a `Comment`. This is why we have given its prop a more generic name: `user` rather than `author`.

We recommend naming props from the component's own point of view rather than the context in which it is being used.

We can now simplify `Comment` a tiny bit:

```js{5}
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

Next, we will extract a `UserInfo` component that renders an `Avatar` next to the user's name:

```js{3-8}
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

This lets us simplify `Comment` even further:

```js{4}
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

[សាកល្បងនៅលើ CodePen](codepen://components-and-props/extracting-components-continued)

Extracting components might seem like grunt work at first, but having a palette of reusable components pays off in larger apps. A good rule of thumb is that if a part of your UI is used several times (`Button`, `Panel`, `Avatar`), or is complex enough on its own (`App`, `FeedStory`, `Comment`), it is a good candidate to be a reusable component.

## Props គឺមិនអាចកែសម្រួល {#props-are-read-only}

Whether you declare a component [as a function or a class](#function-and-class-components), it must never modify its own props. Consider this `sum` function:

```js
function sum(a, b) {
  return a + b;
}
```

Such functions are called ["pure"](https://en.wikipedia.org/wiki/Pure_function) because they do not attempt to change their inputs, and always return the same result for the same inputs.

In contrast, this function is impure because it changes its own input:

```js
function withdraw(account, amount) {
  account.total -= amount;
}
```

React is pretty flexible but it has a single strict rule:

**All React components must act like pure functions with respect to their props.**

Of course, application UIs are dynamic and change over time. In the [next section](/docs/state-and-lifecycle.html), we will introduce a new concept of "state". State allows React components to change their output over time in response to user actions, network responses, and anything else, without violating this rule.
