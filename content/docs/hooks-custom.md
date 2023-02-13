---
id: hooks-custom
title: Building Your Own Hooks
permalink: docs/hooks-custom.html
next: hooks-reference.html
prev: hooks-rules.html
---

<<<<<<< HEAD
*Hooks* គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។
=======
> Try the new React documentation.
> 
> These new documentation pages teach modern React and include live examples:
>
> - [Reusing Logic with Custom Hooks](https://beta.reactjs.org/learn/reusing-logic-with-custom-hooks)
>
> The new docs will soon replace this site, which will be archived. [Provide feedback.](https://github.com/reactjs/reactjs.org/issues/3308)

*Hooks* are a new addition in React 16.8. They let you use state and other React features without writing a class.
>>>>>>> 47adefd30c46f486428d8231a68e639d62f02c9e

ការបង្កើត Hooks ផ្ទាល់ខ្លួនរបស់អ្នក អនុញ្ញាតឱ្យអ្នក extract component logic ទៅជា functions ដែលអាចប្រើឡើងវិញ (reusable)។

នៅពេលដែលយើងបានកំពុងរៀនពី [ការប្រើ Effect Hook](/docs/hooks-effect.html#example-using-hooks-1), យើងបានឃើញ component នេះពី chat application មួយដែលបង្ហាញ message អំពី friend ដែល online និង offline៖

```js{4-15}
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

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

ឥឡូវសូមនិយាយថា chat application របស់យើង ក៏មាន contact list ដែរ, ហើយយើងចង់ render ឈ្មេាះនៃ users ដែល online ជាមួួយនិងពណ៌បៃតង។ យើងអាច copy និង paste logic ដែលស្រដៀងទៅក្នុង `FriendListItem` component របស់យើង ប៉ុន្តែវានឹងមិនល្អទេ៖

```js{4-15}
import React, { useState, useEffect } from 'react';

function FriendListItem(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

ជំនួស, យើនឹង shate logic នេះរវាង `FriendStatus` និង `FriendListItem`។

ជាប្រពៃណីនៅក្នុង React, យើងមានវិធីប្រជាប្រិយពីរដើម្បី share stateful logic រវាង components៖ [render props](/docs/render-props.html) និង [higher-order components](/docs/higher-order-components.html)។ ឥឡូវនេះយើងនឹងពិនិត្យមើលរបៀប Hooks ដោះស្រាយបញ្ហាដូចគ្នាជាច្រើនដោយមិនបង្ខំអ្នកឱ្យបន្ថែម components ទៅកាន់ tree។

## Extracting a Custom Hook {#extracting-a-custom-hook}

នៅពេលយើងចង់ share logic រវាង JavaScript functions ពីរ, យើង extract វាទៅជា function ទីបី។ ទាំង components និង Hooks គឺជា functions, ដូច្នេះការងារនេះក៏មានដំណើរការសម្រាប់ពួកវាដែរ!

**Custom Hook គឺជា JavaScript function ដែលមានឈ្មេាះផ្តើមដោយ "`use`" ហើយដែលអាចហៅថា Hook ផ្សេងទៀត។** ឧទាហរណ៍, `useFriendStatus` ខាងក្រោមគឺជា custom Hook តំបូងរបស់យើង៖

```js{3}
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

មិនមានអ្វីថ្មីនៅខាងក្នុងវាទេ -- logic ត្រូវបាន copy ពី component ខាងលើ។ ដូចគ្នានឹង component ដែរ, ប្រាកដថា call Hooks ផ្សេងៗដែលគ្មាន condition នៅ top level នៃ custom Hook របស់អ្នក។

មិនដូច React component, Custom Hook មិនចាំបាច់មាន specific signature មួយ។ យើងអាចសម្រេចចិត្តថាតើវាត្រូវការ arguments អ្វី​, និងអ្វី​, បើ​មាន​អ្វី, វាគួរតែ return។ ក្នុង​ន័យ​ផ្សេងទៀត, វាគ្រាន់តែដូច function ធម្មតាមួយ។ ឈ្មេាះវាគួរតែចាប់ផ្តើមដោយ `use` ដូច្នេះអ្នកអាចប្រាប់ភ្លាមពី [ច្បាប់ នៃ Hooks](/docs/hooks-rules.html) ដើម្បី apply ទៅកាន់វា។

គោលបំណងនៃ `useFriendStatus` Hook របស់យើងគឺដើម្បី subscribe ពួកយើងទៅកាន់ status របស់ friend។ នេះជាមូលហេតុដែលវាត្រូវការ `friendID` ជា argument, ហើយ returns friend នេះគឺ online៖

```js
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  return isOnline;
}
```

ឥឡូវយើងនឹងមើលពីរបៀបដែលយើងអាចប្រើ  custom Hook របស់យើង។

## Using a Custom Hook {#using-a-custom-hook}

នៅពេល​ចាប់ផ្តើម, គោលដៅដែលបានបញ្ជាក់របស់យើងគឺលុប logic ដែលជាន់គ្នាពី `FriendStatus` និង `FriendListItem` components។ ពួកវាទាំងពីរចង់ដឹងថា តើ friend គឺ online ដែរឬទេ។

ឥឡូវ​នេះយើងបាន extract logic នេះទៅជា `useFriendStatus` hook, យើអាច *គ្រាន់តែប្រើវា៖*

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

**តើកូដនេះស្មើឬដូចនឹងឧទាហរណ៍ដើមទេ?** បាទ, វាដំណើរការតាមរបៀបដូចគ្នា។ ប្រសិនបើអ្នកមើលឱ្យច្បាស់លាស់, អ្នកនឹងសម្គាល់ឃើញថាយើងមិនបានធ្វើការផ្លាស់ប្តូរឥរិយាបទទេ។ អ្វីដែលយើងបានធ្វើគឺ extract code ធម្មតាខ្លះរវាង functions ពីរទៅជា function ដាច់ដោយឡែក។ **Custom Hooks គឺជា convention ដែលធ្វើតាមធម្មជាតិនៃការ design នៃ Hooks, ជាជាង React feature។**

**តើខ្ញុំត្រូវដាក់ឈ្មោះ custom Hooks របស់ខ្ញុំដោយចាប់ផ្តើមដោយ “`use`”?** សូមធ្វើវា។ Convention នេះ គឺសំខាន់ណាស់។ ដោយ​គ្មាន​វា, យើងនឹងមិនអាចត្រួតពិនិត្យដោយស្វ័យប្រវត្តិចំពោះការ violations នៃ [ច្បាប់នៃ​ Hooks](/docs/hooks-rules.html) ព្រោះយើងមិនអាចប្រាប់បានទេថាតើ function ជាក់លាក់មានការ calls ទៅកាន់ Hooks ដែលនៅខាងក្នុងវា។

**តើ components ពីរប្រើ Hook ដូចគ្នា share state ដែរឬទេ?** ទេ។ Custom Hooks គឺជាយន្តការដើម្បីប្រើឡើងវិញនូវ *stateful logic*  (ដូចជាការ setting up subscription និង ការចងចាំ current value), ប៉ុន្តែរាល់ពេលដែលអ្នកប្រើ custom Hook, state និង effects ទាំងអស់ដែលនៅខាងក្នុងវាគឺ fully isolated។

**តើ custom Hook អាច get state ដែលនៅឆ្ងាយយ៉ាងដូចម្តេច?** រាល់ *ការ call* ទៅកាន់ Hook ទទួលបាន isolated state។ ពីព្រេាះយើង call `useFriendStatus` ដោយផ្ទាល់, តាមទស្សនៈរបស់ React, component របស់យើងគ្រាន់តែ calls `useState` និង `useEffect`។ ហើយដូចដែលយើង [បានរៀន](/docs/hooks-state.html#tip-using-multiple-state-variables) [មុននេះ](/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns), យើងអាច call `useState` និង `useEffect` ច្រើនដងនៅក្នុង component មួយ, ហើយពួកគេនឹងឯករាជ្យទាំងស្រុង។

### Tip: Pass Information Between Hooks {#tip-pass-information-between-hooks}

ដែល Hooks គឺជា functions, យើងអាចបញ្ជូន (pass) ព័ត៌មានរវាងពួកវា។

ដើម្បីបង្ហាញរឿងនេះ, យើងនឹងប្រើ component ផ្សេងពីសម្មតិកម្មឧទាហរណ៍ chat របស់យើង។ នេះគឺ​ជា chat message recipient picker ដែលបង្ហាញថា តើ friend ដែលបាន select បច្ចុប្បន្ន គឺ online៖

```js{8-9,13}
const friendList = [
  { id: 1, name: 'Phoebe' },
  { id: 2, name: 'Rachel' },
  { id: 3, name: 'Ross' },
];

function ChatRecipientPicker() {
  const [recipientID, setRecipientID] = useState(1);
  const isRecipientOnline = useFriendStatus(recipientID);

  return (
    <>
      <Circle color={isRecipientOnline ? 'green' : 'red'} />
      <select
        value={recipientID}
        onChange={e => setRecipientID(Number(e.target.value))}
      >
        {friendList.map(friend => (
          <option key={friend.id} value={friend.id}>
            {friend.name}
          </option>
        ))}
      </select>
    </>
  );
}
```

យើងរក្សាទុក friend ID ដែលបានជ្រើសរើសបច្ចុប្បន្ននៅក្នុង `recipientID` state variable, ហើយ ធ្វើបច្ចុប្បន្នភាពវាប្រសិនបើ​ user ជ្រើសរើស friend ផ្សេងនៅក្នុង `<select>` picker។

ព្រេាះការ call `useState` Hook ផ្តល់អោយយើងនូវតម្លៃចុងក្រោយនៃ `recipientID` state variable, យើងអាចបញ្ជូន (pass) វាទៅកាន់ custom `useFriendStatus` Hook របស់យើងជា argument មួយ៖

```js
  const [recipientID, setRecipientID] = useState(1);
  const isRecipientOnline = useFriendStatus(recipientID);
```

នេះអនុញ្ញាតឱ្យយើងដឹងថា តើ​ friend ដែល *ត្រូវបានជ្រើសរើសបច្ចុប្បន្ន* គឺ online ឬទេ។ ប្រសិនបើយើងជ្រើសរើសមិត្តភក្តិផ្សេង ហើយ ធ្វើបច្ចុប្បន្នភាព `recipientID` state variable, `useFriendStatus` Hook របស់យើងនឹង unsubscribe ពី friend ដែលបានជ្រើសរើសពីមុន, និង subscribe ទៅកាន់ status ដែលបានជ្រើសរើសថ្មី។

## `useYourImagination()` {#useyourimagination}

Custom Hooks ផ្តល់ជូននូវភាពបត់បែននៃការចែករំលែក logic ដែលមិនអាចទៅរួច នៅក្នុង React component ពីមុនមក។ អ្នកអាចសរសេរ custom Hooks ដែល cover ករណីប្រើប្រាស់ជាច្រើន ដូចជា form handling, animation, declarative subscriptions, timers, ហើយប្រហែលជាមានច្រើនទៀតដែលយើងមិនបានពិចារណា។ មាន​អ្វី​បន្ថែម, អ្នកអាចបង្កើត Hooks គឺគ្រាន់តែជាការងាយស្រួលក្នុងការប្រើជាលក្ខណៈពិសេសដែលភ្ជាប់មកជាមួយ React។

ព្យាយាមទប់ទល់នឹងការបន្ថែម abstraction ឆាប់ពេក។ ឥឡូវ​នេះ function components នេាះអាចធ្វើបានច្រើនទៀត, វាទំនងជាថា មធ្យមភាគនៃ function component នៅក្នុង codebase របស់អ្នកនឹងក្លាយជាវែងជាងនេះ។ នេះគឺធម្មតា --​ កុំមានអារម្មណ៍ដូចអ្នក *ត្រូវតែ* បំបែកវាភ្លាមទៅជា Hooks។ ប៉ុន្តែយើងក៏លើកទឹកចិត្តអ្នកឱ្យចាប់ផ្តើមករណីដែល custom Hook អាចលាក់ logic ដែលស្មុគស្មាញអោយនៅពីក្រោយ interface សាមញ្ញមួយ, ឬក៏ជួយដេាះស្រាយបញ្ហារញ៉េរញ៉ៃរបស់ component។

ឧទាហរណ៍, ប្រហែលជាអ្នកមាន component ស្មុគស្មាញដែលមាន local state ជាច្រើនដែលត្រូវបានគ្រប់គ្រងតាមរបៀប ad-hoc។ `useState` មិនបង្កើត centralizing ដើម្បីធ្វើបច្ចុប្បន្នភាព logic កាន់តែងាយស្រួលឡើយ ដូច្នេះអ្នកប្រហែលជា prefer សរសេរវាជា [Redux](https://redux.js.org/) reducer៖

```js
function todosReducer(state, action) {
  switch (action.type) {
    case 'add':
      return [...state, {
        text: action.text,
        completed: false
      }];
    // ... other actions ...
    default:
      return state;
  }
}
```

Reducers គឺងាយស្រួលណាស់ដើម្បី test ក្នុង isolation, និង scale ដើម្បីបង្ហាញការធ្វើបច្ចុប្បន្នភាព logic ដែលស្មុគស្មាញ។ អ្នកអាចបំបែកពួកវាដាច់ដោយឡែកពីគ្នាទៅជា reducers កាន់តែតូច បើចាំបាច់។ ទោះយ៉ាងណាក៏ដោយ, អ្នកក៏អាចរីករាយនឹងអត្ថប្រយោជន៍នៃការប្រើប្រាស់ React local state, ឬប្រហែលជាមិនចង់ install library ផ្សេង។

ដូច្នេះចុះបើយើងអាចសរសេរ `useReducer` Hook ដែលអនុញ្ញាតឱ្យយើងគ្រប់គ្រង *local* state នៃ component របស់យើងជាមួយ reducer? កំណែសាមញ្ញរបស់វាអាចមើលទៅដូចនេះ៖

```js
function useReducer(reducer, initialState) {
  const [state, setState] = useState(initialState);

  function dispatch(action) {
    const nextState = reducer(state, action);
    setState(nextState);
  }

  return [state, dispatch];
}
```

ឥឡូវនេះយើងអាចប្រើវានៅក្នុង component របស់យើង, ហើយអនុញ្ញាតឱ reducer drive state management របស់វា៖

```js{2}
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer, []);

  function handleAddClick(text) {
    dispatch({ type: 'add', text });
  }

  // ...
}
```

តម្រូវការដើម្បីគ្រប់គ្រង local state ជាមួយ reducer នៅក្នុង component ដែលស្មុគស្មាញ គឺជារឿងធម្មតា ដែលយើងបង្កើត `useReducer` Hook នៅក្នុង React។ អ្នកនឹងរកឃើញវាជាមួយគ្នានឹង built-in Hooks នៅក្នុង [Hooks API reference](/docs/hooks-reference.html)។
