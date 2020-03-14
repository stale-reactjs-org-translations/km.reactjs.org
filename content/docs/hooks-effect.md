---
id: hooks-state
title: Using the Effect Hook
permalink: docs/hooks-effect.html
next: hooks-rules.html
prev: hooks-state.html
---

*Hooks* គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។

*Effect Hook* អនុញ្ញាតឱ្យអ្នកអនុវត្ត side effects នៅក្នុង function components៖

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

អត្ថបទខ្លីនេះមានមូលដ្ឋានលើ [counter example ពីទំព័រមុន](/docs/hooks-state.html), ប៉ុន្តែយើងបានបន្ថែមមុខងារ (feature) ថ្មីទៅវា៖ យើង set document title អោយ​ custom message រួមទាំង ចំនួននៃការចុច។

ការទាញយកទិន្នន័យ (Data fetching), setting up a subscription, និង ការផ្លាស់ប្តូរ DOM ដោយដៃ នៅក្នុង React components គឺជាឧទាហរណ៍ទាំងអស់នៃ side effects។ ថា​តើ​បាន​ឬ​មិន​បាន អ្នកធ្លាប់ហៅប្រតិបត្តិការទាំងនេះ "side effects" (ឬគ្រាន់តែ "effects"), អ្នកទំនងជាបានអនុវត្តពួកវាក្នុង components របស់អ្នកពីមុនមក។

>គន្លឹះ
>
>ប្រសិនបើអ្នកសុាំ (familiar) ជាមួយ React class lifecycle methods, អ្នកអាចគិតថា `useEffect` Hook គឺដូចទៅនឹង `componentDidMount`, `componentDidUpdate`, និង `componentWillUnmount`
រួមបញ្ចូលគ្នា។

មានពីរប្រភេទនៃ side effects ក្នុង React components៖ ប្រភេទដែលមិនទាមទារអោយ cleanup, និងប្រភេទដេលទាមទារអោយ clearnup។ សូមក្រឡេកមើលភាពខុសគ្នានេះឱ្យកាន់តែលម្អិត។

## Effects Without Cleanup {#effects-without-cleanup}

ពេលខ្លះ, យើងចង់ **run កូដបន្ថែមមួយចំនួនបន្ទាប់ពី React ធ្វើបច្ចុប្បន្នភាព DOM។** Network requests, ការផ្លាស់ប្តូរ DOM ដោយដៃ, និង logging គឺជា ឧទាហរណ៍ទូទៅនៃ effects ដែលមិនទាមទារអោយ cleanup។ យើងនិយាយដូច្នេះពីព្រេាះយើងអាច run ពួកវាហើយត្រូវភ្លេចអំពីពួកវាភ្លាម។ សូមប្រៀបធៀបរបៀប classes និង Hooks អនុញ្ញាតអោយយើងបង្ហាញពី side effects ទាំងនេាះ។

### Example Using Classes {#example-using-classes}

នៅក្នុង React class components, `render` method ខ្លួនឯងមិនគួរបណ្តាលឱ្យ side effects។
វាលឿនពេកហើយ -- ជាធម្មតាយើងចង់អនុវត្ត (perform) effects របស់យើង *បន្ទាប់ពី* React បានធ្វើបច្ចុប្បន្នភាព DOM។

នេះ​ជាមូលហេតុដែលនៅក្នុង React classes, យើងដាក់ side effects ចូលទៅក្នុង `componentDidMount` និង `componentDidUpdate`។ ត្រលប់មកឧទាហរណ៍របស់យើងវិញ, នេះគឺជា React counter class component ដែលធ្វើបច្ចុប្បន្នភាព document title បន្ទាប់ពី React បានផ្លាស់ប្តូរ DOM៖

```js{9-15}
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

កត់សំគាល់របៀប **យើងមាន duplicate code រវាង lifecycle methods ពីរនេះនៅក្នុង class។**

នេះដោយសារតែក្នុងករណីជាច្រើនដែលយើងចង់អនុវត្ត side effect ដូចគ្នា ដោយមិនគិតថាតើ component ទើបតែត្រូវបាន mount ទេ, ឬក៏វាបានធ្វើបច្ចុប្បន្នភាព។ តាមគំនិត, យើងចង់អោយវាកើតឡើងបន្ទាប់ពីរាល់ពេល render -- ប៉ុន្តែ React class components មិនមាន method ដូចនេះ។ យើងអាច extract method ដាច់ដោយឡែក ប៉ុន្តែយើងនឹងនៅតែត្រូវ call វានៅពីរកន្លែងផ្សេងគ្នា។

ឥឡូវ​នេះតោះមើលរបៀបដែលយើងអាចធ្វើបានដូចគ្នាជាមួយ `useEffect` Hook។

### Example Using Hooks {#example-using-hooks}

យើងបានឃើញឧទាហរណ៍នេះរួចហើយនៅផ្នែកខាងលើនៃទំព័រនេះ, ប៉ុន្តែសូមពិនិត្យឱ្យបានដិតដល់អំពីវា៖

```js{1,6-8}
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
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

**តើ `useEffect` ធ្វើអ្វីខ្លះ?** ដោយការប្រើ Hook នេះ, អ្នកប្រាប់ React ថា compoent របស់អ្នក ត្រូវការធ្វើអ្វីមួយបន្ទាប់ពី render។ React នឹងចងចាំ function ដែលអ្នកបានបេាះ (pass) (យើងនឹងយោងទៅវាដូចជា "effect" របស់យើង), ហើយ call វាពេលក្រោយបន្ទាប់ពីការអនុវត្តការ
ធ្វើបច្ចុប្បន្នភាព DOM។ នៅក្នុង effect នេះ, យើង set the document titile, ប៉ុន្តែយើងក៏អាចអនុវត្ត data fetching ឬ call API ចាំបាច់មួយចំនួនផ្សេងទៀត។

**ហេតុអ្វី `useEffect` ត្រូវបាន call នៅខាងក្នុង component?** ការដាក់ `useEffect` នៅខាងក្នុង component អនុញ្ញាតឱ្យយើងចូលប្រើ (access) `count` state variable (ឬក៏ props ផ្សេងៗ) ពី effect។ យើងមិនត្រូវការ API ពិសេសដើម្បីអាន (read) វាទេ -- វាស្ថិតនៅក្នុងវិសាលភាព function រួចហើយ។ Hooks ភ្ជាប់មកជាមួយ JavaScript closures និង ចៀសវាងការណែនាំ React-specific APIs ដែល 
JavaScript បានផ្តល់នូវដំណោះស្រាយរួចហើយ។

**តើ `useEffect` run បន្ទាប់ពីរាល់ពេល render?** បាទ! By default, វា run ទាំងបន្ទាប់ពី render តំបូង *និង* ទាំងបន្ទាប់ពីរាល់ពេលធ្វើបច្ចុប្បន្នភាព (update)។ (យើងនឹងនិយាយពី [how to customize this](#tip-optimizing-performance-by-skipping-effects) នៅពេលក្រោយ។)​ ជំនួសឱ្យការគិតនៅក្នុងលក្ខខណ្ឌនៃ "mounting" និង "updating", អ្នកអាចគិតថាវាងាយស្រួលក្នុងការគិតថា effects កើតឡើង "បន្ទាប់ពី render"។ React ធានាថា DOM ត្រូវបានគេធ្វើបច្ចុប្បន្នភាពនៅពេលវា run the effects។

### Detailed Explanation {#detailed-explanation}

ឥឡូវយើងដឹងកាន់តែច្បាស់ហើយអំពី effects, បន្ទាត់ទាំងនេះគួរតែធ្វើឱ្យយល់បាន៖

```js
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
}
```

យើងប្រកាស (declare) `count` state variable, ហើយបន្ទាប់មកយើងប្រាប់ React យើងត្រូវប្រើ effect។ យើងបេាះ (pass) function ទៅអោយ `useEffect` Hook។ function នេះយើងបេាះ (pass) *គឺ* effect របស់យើង។ នៅខាងក្នុង effect របស់យើង, យើង set the document title ដោយការប្រើ the `document.titile` របស់ browser API។ យើងអាច read `count` ចុងក្រោយដែលនៅខាងក្នុង effect ពីព្រោះវាស្ថិតនៅក្នុងវិសាលភាពនៃ function របស់យើង។ នៅពេល React renders component របស់យើង, វានឹងចងចាំ effect ដែលយើងបានប្រើ, ហើយបន្ទាប់មក run effect របស់យើងបន្ទាប់ពីធ្វើបច្ចុប្បន្នភាព DOM។ នេះកើតឡើងសម្រាប់រាល់ពេល render, រួមទាំងពេលដំបូង។

JavaScript developers ដែលមានបទពិសោធន៍​ អាចកត់សម្គាល់ឃើញថា function ដែលបានបេាះ (pass) អោយ `useEffect` នឹងមានភាពខុសគ្នានៅលើរាល់ការ render។ នេះគឺជាចេតនា។ តាមពិត, នេះជាអ្វីដែលអាចអោយយើងអាន (read) តម្លៃ `count` ពីខាងក្នុង effect ដោយមិនបារម្ភអំពីវាមិនទទួលបានតម្លៃចុងក្រោយ។ រាល់ពេលយើង re-render,​​យើងកំណត់ពេលវេលា effect _ផ្សេង_, ជំនួសមួយមុន។ តាមរបៀបមួយទៀត, បែបនេះធ្វើអោយ effect មានឥរិយាបទច្រើនដូចជាផ្នែកមួយនៃលទ្ធផល render -- effect និមួយៗ "belongs" ទៅ render ជាក់លាក់មួយ។ យើងនឹងឃើញកាន់តែច្បាស់ថាហេតុអ្វីបានជាវាមានប្រយោជន៍ [នៅពេលក្រោយនៅលើទំព័រនេះ](#explanation-why-effects-run-on-each-update)។

>គន្លឹះ
>
>មិន​ដូច `componentDidMount` ឬ `componentDidUpdate`, effects បានកំណត់ពេលជាមួយ `useEffect` ដោយមិន block browser ពីការធ្វើបច្ចុប្បន្នភាព screen។ វាធ្វើឱ្យកម្មវិធីរបស់អ្នកកាន់តែឆ្លើយតប (responsive)។ ភាគច្រើននៃ effect មិនចាំបាច់កើតឡើងដំណាលគ្នាទេ (synchronous)។ ក្នុងករណីមិនធម្មតាដែលពួកវាធ្វើ (ដូចជាវាស់ layout), មាន [`useLayoutEffect`](/docs/hooks-reference.html#uselayouteffect) Hook ដាច់ដោយឡែក ជាមួយ API ដូចគ្នាបេះបិទទៅនឹង `useEffect`។

## Effects with Cleanup {#effects-with-cleanup}

មុននេះ, យើងបានពិនិត្យមើលវិធីដើម្បីបង្ហាញ side effects ដែលមិនត្រូវការ cleanup។ ទោះយ៉ាងណាក៏ដោយ, effects មួយចំនួនត្រូវការ។ ឧទាហរណ៍, **យើងប្រហែលជាចង់ set up a subscription** អោយ external data source មួយចំនួន។ ក្នុងករណី​នេះ, វាជាការសំខាន់ដើម្បី clean up ដូច្នេះយើងមិនបង្កើត memory leak! 
ចូរយើងប្រៀបធៀបរបៀបដែលយើងអាចធ្វើវាបានជាមួយ calleses និងជាមួយ Hooks។

### Example Using Classes {#example-using-classes-1}

In a React class, you would typically set up a subscription in `componentDidMount`, and clean it up in `componentWillUnmount`. For example, let's say we have a `ChatAPI` module that lets us subscribe to a friend's online status. Here's how we might subscribe and display that status using a class:

```js{8-26}
class FriendStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }

  render() {
    if (this.state.isOnline === null) {
      return 'Loading...';
    }
    return this.state.isOnline ? 'Online' : 'Offline';
  }
}
```

Notice how `componentDidMount` and `componentWillUnmount` need to mirror each other. Lifecycle methods force us to split this logic even though conceptually code in both of them is related to the same effect.

>Note
>
>Eagle-eyed readers may notice that this example also needs a `componentDidUpdate` method to be fully correct. We'll ignore this for now but will come back to it in a [later section](#explanation-why-effects-run-on-each-update) of this page.

### Example Using Hooks {#example-using-hooks-1}

Let's see how we could write this component with Hooks.

You might be thinking that we'd need a separate effect to perform the cleanup. But code for adding and removing a subscription is so tightly related that `useEffect` is designed to keep it together. If your effect returns a function, React will run it when it is time to clean up:

```js{6-16}
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

**Why did we return a function from our effect?** This is the optional cleanup mechanism for effects. Every effect may return a function that cleans up after it. This lets us keep the logic for adding and removing subscriptions close to each other. They're part of the same effect!

**When exactly does React clean up an effect?** React performs the cleanup when the component unmounts. However, as we learned earlier, effects run for every render and not just once. This is why React *also* cleans up effects from the previous render before running the effects next time. We'll discuss [why this helps avoid bugs](#explanation-why-effects-run-on-each-update) and [how to opt out of this behavior in case it creates performance issues](#tip-optimizing-performance-by-skipping-effects) later below.

>Note
>
>We don't have to return a named function from the effect. We called it `cleanup` here to clarify its purpose, but you could return an arrow function or call it something different.

## Recap {#recap}

We've learned that `useEffect` lets us express different kinds of side effects after a component renders. Some effects might require cleanup so they return a function:

```js
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

Other effects might not have a cleanup phase, and don't return anything.

```js
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

The Effect Hook unifies both use cases with a single API.

-------------

**If you feel like you have a decent grasp on how the Effect Hook works, or if you feel overwhelmed, you can jump to the [next page about Rules of Hooks](/docs/hooks-rules.html) now.**

-------------

## Tips for Using Effects {#tips-for-using-effects}

We'll continue this page with an in-depth look at some aspects of `useEffect` that experienced React users will likely be curious about. Don't feel obligated to dig into them now. You can always come back to this page to learn more details about the Effect Hook.

### Tip: Use Multiple Effects to Separate Concerns {#tip-use-multiple-effects-to-separate-concerns}

One of the problems we outlined in the [Motivation](/docs/hooks-intro.html#complex-components-become-hard-to-understand) for Hooks is that class lifecycle methods often contain unrelated logic, but related logic gets broken up into several methods. Here is a component that combines the counter and the friend status indicator logic from the previous examples:

```js
class FriendStatusWithCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0, isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }
  // ...
```

Note how the logic that sets `document.title` is split between `componentDidMount` and `componentDidUpdate`. The subscription logic is also spread between `componentDidMount` and `componentWillUnmount`. And `componentDidMount` contains code for both tasks.

So, how can Hooks solve this problem? Just like [you can use the *State* Hook more than once](/docs/hooks-state.html#tip-using-multiple-state-variables), you can also use several effects. This lets us separate unrelated logic into different effects:

```js{3,8}
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

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
  // ...
}
```

**Hooks let us split the code based on what it is doing** rather than a lifecycle method name. React will apply *every* effect used by the component, in the order they were specified.

### Explanation: Why Effects Run on Each Update {#explanation-why-effects-run-on-each-update}

If you're used to classes, you might be wondering why the effect cleanup phase happens after every re-render, and not just once during unmounting. Let's look at a practical example to see why this design helps us create components with fewer bugs.

[Earlier on this page](#example-using-classes-1), we introduced an example `FriendStatus` component that displays whether a friend is online or not. Our class reads `friend.id` from `this.props`, subscribes to the friend status after the component mounts, and unsubscribes during unmounting:

```js
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

**But what happens if the `friend` prop changes** while the component is on the screen? Our component would continue displaying the online status of a different friend. This is a bug. We would also cause a memory leak or crash when unmounting since the unsubscribe call would use the wrong friend ID.

In a class component, we would need to add `componentDidUpdate` to handle this case:

```js{8-19}
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate(prevProps) {
    // Unsubscribe from the previous friend.id
    ChatAPI.unsubscribeFromFriendStatus(
      prevProps.friend.id,
      this.handleStatusChange
    );
    // Subscribe to the next friend.id
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

Forgetting to handle `componentDidUpdate` properly is a common source of bugs in React applications.

Now consider the version of this component that uses Hooks:

```js
function FriendStatus(props) {
  // ...
  useEffect(() => {
    // ...
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

It doesn't suffer from this bug. (But we also didn't make any changes to it.)

There is no special code for handling updates because `useEffect` handles them *by default*. It cleans up the previous effects before applying the next effects. To illustrate this, here is a sequence of subscribe and unsubscribe calls that this component could produce over time:

```js
// Mount with { friend: { id: 100 } } props
ChatAPI.subscribeToFriendStatus(100, handleStatusChange);     // Run first effect

// Update with { friend: { id: 200 } } props
ChatAPI.unsubscribeFromFriendStatus(100, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(200, handleStatusChange);     // Run next effect

// Update with { friend: { id: 300 } } props
ChatAPI.unsubscribeFromFriendStatus(200, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(300, handleStatusChange);     // Run next effect

// Unmount
ChatAPI.unsubscribeFromFriendStatus(300, handleStatusChange); // Clean up last effect
```

This behavior ensures consistency by default and prevents bugs that are common in class components due to missing update logic.

### Tip: Optimizing Performance by Skipping Effects {#tip-optimizing-performance-by-skipping-effects}

In some cases, cleaning up or applying the effect after every render might create a performance problem. In class components, we can solve this by writing an extra comparison with `prevProps` or `prevState` inside `componentDidUpdate`:

```js
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `You clicked ${this.state.count} times`;
  }
}
```

This requirement is common enough that it is built into the `useEffect` Hook API. You can tell React to *skip* applying an effect if certain values haven't changed between re-renders. To do so, pass an array as an optional second argument to `useEffect`:

```js{3}
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

In the example above, we pass `[count]` as the second argument. What does this mean? If the `count` is `5`, and then our component re-renders with `count` still equal to `5`, React will compare `[5]` from the previous render and `[5]` from the next render. Because all items in the array are the same (`5 === 5`), React would skip the effect. That's our optimization.

When we render with `count` updated to `6`, React will compare the items in the `[5]` array from the previous render to items in the `[6]` array from the next render. This time, React will re-apply the effect because `5 !== 6`. If there are multiple items in the array, React will re-run the effect even if just one of them is different.

This also works for effects that have a cleanup phase:

```js{10}
useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Only re-subscribe if props.friend.id changes
```

In the future, the second argument might get added automatically by a build-time transformation.

>Note
>
>If you use this optimization, make sure the array includes **all values from the component scope (such as props and state) that change over time and that are used by the effect**. Otherwise, your code will reference stale values from previous renders. Learn more about [how to deal with functions](/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) and [what to do when the array changes too often](/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often).
>
>If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array (`[]`) as a second argument. This tells React that your effect doesn't depend on *any* values from props or state, so it never needs to re-run. This isn't handled as a special case -- it follows directly from how the dependencies array always works.
>
>If you pass an empty array (`[]`), the props and state inside the effect will always have their initial values. While passing `[]` as the second argument is closer to the familiar `componentDidMount` and `componentWillUnmount` mental model, there are usually [better](/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) [solutions](/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often) to avoid re-running effects too often. Also, don't forget that React defers running `useEffect` until after the browser has painted, so doing extra work is less of a problem.
>
>We recommend using the [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) rule as part of our [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It warns when dependencies are specified incorrectly and suggests a fix.

## Next Steps {#next-steps}

Congratulations! This was a long page, but hopefully by the end most of your questions about effects were answered. You've learned both the State Hook and the Effect Hook, and there is a *lot* you can do with both of them combined. They cover most of the use cases for classes -- and where they don't, you might find the [additional Hooks](/docs/hooks-reference.html) helpful.

We're also starting to see how Hooks solve problems outlined in [Motivation](/docs/hooks-intro.html#motivation). We've seen how effect cleanup avoids duplication in `componentDidUpdate` and `componentWillUnmount`, brings related code closer together, and helps us avoid bugs. We've also seen how we can separate effects by their purpose, which is something we couldn't do in classes at all.

At this point you might be questioning how Hooks work. How can React know which `useState` call corresponds to which state variable between re-renders? How does React "match up" previous and next effects on every update? **On the next page we will learn about the [Rules of Hooks](/docs/hooks-rules.html) -- they're essential to making Hooks work.**
