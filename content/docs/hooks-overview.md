---
id: hooks-overview
title: Hooks at a Glance
permalink: docs/hooks-overview.html
next: hooks-state.html
prev: hooks-intro.html
---

*Hooks* គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។

Hooks គឺជា [backwards-compatible](/docs/hooks-intro.html#no-breaking-changes)។ ទំព័រនេះផ្តល់នូវទិដ្ឋភាពទូទៅ (overview) នៃ Hooks សម្រាប់អ្នកប្រើប្រាស់ដែលមានបទពិសោធន៍លើ React។ នេះគឺជាការ overview ខ្លីៗ។ ប្រសិនបើអ្នកច្រឡំ, សូមមើលប្រអប់ពណ៌លឿងខាងក្រោម៖

>ការពន្យល់យ៉ាងលម្អិត
>
>សូមអាន [Motivation](/docs/hooks-intro.html#motivation) ដើម្បីរៀនពីមូលហេតុដែលយើងណែនាំ Hooks។

**↑↑↑ ផ្នែកនីមួយៗបញ្ចប់ដោយប្រអប់ពណ៌លឿងដូចនេះ។** ពួកវាភ្ជាប់ទៅនឹងការពន្យល់លម្អិត។

## 📌 State Hook {#state-hook}

ឧទាហរណ៍នេះ renders នូវ counter។ នៅពេលដែលអ្នកចុចលើ​ប៊ូតុង, វាបង្កើនតម្លៃ៖

```js{1,4,5}
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

នេះ, `useState` គឺជា *Hook* មួយ (យើងនឹងនិយាយអំពីវាថាតើវាមានន័យដូចម៉្តេចក្នុងពេលបន្តិចទៀតនេះ)។ យើង call វានៅខាងក្នុង function component ដើម្បីបន្ថែម local state មួយចំនួន។ React នឹងការពារ state នេះរវាង re-renders។ `useState` returns នូវ pair ដូចនេះ៖ តម្លៃរបស់ *current* state និង function ដែលអនុញ្ញាតឱ្យអ្នក update វា។ អ្នកអាច call function នេះពី event handler ឬក៏អ្វីផ្សេងទៀត។ វាស្រដៀងនឹង `this.setState` នៅក្នុង class, 
លើកលែងវា កុំបញ្ចូលចូលគ្នារវាង state ចាស់និង state ថ្មីជាមួយគ្នា។ (យើងនឹងបង្ហាញឧទាហរណ៍ប្រៀបធៀបមួយនៃការប្រើ `useState` ជំនួសអោយ `this.state` នៅក្នុង [ការប្រើប្រាស់ State Hook](/docs/hooks-state.html)។)

`useState` មាន argument តែមួយគត់គឺ initial state។ ក្នុងឧទាហរណ៍ខាងលើ, វាគឺ `0` ពីព្រេាះ counter របស់យើងចាប់ផ្តើមពីសូន្យ។ ចំណាំថា វាមិនដូច `this.state` នេាះទេ, state នៅទីនេះវាមិនត្រូវតែជា object នេាះទេ -- វាអាចជាអ្វីផ្សេងៗប្រសិនបើអ្នកចង់។ initial state argument គឺត្រូវបានគេប្រើតែកំឡុងពេល render តំបូងតែប៉ុណ្ណោះ។

#### Declaring multiple state variables {#declaring-multiple-state-variables}

អ្នកអាចប្រើ State Hook ច្រើនជាងមួយក្នុង component មួយ៖

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

The [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring) syntax អនុញ្ញាតឱ្យយើងដាក់ឈ្មេាះផ្សេងៗឱ្យ state variables យើងបានប្រកាសដោយការ call `useState`។ រាល់ការ rende ទាំងនេាះ។ យើងនឹងត្រលប់ទៅមើល មូលហេតុដែលវាដំណើរការ ហើយនិងនៅពេលដែលវាប្រយោជន៍នៅពេលក្រោយ។

#### But what is a Hook? {#but-what-is-a-hook}

Hooks គឺជា functions ដែលអនុញ្ញាតឱ្យអ្នក​ “hook into” React state និង lifecycle features ពី function components។ Hooks អត់ដំណើរនៅក្នុង classes ទេ -- ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ React ដោយមិនមាន classes។ (យើង [មិនណែនាំ](/docs/hooks-intro.html#gradual-adoption-strategy) ឱ្យសរសេរឡើងវិញនូវ components របស់អ្នកនេាះទេ ប៉ុន្តែអ្នកអាចចាប់ផ្តើមការប្រើ Hooks នៅក្នុង components ថ្មីប្រសិនបើអ្នកចង់។)

React ផ្តល់នូវ built-in Hooks មួយចំនួនដូចជា `useState`។ អ្នកក៏អាចបង្កើត Hooks ផ្ទាល់ខ្លួនរបស់អ្នកដើម្បីកាត់បន្ថយលក្ខណះ stateful រវាង components ផ្សេងៗគ្នា។ យើងនឹងក្រឡេកទៅមើល built-in Hooks មុនគេ។

>ការពន្យល់យ៉ាងលម្អិត
>
>អ្នកអាចរៀនបន្ថែមពី State Hook លើទំព័រផ្សេង៖ [ការប្រើ State Hook](/docs/hooks-state.html)។

## ⚡️ Effect Hook {#effect-hook}

អ្នកទំនងជាចូលចិត្តអនុវត្ត data fetching, subscriptions, ឬក៏ផ្លាស់ប្តូរ DOM ដោយផ្ទាល់ពី React components ពីមុន។ យើងហៅប្រតិបត្តិការទាំងនេះថា "side effects" (ឬ "effects" for short) ពីព្រេាះពួកវាអាចធ្វើអោយប៉ះពាល់ components ផ្សេងៗហើយនិងមិនអាច done កំឡុងពេល rendering។

Effect Hook, `useEffect`, បន្ថែមសមត្ថភាពក្នុងការអនុវត្ត side effects ពី function component។ វាបម្រើគោលបំណងដូចគ្នានឹង `componentDidMount`, `componentDidUpdate`, និង `componentWillUnmount` ក្នុង React classes។ ប៉ុន្តែបានបង្រួបបង្រួមចូលទៅក្នុង API តែមួយ។ (យើងនឹងបង្ហាញឧទាហរណ៍ប្រៀបធៀបរវាង `useEffect` ទៅនឹង methods ទាំងនេាះក្នុង [Using the Effect Hook](/docs/hooks-effect.html)។)

ឧទាហរណ៍, component នេះ sets នូវ document title បន្ទាប់ពី React ធ្វើបច្ចុប្បន្នភាព DOM៖

```js{1,6-10}
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

នៅពេលដែលអ្នក call `useEffect`, អ្នកកំពុងតែប្រាប់ React អោយ run "effect" function របស់អ្នកបន្ទាប់ពីការផ្លាស់ប្តូរចំពេាះ DOM។ Effect ត្រូវបានប្រកាស (declare) ខាងក្នុង component ដូច្នេះពួកវាមានសិទ្ធិចូលដំណើរការ props និង state របស់ពួកវា។ តាម​លំនាំដើម (by default), React runs effects បន្ទាប់ពី រាល់ពេល render -- *រួមទាំង* ពេល render តំបូង។ (
យើងនឹងនិយាយបន្ថែមទៀតអំពីរបៀបធៀបវាទៅនឹង class lifecycles នៅក្នុង [ការប្រើ Effect Hook](/docs/hooks-effect.html)។)

Effects ប្រហែលអាចជារបៀបដើម្បី "clean up" ដោយការ return ពី function។ ឧទាហរណ៍, component នេះប្រើ effect ដើម្បី subscribe ទៅកាន់ online status របស់ friend មួយនាក់, ហើយនិង cleans up ដោយការ unsubscribe ពីវា៖

```js{10-16}
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);

    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

ក្នុងឧទាហរណ៍នេះ, React នឹង unsubscribe ពី `ChatAPI` របស់យើង នៅពេលដែល component unmounts, ក៏ដូចជាបន្ទាប់ពី re-running effect ដោយសារតែ render បន្តបន្ទាប់។ (ប្រសិនបើអ្នកចង់, មានវិធីមួយដើម្បី [ប្រាប់ React អោយ skip ការ re-subscribe](/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects) ប្រសិនបើ `props.friend.id` ដែលយើងបាន pass ទៅអោយ `ChatAPI` មិនបានផ្លាស់ប្តូរ។)

ដូចទៅនឹង `useState`, អ្នកអាចប្រើ effect ច្រើនជាងតែមួយ នៅក្នុង component មួយ៖

```js{3,8}
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

Hooks អនុញ្ញាតឱ្យអ្នករៀបចំ side effects នៅក្នុង component ដោយ បំណែកអ្វីដែលទាក់ទងគ្នា (ដូចជាការបន្ថែមនិងការយកចេញ subscription), ជាជាងបង្ខំឱ្យមានការបំបែកដោយផ្អែកលើ lifecycle methods។

>ការពន្យល់យ៉ាងលម្អិត
>
>អ្នកអាចស្វែងយល់បន្ថែមអំពី `useEffect` លើទំព័រផ្សេង៖ [ការប្រើប្រាស់ Effect Hook](/docs/hooks-effect.html)។

## ✌️ Rules of Hooks {#rules-of-hooks}

Hooks គឺ JavaScript functions, ប៉ុន្តែពួកគេដាក់ចេញច្បាប់ (rule) ពីរបន្ថែមទៀត៖

* Call Hooks តែ **នៅ top level**។ កុំ call Hooks នៅខាងក្នុង loops, លក្ខខណ្ឌ (conditions), ឬក៏ nested functions។
* Call Hooks តែ **ពី React function components**។ កុំ call Hooks ពី JavaScript functions។ (មានកន្លែងត្រឹមត្រូវមួយតែមួយផ្សេងទៀតដើម្បី call Hooks -- Customs Hooks របស់អ្នកផ្ទាល់។ យើងនឹងរៀនអំពីពួកគេក្នុងពេលបន្តិចទៀតនេះ។)

យើងផ្តល់នូវ [linter plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks) មួយដើម្បីអនុវត្តច្បាប់ទាំងនេះដោយស្វ័យប្រវត្តិ។​ យើងយល់ថាច្បាប់ទាំងនេះមើលទៅដូចជាមានកំណត់ឬច្របូកច្របល់នៅពេលដំបូង, ប៉ុន្តែវាចាំបាច់ណាស់ក្នុងការធ្វើឱ្យ Hooks ដំណើរការល្អ។

>ការពន្យល់យ៉ាងលម្អិត
>
>អ្នកអាចស្វែងយល់បន្ថែមអំពីច្បាប់​ (rules) នេះលើទំព័រផ្សេង៖ [ច្បាប់ (Rules) នៃ Hooks](/docs/hooks-rules.html)។

## 💡 Building Your Own Hooks {#building-your-own-hooks}

Sometimes, we want to reuse some stateful logic between components. Traditionally, there were two popular solutions to this problem: [higher-order components](/docs/higher-order-components.html) and [render props](/docs/render-props.html). Custom Hooks let you do this, but without adding more components to your tree.

Earlier on this page, we introduced a `FriendStatus` component that calls the `useState` and `useEffect` Hooks to subscribe to a friend's online status. Let's say we also want to reuse this subscription logic in another component.

First, we'll extract this logic into a custom Hook called `useFriendStatus`:

```js{3}
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

It takes `friendID` as an argument, and returns whether our friend is online.

Now we can use it from both components:


```js{2}
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

```js{2}
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

The state of these components is completely independent. Hooks are a way to reuse *stateful logic*, not state itself. In fact, each *call* to a Hook has a completely isolated state -- so you can even use the same custom Hook twice in one component.

Custom Hooks are more of a convention than a feature. If a function's name starts with "`use`" and it calls other Hooks, we say it is a custom Hook. The `useSomething` naming convention is how our linter plugin is able to find bugs in the code using Hooks.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven't considered. We are excited to see what custom Hooks the React community will come up with.

>Detailed Explanation
>
>You can learn more about custom Hooks on a dedicated page: [Building Your Own Hooks](/docs/hooks-custom.html).

## 🔌 Other Hooks {#other-hooks}

There are a few less commonly used built-in Hooks that you might find useful. For example, [`useContext`](/docs/hooks-reference.html#usecontext) lets you subscribe to React context without introducing nesting:

```js{2,3}
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
  // ...
}
```

And [`useReducer`](/docs/hooks-reference.html#usereducer) lets you manage local state of complex components with a reducer:

```js{2}
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);
  // ...
```

>Detailed Explanation
>
>You can learn more about all the built-in Hooks on a dedicated page: [Hooks API Reference](/docs/hooks-reference.html).

## Next Steps {#next-steps}

Phew, that was fast! If some things didn't quite make sense or you'd like to learn more in detail, you can read the next pages, starting with the [State Hook](/docs/hooks-state.html) documentation.

You can also check out the [Hooks API reference](/docs/hooks-reference.html) and the [Hooks FAQ](/docs/hooks-faq.html).

Finally, don't miss the [introduction page](/docs/hooks-intro.html) which explains *why* we're adding Hooks and how we'll start using them side by side with classes -- without rewriting our apps.
