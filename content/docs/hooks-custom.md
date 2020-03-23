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

There's nothing new inside of it -- the logic is copied from the components above. Just like in a component, make sure to only call other Hooks unconditionally at the top level of your custom Hook.

Unlike a React component, a custom Hook doesn't need to have a specific signature. We can decide what it takes as arguments, and what, if anything, it should return. In other words, it's just like a normal function. Its name should always start with `use` so that you can tell at a glance that the [rules of Hooks](/docs/hooks-rules.html) apply to it.

The purpose of our `useFriendStatus` Hook is to subscribe us to a friend's status. This is why it takes `friendID` as an argument, and returns whether this friend is online:

```js
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  return isOnline;
}
```

Now let's see how we can use our custom Hook.

## Using a Custom Hook {#using-a-custom-hook}

In the beginning, our stated goal was to remove the duplicated logic from the `FriendStatus` and `FriendListItem` components. Both of them want to know whether a friend is online.

Now that we've extracted this logic to a `useFriendStatus` hook, we can *just use it:*

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

**Is this code equivalent to the original examples?** Yes, it works in exactly the same way. If you look closely, you'll notice we didn't make any changes to the behavior. All we did was to extract some common code between two functions into a separate function. **Custom Hooks are a convention that naturally follows from the design of Hooks, rather than a React feature.**

**Do I have to name my custom Hooks starting with “`use`”?** Please do. This convention is very important. Without it, we wouldn't be able to automatically check for violations of [rules of Hooks](/docs/hooks-rules.html) because we couldn't tell if a certain function contains calls to Hooks inside of it.

**Do two components using the same Hook share state?** No. Custom Hooks are a mechanism to reuse *stateful logic* (such as setting up a subscription and remembering the current value), but every time you use a custom Hook, all state and effects inside of it are fully isolated.

**How does a custom Hook get isolated state?** Each *call* to a Hook gets isolated state. Because we call `useFriendStatus` directly, from React's point of view our component just calls `useState` and `useEffect`. And as we [learned](/docs/hooks-state.html#tip-using-multiple-state-variables) [earlier](/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns), we can call `useState` and `useEffect` many times in one component, and they will be completely independent.

### Tip: Pass Information Between Hooks {#tip-pass-information-between-hooks}

Since Hooks are functions, we can pass information between them.

To illustrate this, we'll use another component from our hypothetical chat example. This is a chat message recipient picker that displays whether the currently selected friend is online:

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

We keep the currently chosen friend ID in the `recipientID` state variable, and update it if the user chooses a different friend in the `<select>` picker.

Because the `useState` Hook call gives us the latest value of the `recipientID` state variable, we can pass it to our custom `useFriendStatus` Hook as an argument:

```js
  const [recipientID, setRecipientID] = useState(1);
  const isRecipientOnline = useFriendStatus(recipientID);
```

This lets us know whether the *currently selected* friend is online. If we pick a different friend and update the `recipientID` state variable, our `useFriendStatus` Hook will unsubscribe from the previously selected friend, and subscribe to the status of the newly selected one.

## `useYourImagination()` {#useyourimagination}

Custom Hooks offer the flexibility of sharing logic that wasn't possible in React components before. You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven't considered. What's more, you can build Hooks that are just as easy to use as React's built-in features.

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
