---
id: hooks-state
title: Using the State Hook
permalink: docs/hooks-state.html
next: hooks-effect.html
prev: hooks-overview.html
---

Hooks គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។

[ទំព័រណែនាំ](/docs/hooks-intro.html) បានប្រើឧទាហរណ៍នេះដើម្បីស៊ាំ (get familiar) ជាមួយ Hooks

```js{4-5}
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

យើងនឹងចាប់ផ្តើមរៀនពី Hooks ដោយប្រៀបធៀបកូដនេះទៅនឹងឧទាហរណ៍កំរិតស្មើរគ្នាឬដូចគ្នា។

## Equivalent Class Example {#equivalent-class-example}

ប្រសិនបើអ្នកបានប្រើ classes នៅក្នុង React ពីមុន, កូដនេះគួរតែមើលទៅស៊ាំ (familiar)

```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
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

State ចាប់ផ្តើមដោយ `{ count: 0 }`, និងយើងតម្លើង `state.count` នៅពេល user ចុចប៊ូតុងដោយការ call `this.setState()`។ យើងនឹងប្រើអត្ថបទខ្លីៗចាប់ពី class នេះ ពេញទំព័រនេះ។

>ចំណាំ៖
>
>អ្នកប្រហែលជាកំពុងតែឆ្ងល់ហើយ ហេតុអ្វីយើងកំពុងតែប្រើ counter នៅទីនេះជជំនួសអោយឧទាហរណ៍ជាក់ស្តែង។ នេះគឺដើម្បីជួយយើងឱ្យផ្តោតលើ API ខណៈពេលដែលយើងកំពុងធ្វើជំហានដំបូងរបស់យើងជាមួយ Hooks។

## Hooks and Function Components {#hooks-and-function-components}

ជាការរំលឹក, function components នៅក្នុង React មើលទៅដូចនេះ៖

```js
const Example = (props) => {
  // You can use Hooks here!
  return <div />;
}
```

ឬក៏ដូចនេះ៖

```js
function Example(props) {
  // You can use Hooks here!
  return <div />;
}
```

អ្នកប្រហែលជាធ្លាប់បានស្គាល់ពីមុនថាទាំងនេះជា "stateless components"។ ឥឡូវនេះយើងកំពុងណែនាំសមត្ថភាពក្នុងការប្រើប្រាស់ React state ពីទីនេះ, 
ដូច្នេះយើងចូលចិត្តឈ្មោះ "function components" ជាង។

Hooks ** មិន ** ធ្វើការនៅខាងក្នុង classes ទេ។ ប៉ុន្តែអ្នកអាចប្រើវាជំនួសឱ្យការសរសេរ classes។

## What's a Hook? {#whats-a-hook}

ឧទាហរណ៍ថ្មីរបស់យើងចាប់ផ្តើមដោយការ import `useState` Hook ពី React៖

```js{1}
import React, { useState } from 'react';

function Example() {
  // ...
}
```

**តើ Hook គឺជាអ្វី?** Hook គឺជា function ពិសេសមួយដែលអនុញ្ញាតឱ្យអ្នក "hook into" លក្ខណៈពិសេស (features) របស់ React។ ឧទាហរណ៍, `useState` គឺជា Hook ដែលអនុញ្ញាតឱ្យអ្នកបន្ថែម React state ទៅកាន់ function components។

**តើខ្ញុំនឹងប្រើ Hook នៅពេលណា?** ប្រសិនបើអ្នកសរសេរ function component មួយហើយដឹងថាអ្នកត្រូវការបន្ថែម state មួយចំនួនអោយវា, ពីមុនអ្នកត្រូវតែបំលែងវាជាស class។ ឥឡូវ​នេះអ្នកអាចប្រើ Hook នៅខាងក្នុង function component ដែលមានស្រាប់។ យើងនឹងធ្វើវាឥឡូវនេះ!

>ចំណាំ៖
>
>មានច្បាប់ពិសេសមួយចំនួនអំពីកន្លែងដែលអ្នកអាចនិងមិនអាចប្រើប Hooks នៅក្នុង component មួយបាន។ 
យើងនឹងរៀនវានៅក្នុង [វិធាននៃ Hooks](/docs/hooks-rules.html)។

## Declaring a State Variable {#declaring-a-state-variable}

នៅក្នុង class, យើងផ្តល់តម្លៃតំបូងអោយ `count` state នូវតម្លៃ `0` ដោយការ set `this.state` ជា `{ count: 0 }` នៅក្នុង constructor៖

```js{4-6}
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
```

នៅក្នុង function component, យើងមិនមាន `this`, ដូច្នេះយើងមិនអាច assign ឬ អាន (read) `this.state`​។ ជំនួសទៅវិញ, យើង call `useState` Hook ដោយផ្ទាល់នៅខាងក្នុង component របស់យើង៖

```js{4,5}
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
```

**តើការហៅ (call) `useState` ធ្វើអ្វី?** វាប្រកាស "state variable"។ Variable របស់យើងត្រូវបានគេហៅថា `count` ប៉ុន្តែយើងអាចហៅវាថាជាអ្វីផ្សេង, ដូចជា `banana`។ នេះគឺជាវិធីដើម្បី "រក្សា" តម្លៃមួយចំនួនរវាង function calls — `useState` 
គឺជាវិធីថ្មីដើម្បីប្រើសមត្ថភាពដូចគ្នាដែល `this.state` ផ្តល់ជូននៅក្នុង class។ ជាធម្មតា, variables "បាត់ (disappear)" នៅពេល function exits ប៉ុន្តែ state variables ត្រូវបានរក្សាទុកដោយ React។

**តើអ្វីដែលយើងបេាះ (pass) អោយ​ `useState` ជា argument?** argument តែមួយគត់សម្រាប់ `useState()` Hook គឺ initial state។ មិនដូចជាមួយ classes, state 
មិនចាំបាច់ជា object។ យើងអាចរក្សាទុក number ឬ string 
ប្រសិនបើនោះជាអ្វីដែលយើងត្រូវការ។ ក្នុងឧទាហរណ៍របស់យើង, យើងគ្រាន់តែចង់បាន number សម្រាប់ ចំនួនដងដែលអ្នកប្រើប្រាស់ចុច, ដូច្នេះបេាះ (pass) `0` ជា initial state សម្រាប់ variable របស់យើង។ (ប្រសិនបើយើងចង់រក្សាទុកតម្លៃពីរផ្សេងគ្នានៅក្នុង state, យើងនឹង call `useState()` ពីរដង។)

**តើអ្វីដែល `useState` return?** វា returns គូរ (pair) នៃ តម្លៃ៖ state បច្ចុប្បន្ន (current) និង function ដែលធ្វើបច្ចុប្បន្នភាព (update) វា។ នេះជាហេតុផលដែលយើងសរសេរ `const [count, setCount] = useState()`។ នេះគឺស្រដៀងនឹង `this.state.count` និង `this.setState` នៅក្នុង class, លើកលែងតែអ្នកទទួលពួកគេនៅក្នុងគូរ (pair)។ ប្រសិនបើអ្នកមិនស៊ាំ (familiar) ជាមួយនិង syntax ដែលយើងបានប្រើ, យើងនឹងត្រលប់ទៅវាវិញ [នៅផ្នែកខាងក្រោមនៃទំព័រនេះ](/docs/hooks-state.html#tip-what-do-square-brackets-mean)។

Now that we know what the `useState` Hook does, our example should make more sense:

```js{4,5}
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
```

We declare a state variable called `count`, and set it to `0`. React will remember its current value between re-renders, and provide the most recent one to our function. If we want to update the current `count`, we can call `setCount`.

>Note
>
>You might be wondering: why is `useState` not named `createState` instead?
>
>"Create" wouldn't be quite accurate because the state is only created the first time our component renders. During the next renders, `useState` gives us the current state. Otherwise it wouldn't be "state" at all! There's also a reason why Hook names *always* start with `use`. We'll learn why later in the [Rules of Hooks](/docs/hooks-rules.html).

## Reading State {#reading-state}

នៅពេលយើងចង់បង្ហាញ current count ​នៅក្នុង class, យើងអាន (read) ពី​ `this.state.count`៖

```js
  <p>You clicked {this.state.count} times</p>
```

នៅក្នុង function, យើងអាចប្រើ `count` ដោយ​ផ្ទាល់៖

```js
  <p>You clicked {count} times</p>
```

## Updating State {#updating-state}

នៅក្នុង class, យើងត្រូវការ call `this.setState()` ដើម្បីធ្វើបច្ចុប្បន្នភាព (update) `count` state៖

```js{1}
  <button onClick={() => this.setState({ count: this.state.count + 1 })}>
    Click me
  </button>
```

នៅក្នុង​ function, យើងមាន `setCount` និង `count` ជា variables រួចជាស្រេច ដូច្នេះយើងមិនត្រូវការ `this`៖

```js{1}
  <button onClick={() => setCount(count + 1)}>
    Click me
  </button>
```

## Recap {#recap}

Let's now **recap what we learned line by line** and check our understanding.

<!--
  I'm not proud of this line markup. Please somebody fix this.
  But if GitHub got away with it for years we can cheat.
-->
```js{1,4,9}
 1:  import React, { useState } from 'react';
 2:
 3:  function Example() {
 4:    const [count, setCount] = useState(0);
 5:
 6:    return (
 7:      <div>
 8:        <p>You clicked {count} times</p>
 9:        <button onClick={() => setCount(count + 1)}>
10:         Click me
11:        </button>
12:      </div>
13:    );
14:  }
```

* **Line 1:** We import the `useState` Hook from React. It lets us keep local state in a function component.
* **Line 4:** Inside the `Example` component, we declare a new state variable by calling the `useState` Hook. It returns a pair of values, to which we give names. We're calling our variable `count` because it holds the number of button clicks. We initialize it to zero by passing `0` as the only `useState` argument. The second returned item is itself a function. It lets us update the `count` so we'll name it `setCount`.
* **Line 9:** When the user clicks, we call `setCount` with a new value. React will then re-render the `Example` component, passing the new `count` value to it.

This might seem like a lot to take in at first. Don't rush it! If you're lost in the explanation, look at the code above again and try to read it from top to bottom. We promise that once you try to "forget" how state works in classes, and look at this code with fresh eyes, it will make sense.

### Tip: What Do Square Brackets Mean? {#tip-what-do-square-brackets-mean}

អ្នកប្រហែលជាកត់សម្គាល់វង់ក្រចកការ៉េនៅពេលយើងប្រកាស state variable៖

```js
  const [count, setCount] = useState(0);
```

ឈ្មោះនៅខាងឆ្វេងមិនមែនជាផ្នែកមួយនៃ React API នេាះទេ។ អ្នកអាចដាក់ឈ្មោះ state variables ផ្ទាល់ខ្លួនរបស់អ្នក។

```js
  const [fruit, setFruit] = useState('banana');
```

JavaScript syntax នេះត្រូវបានគេហៅថា ["array destructuring"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring)។ វាមានន័យថាយើងកំពុងបង្កើត variables ថ្មីពីរ `fruit` and `setFruit`, ដែល `fruit` គឺ set ទៅអោយតម្លៃទីមួយដែលបាន return ដោយ `useState`, ហើយ `setFruit` គឺទីពីរ។ វាស្មើនឹងកូដនេះ៖

```js
  var fruitStateVariable = useState('banana'); // Returns a pair
  var fruit = fruitStateVariable[0]; // First item in a pair
  var setFruit = fruitStateVariable[1]; // Second item in a pair
```

នៅពេលដែលយើងប្រកាស state variable ជាមួយ `useState`, វា returns មួយគូរ — array មួយជាមួយ
ធាតុពីរ។ ធាតុទីមួយគឺ តម្លៃ​​បច្ចុប្បន្ន, និង ទីពីរគឺ function ដែលអនុញ្ញាតឱ្យយើងធ្វើបច្ចុប្បន្នភាពវា។ ការប្រើ `[0]` និង `[1]` ដើម្បីចូលប្រើ (access) ពួកវា គឺមានការច្របូកច្របល់បន្តិច ពីព្រេាះពួកវាមានអត្ថន័យជាក់លាក់។ នេះជាមូលហេតុដែលយើងប្រើ array destructuring ជំនួសវិញ។

>ចំណាំ៖
>
>អ្នកប្រហែលជាចង់ដឹងចង់ឃើញពីរបៀប React ដឹង component មួយណាដែល `useState`
>អ្នកប្រហែលជាចង់ដឹងថាតើ React ដឹងថាសមាសធាតុមួយណាដែល `useState` ត្រូវនឹង ដែលយើងមិនបានកំពុង pass អ្វីទាំងអស់ ដូចជា `this` ត្រឡប់អោយ React។​ យើងនឹងឆ្លើយ [សំណួរនេះ](/docs/hooks-faq.html#how-does-react-associate-hook-calls-with-components)  និងផ្នែកផ្សេងទៀតជាច្រើននៅក្នុងផ្នែកសំណួរគេសួរញឹកញាប់។

### Tip: Using Multiple State Variables {#tip-using-multiple-state-variables}

ការប្រកាស state variables ជា pair នៃ `[something, setSomething]` គឺងាយស្រួលក្នុងការប្រើ ពីព្រេាះវាអនុញ្ញាតឱ្យយើងផ្តល់ឱ្យឈ្មេាះ *ផ្សេង* ទៅអោយ state variables ផ្សេងគ្នា ប្រសិនបើយើងចង់ប្រើច្រើនជាងមួយ៖

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
```

នៅក្នុង component ខាងលើ, យើងមាន `age`, `fruit`, និង `todos` ជា local variables, 
ហើយយើងអាចធ្វើបច្ចុប្បន្នភាពពួកវាមួយៗ៖

```js
  function handleOrangeClick() {
    // Similar to this.setState({ fruit: 'orange' })
    setFruit('orange');
  }
```

អ្នក **មិនចាំបាច់** ប្រើ state variables ច្រើនទេ។ State variables អាចផ្ទុក objects និង arrays បានល្អ, ដូច្នេះអ្នកនៅតែអាចដាក់ទិន្នន័យទាក់ទងក្រុមជាមួយគ្នា។ ទោះយ៉ាងណាក៏ដោយ, មិនដូច `this.setState` នៅក្នុង class, ការធ្វើបច្ចុប្បន្នភាព state variable តែងតែ *replace* វា
ជំនួសឱ្យការច្របាច់បញ្ចូល (merging) វា។

យើងផ្តល់នូវអនុសាសន៍ (recommendations) បន្ថែមទៀតលើការបែងចែក independent state variables [នៅក្នុងសំណួរគេសួរញឹកញាប់](/docs/hooks-faq.html#should-i-use-one-or-many-state-variables)។

## Next Steps {#next-steps}

នៅលើទំព័រនេះយើងបានរៀនអំពី Hooks មួយដែលផ្តល់ដោយ React, ត្រូវបានគេហៅថា `useState`។ 
ពេលខ្លះយើងក៏នឹងយោងទៅវាជា "State Hook"។ វាអនុញ្ញាតឱ្យយើងបន្ថែម local state ទៅអោយ React function components -- ដែលយើងបានធ្វើជាលើកដំបូងដែលមិនធ្លាប់មាន!

យើងក៏បានរៀនថែមបន្តិចផងដែរអំពី៖ អ្វីគឺជា Hooks។ Hooks គឺជា function ដែលអនុញ្ញាតឱ្យអ្នក "hook into" លក្ខណៈពិសេស (features) របស់ React ពី function components។ ឈ្មោះរបស់ពួកវាតែងតែចាប់ផ្តើមជាមួយ `use`, ហើយមាន Hooks ច្រើនទៀតដែលយើងមិនទាន់បានឃើញនៅឡើយ។

**ឥឡូវសូមបន្តដោយ [ការរៀន Hook បន្ទាប់៖ `useEffect`.](/docs/hooks-effect.html)** 
វាអនុញ្ញាតឱ្យអ្នកអនុវត្ត side effects នៅក្នុង components, ហើយវាស្រដៀងទៅនឹង lifecycle methods នៅក្នុង classes។
