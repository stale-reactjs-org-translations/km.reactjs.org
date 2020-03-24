---
id: hooks-custom
title: Building Your Own Hooks
permalink: docs/hooks-custom.html
next: hooks-reference.html
prev: hooks-rules.html
---

*Hooks* គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។

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

Try to resist adding abstraction too early. Now that function components can do more, it's likely that the average function component in your codebase will become longer. This is normal -- don't feel like you *have to* immediately split it into Hooks. But we also encourage you to start spotting cases where a custom Hook could hide complex logic behind a simple interface, or help untangle a messy component.

For example, maybe you have a complex component that contains a lot of local state that is managed in an ad-hoc way. `useState` doesn't make centralizing the update logic any easier so you might prefer to write it as a [Redux](https://redux.js.org/) reducer:

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

Reducers are very convenient to test in isolation, and scale to express complex update logic. You can further break them apart into smaller reducers if necessary. However, you might also enjoy the benefits of using React local state, or might not want to install another library.

So what if we could write a `useReducer` Hook that lets us manage the *local* state of our component with a reducer? A simplified version of it might look like this:

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

Now we could use it in our component, and let the reducer drive its state management:

```js{2}
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer, []);

  function handleAddClick(text) {
    dispatch({ type: 'add', text });
  }

  // ...
}
```

The need to manage local state with a reducer in a complex component is common enough that we've built the `useReducer` Hook right into React. You'll find it together with other built-in Hooks in the [Hooks API reference](/docs/hooks-reference.html).
