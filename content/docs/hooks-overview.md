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

ជួនកាល, យើងចង់កាត់បន្ថយ stateful logic មួយចំនួនរវាង components។ ជាប្រពៃណី, មានដំណោះស្រាយពេញនិយមពីរចំពោះបញ្ហានេះ៖ [higher-order components](/docs/higher-order-components.html) និង [render props](/docs/render-props.html)។ Custom Hooks អនុញ្ញាតឱ្យអ្នកធ្វើរឿងនេះបាន, ប៉ុន្តែដោយមិនបន្ថែមទៀត components ទៅកាន់ tree របស់អ្នក។

មុននេះនៅលើទំព័រនេះ, យើងបានណែនាំ `FriendStatus` component មួយដែល calls `useState` និង `useEffect` Hooks ដើម្បី subscribe ទៅកាន់ online status របស់ friend ម្នាក់។ តេាះនិយាយថា យើងក៏ចង់កាត់បន្ថយ subscription logic នេះនៅក្នុង component ផ្សេង។

តំបូង, យើងនឹងស្រង់ (extract) logic នេះចូលទៅក្នុង custom Hook ដែលត្រូវបានគេហៅថា `useFriendStatus`៖

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

វាទទួលយក `friendID` ដែលជា argument, ហើយ returns ថា friend យើងគឺ online។

ឥឡូវ​នេះយើងអាចប្រើវាពី components ទាំងពីរ៖


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

<<<<<<< HEAD
State នៃ components ទាំងនេះគឺ ឯករាជ្យទាំងស្រុង។ Hooks គឺជាមធ្យោបាយដើម្បីកាត់បន្ថយ *stateful logic*, មិនមែន state ខ្លួនវាផ្ទាល់។ តាមពិត, *call* នីមួយៗ ទៅកាន់ Hook មួយ មាន state ដាច់ឆ្ងាយទាំងស្រុង -- ដូច្នេះអ្នកអាចសូម្បីតែប្រើ custom Hook ដូចគ្នាពីរដងនៅក្នុង component តែមួយ។
=======
The state of each component is completely independent. Hooks are a way to reuse *stateful logic*, not state itself. In fact, each *call* to a Hook has a completely isolated state -- so you can even use the same custom Hook twice in one component.
>>>>>>> ba290ad4e432f47a2a2f88d067dacaaa161b5200

Custom Hooks គឺលើសពី convention មួយជាង feature មួយ។ ប្រសិនបើឈ្មេាះរបស់ function ផ្តើមដោយ "`use`" និងវា call ថា Hooks ផ្សេង, យើងអាចនិយាយបានថាវាគឺជា custom Hook មួយ។ `useSomething` convention នៃការដាក់ឈ្មេាះគឺជារបៀបដែល linter plugin របស់យើងគឺអាចរកឃើញ bugs នៅក្នុង code ដែលកំពុងប្រើ Hooks។

អ្នកអាចសរសេរ custom Hooks ដែលគ្រប់ដណ្តប់នូវការករណីប្រើប្រាស់យ៉ាងទូលំទូលាយដូចជា form handling, animation, declarative subscriptions, timers, និងអ្វីៗផ្សេងៗទៀតដែលយើមិនបានគិតដល់។ យើងរំភើបណាស់ដែលបានឃើញអ្វីដែល សហគមន៍ React custom Hooks នឹងមកជាមួយ។

>ការពន្យល់យ៉ាងលម្អិត
>
>អ្នកអាចស្វែងយល់បន្ថែមអំពី custom Hooks លើទំព័រផ្សេង៖ [ការបង្កើត Hooks ផ្ទាល់ខ្លួនរបស់អ្នក](/docs/hooks-custom.html)។

## 🔌 Other Hooks {#other-hooks}

មានតិចតួចដែលត្រូវបានប្រើជាទូទៅ built-in Hooks ដែលអ្នកប្រហែលយល់ថា useful។ ឧទាហរណ៍, [`useContext`](/docs/hooks-reference.html#usecontext) 
អនុញ្ញាតឱ្យអ្នក subscribe ទៅកាន់ React context ដោយមិនមានការណែនាំ nesting៖

```js{2,3}
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
  // ...
}
```

ហើយនិង [`useReducer`](/docs/hooks-reference.html#usereducer) អនុញ្ញាតឱ្យអ្នកគ្រប់គ្រង local state នៃ components ស្មុគស្មាញជាមួយនិង reducer៖

```js{2}
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);
  // ...
```

>ការពន្យល់យ៉ាងលម្អិត
>
>អ្នកអាចស្វែងយល់បន្ថែមអំពី built-in Hooks ទាំងអស់ លើទំព័រផ្សេង៖: [Hooks API Reference](/docs/hooks-reference.html)។

## Next Steps {#next-steps}

Phew, នេះគឺលឿនមែនទែន! ប្រសិនបើមានរឿងខ្លះមិនសមហេតុផល ឬក៏អ្នកចង់រៀនលម្អិតបន្ថែមទៀត, អ្នកអាចអាននៅទំព័របន្ទាប់, ចាប់ផ្តើមជាមួយឯកសារ [State Hook](/docs/hooks-state.html)។

អ្នកអាចពិនិត្យផងដែរនូវ [Hooks API reference](/docs/hooks-reference.html) ហើយនិង [Hooks FAQ](/docs/hooks-faq.html) របស់យើង។

ជាចុងក្រោយ, កុំខកខាន [introduction page](/docs/hooks-intro.html) ដែលពន្យល់ *ហេតុអ្វី* យើកំពុងបន្ថែម Hooks និងរបៀបដែលយើងនឹងចាប់ផ្តើមការប្រើប្រាស់ពួកវានៅក្បែរគ្នាជាមួយ classes -- ដោយគ្មានការសរសេរឡើងវិញនូវ app របស់យើង។
