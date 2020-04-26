---
id: hooks-reference
title: Hooks API Reference
permalink: docs/hooks-reference.html
prev: hooks-custom.html
next: hooks-faq.html
---

*Hooks* គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។

ទំព័រនេះពិពណ៌នាពី APIs សម្រាប់ built-in Hooks នៅក្នុង React។

ប្រសិនបើអ្នកថ្មីជាមួយ Hooks, អ្នកប្រហែលជាចង់ពិនិត្យមើល [the overview](/docs/hooks-overview.html) ជាមុន។ អ្នកក៏អាចរកឃើញព័ត៌មានមានប្រយោជន៍នៅក្នុងផ្នែក [សំណួរ​ដែលគេ​ច្រើន​សួរ](/docs/hooks-faq.html)។

- [Basic Hooks](#basic-hooks)
  - [`useState`](#usestate)
  - [`useEffect`](#useeffect)
  - [`useContext`](#usecontext)
- [Additional Hooks](#additional-hooks)
  - [`useReducer`](#usereducer)
  - [`useCallback`](#usecallback)
  - [`useMemo`](#usememo)
  - [`useRef`](#useref)
  - [`useImperativeHandle`](#useimperativehandle)
  - [`useLayoutEffect`](#uselayouteffect)
  - [`useDebugValue`](#usedebugvalue)

## Basic Hooks {#basic-hooks}

### `useState` {#usestate}

```js
const [state, setState] = useState(initialState);
```

Returns stateful value មួយ, និង function មួយដើម្បីធ្វើបច្ចុប្បន្នភាពវា។

កំឡុងពេល the initial render, the returned state គឺដូចគ្នានឹងតម្លៃដែលបានបញ្ជូន (pass) ជា argument ទីមួយ (`initialState`)។

The `setState` function ត្រូវបានប្រើដើម្បីធ្វើបច្ចុប្បន្នភាព state។ វាទទួលយក state value ថ្មីមួយ ហើយ enqueues re-render នៃ component។

```js
setState(newState);
```

កំឡុងពេល re-renders ជាបន្តបន្ទាប់, តម្លៃដែលបាន return តំបូងដោយ `useState` នឹង
តែងតែជា state ថ្មីបំផុតបន្ទាប់ពីអនុវត្តបច្ចុប្បន្នភាព។

>ចំណាំ
>
> React ធានាថា ការកំណត់ `setState` function គឺ stable និងមិនផ្លាស់ប្តូរលើ re-renders។ នេះជាមូលហេតុដែលអាចលុបចោលបានពី `useEffect` or `useCallback` តារាង dependency។

#### Functional updates {#functional-updates}

ប្រសិនបើ new state ត្រូវបានគណនាដោយការប្រើ state ពីមុន, អ្នកអាចបញ្ជូន (pass) function ទៅអោយ `setState`។ Function នឹងទទួលតម្លៃពីមុន, ហើយ return តម្លៃដែលបានធ្វើបច្ចុប្បន្នភាព។ នេះជាឧទាហរណ៍នៃ counter component ដែលប្រើ form ទាំងពីរនៃ `setState`៖

```js
function Counter({initialCount}) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
    </>
  );
}
```

ប៊ូតុង "+" និង "-" ប្រើ functional form, ពីព្រេាះ value ដែលបានធ្វើបច្ចុប្បន្នភាពផ្អែកលើតម្លៃមុន។ ប៉ុន្តែប៊ូតុង "Reset" ប្រើ form ធម្មតា, ពីព្រេាះវាតែងតែ sets the count ត្រឡប់ទៅតម្លៃដំបូងវិញ។

ប្រសិនបើ update function returns នូវតម្លៃដូចគ្នានឹង current state, the subsequent rerender នឹងត្រូវរំលង (skip) ទាំងស្រុង។

> ចំណាំ
>
> មិនដូច `setState` method ដែលនៅក្នុង class components, `useState` មិន merge នូវ update objects ដោយស្វ័យប្រវត្តិឡើយ។ អ្នកអាចចម្លងឥរិយាបថនេះឡើងវិញដោយការរួមបញ្ចូលគ្នានូវតម្រង់ funtion updater ជាមួយ object spread syntax៖
>
> ```js
> setState(prevState => {
>   // Object.assign would also work
>   return {...prevState, ...updatedValues};
> });
> ```
>
> ជម្រើសផ្សេងទៀតគឺ `useReducer`, ដែលកាន់តែសមស្របសម្រាប់ការគ្រប់គ្រង state objects ដែលមា​ន sub-values ច្រើន។

#### Lazy initial state {#lazy-initial-state}

The `initialState` argument គឺជា state ដែលបានប្រើកំឡុងពេល render តំបូង។ ក្នុងការ renders ជាបន្តបន្ទាប់, វាត្រូវបានគេមិនយកចិត្តទុកដាក់។ ប្រសិនបើ initial state គឺជាលទ្ធផលនៃការគណនាខ្លាំង, អ្នកអាចផ្តល់នូវ function ជំនួសវិញ, ដែលនឹងត្រូវបានប្រតិបត្តិតែលើការ render តំបូងប៉ុណ្ណោះ៖

```js
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

#### Bailing out of a state update {#bailing-out-of-a-state-update}

ប្រសិនបើអ្នកធ្វើបច្ចុប្បន្នភាព State Hook អោយតម្លៃដូចគ្នានឹង current state, React នឹងធានាអោយនៅក្រៅដោយមិនធ្វើការ render children ឬ firing effects។ (React ប្រើ [`Object.is` comparison algorithm](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#Description)។)

ចំណាំ​ថា React នៅតែត្រូវការ render component ជាក់លាក់នេាំម្តងទៀតមុនពេលការធានាអោយនៅក្រៅ។ នោះមិនគួរជាការព្រួយបារម្ភទេ ពីព្រោះ React នឹងមិនចាំបាច់ទៅ "កាន់តែជ្រៅ" ទៅក្នុង tree។ ប្រសិនបើអ្នកកំពុងធ្វើការគណនាខ្លាំងនៅពេលធ្វើការ render, អ្នកអាចបង្កើនប្រសិទ្ធភាពពួកវាជាមួយ `useMemo`។

### `useEffect` {#useeffect}

```js
useEffect(didUpdate);
```

ទទួល function ដែលមានភាពចាំបាច់, possibly effectful code។

Mutations, subscriptions, timers, logging, និង side effects ផ្សេងៗទៀតមិនត្រូវបានអនុញ្ញាតនៅក្នុង body នៃ function componen (សំដៅដល់ _ដំណាក់កាល render_ របស់ React)។ ការធ្វើដូច្នេះនឹងនាំឱ្យមាន confusing bugs និង ភាពមិនស៊ីចង្វាក់គ្នា ក្នុង UI។

ជំនួស, ប្រើ `useEffect`។ function ដែលបានបញ្ជូន (pass) ទៅកាន់ `useEffect` និង run បន្ទាប់ពីការ render ត្រូវបាន commit ទៅកាន់ screen។ គិត​អំពី effects ជាការរត់គេចខ្លួនពី React's purely functional world ចូលទៅក្នុងពិភពចាំបាច់។

ដោយ default, effects run បន្ទាប់ពីរាល់ការ render ត្រូវបានបញ្ចប់, ប៉ុន្តែអ្នកអាចជ្រើសរើសដើម្បី fire ពួកវា [តែនៅពេលដែលតម្លៃជាក់លាក់បានផ្លាស់ប្តូរ](#conditionally-firing-an-effect)។

#### Cleaning up an effect {#cleaning-up-an-effect}

ជាញឹកញាប់, effects បង្កើត resources ដែលត្រូវការសម្អាត (clean up) មុនពេល component ចាកចេញពី screen, ដូចជា subscription ឬ timer ID។ ដើម្បីធ្វើដូចនេះ, function ដែលបានបញ្ជូនទៅ  `useEffect` អាច return clean-up function វិញ។ ឧទាហរណ៍, ដើម្បីបង្កើត subscription មួយ៖

```js
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  };
});
```

The clean-up function runs មុន component ត្រូវបានលុបពី UI ដើម្បីការពារ memory leaks។ បន្ថែម, ប្រសិនបើ component មួយ renders ច្រើនដង (ដូចដែលពួកវាធ្វើជាធម្មតា), **previous effect ត្រូវបានសម្អាតមុនពេលការប្រតិបត្តិ next effect**។ ក្នុងឧទាហរណ៍របស់យើង, នេះ​មានន័យថា subscription ថ្មីមួយតត្រូវបានបង្កើតនៅរាល់ការធ្វើបច្ចុប្បន្នភាព។ ដើម្បីចៀសវាងការ firing effect លើរាល់ការធ្វើបច្ចុប្បន្នភាព, យោងទៅផ្នែកបន្ទាប់។

#### Timing of effects {#timing-of-effects}

មិនដូច `componentDidMount` និង `componentDidUpdate`, the function ដែលបានបញ្ជូនទៅ `useEffect` fires **បន្ទាប់ពី** layout និង paint, ក្នុងកំឡុងពេល event ពន្យាពេល។ នេះធ្វើឱ្យវាសមស្របសម្រាប់ side effects ទូទៅជាច្រើន, ដូចជាការ set up subscriptions និង event handlers, ពីព្រោះប្រភេទការងារភាគច្រើនមិនគួរ block the browser ពីការធ្វើបច្ចុប្បន្នភាព screen។

ទោះយ៉ាងណាក៏ដោយ, មិនមែនសុទ្ធតែ effects ទាំងអស់អាចត្រូវបានពន្យាលពេលនេាះទេ។ ឧទាហរណ៍, DOM mutation មួយដែល visible ទៅកាន់ user ត្រូវតែ fire synchronously មុនពេល the next paint ដូច្នេះ user មិនយល់ភាពមិនត្រូវគ្នា។ (The distinction is conceptually similar to passive versus active event listeners.) For these types of effects, React ផ្តល់នូវ Hook មួយបន្ថែមទៀតដែលគេហៅថា [`useLayoutEffect`](#uselayouteffect)។ វាមាន signature ដូចគ្នានឹង `useEffect`, and only differs in when it is fired។

ទោះបីជា `useEffect` ត្រូវបានពន្យាពេលរហូតដល់បន្ទាប់ពី the browser has painted, វាត្រូវបានធានាថា fire មុនការ renders ថ្មីៗ។ React នឹងតែងតែ flush នូវ effects របស់ render ពីមុន មុនពេលចាប់ផ្តើមនូវ ការ update ថ្មី។

#### Conditionally firing an effect {#conditionally-firing-an-effect}

ឥរិយាបទដើមសម្រាប់ effects គឺ fire the effect បន្ទាប់ពីរាល់ការ render ត្រូវបានបញ្ចប់។ មធ្យោបាយនេះ effect គឺតែងតែត្រូវបានបង្កើតឡើងវិញ ប្រសិនបើមួយនៃ dependencies របស់វាផ្លាស់ប្តូរ។

ទោះយ៉ាងណាក៏ដោយ, នេះប្រហែលជា overkill ក្នុងករណីមួយចំនួន, ដូចជាឧទាហរណ៍ subscription ពីផ្នែកមុន។ យើងមិនចាំបាច់បង្កើត subscription ថ្មីលើរាល់ការធ្វើបច្ចុប្បន្នភាពទេ, លុះត្រាតែ `source` prop ត្រូវបានផ្លាស់ប្តូរ។

ដើម្បី implement ដូចនេះ, បញ្ជូន argument ទីពីរទៅកាន់ `useEffect` ដែលគឺជា array នៃតម្លៃដែល effect ផ្អែកលើ។ ឧទាហរណ៍ដែលបានធ្វើបច្ចុប្បន្នភាពរបស់យើងឥឡូវនេះមើលទៅដូចនេះ៖

```js
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```

ឥឡូវ​នេះ the subscription នឹងត្រូវបានបង្កើតឡើងវិញតែនៅពេលដែល `props.source` ផ្លាស់ប្តូរ។

>ចំណាំ
>
>ប្រសិនបើអ្នកប្រើការបង្កើនប្រសិទ្ធិភាព (o​ptimization) នេះ, ធ្វើ​ឱ្យ​ប្រាកដ​ថា array រួមបញ្ចូល **តម្លៃទាំងអស់ពី scope របស់ component (ដូចជា props និង state) ដែលផ្លាស់ប្តូរតាមពេលនិងដែលបានប្រើដោយ effect**។ បើមិនដូច្នេះទេ, កូដរបស់អ្នករបស់អ្នកនឹងយោងលើតម្លៃចាស់ពី previous renders។ ស្វែងយល់បន្ថែមអំពី [របៀបដោះស្រាយជាមួយ functions](/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) និងអ្វីដែលត្រូវធ្វើនៅពេល [តម្លៃ array ផ្លាស់ប្តូរញឹកញាប់ពេក](/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often)។
>
>ប្រសិនបើអ្នកចង់ run effect មួយហើយ clean វាតែម្តងគត់ (នៅពេល mount និង unmount), អ្នកអាចបញ្ជូន array ទទេរមួយ (`[]`) ជា argument ទីពីរ។ នេះប្រាប់ React ថា effect របស់អ្នកមិនផ្អែកលើតម្លៃ *ណាមួយ* ពី props ឬ state, ដូច្នេះវាមិនចាំដើម្បី re-run។ នេះមិនត្រូវបានដោះស្រាយជាករណីពិសេសទេ -- 
វាធ្វើតាមដោយផ្ទាល់ពីរបៀបដែល dependencies array តែងតែដំណើរការ។
>ប្រសិនបើយអ្នកបញ្ជូន array ទទេរមួយ (`[]`), props និង state នៅខាងក្នុង effect នឹងតែងតែមានតម្លៃ initial របស់ពួកវា។ ខណៈពេល កំពុងបញ្ជូន `[]` ជា argument ទីពីរ គឺកាន់តែខិតទៅជិតគ្រួសារ `componentDidMount` និង `componentWillUnmount` mental model, ជាធម្មតាមាន [better](/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) [solutions](/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often) ដើម្បីជៀសវាង re-running effect ញឹកញាប់ពេក។ ផងដែរ, កុំភ្លេចថា React ពន្យាពេល running `useEffect` រហូតដល់បន្ទាប់ពី browser has painted, ដូច្នេះការធ្វើការងារបន្ថែមគឺមិនមានបញ្ហាទេ។
>
>
>យើងសូមណែនាំឱ្យប្រើច្បាប់ [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) 
ជាផ្នែកមួយនៃ [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package របស់យើង។ វាព្រមាននៅពេល dependencies ត្រូវបានបញ្ជាក់មិនត្រឹមត្រូវនិងស្នើឱ្យដោះស្រាយ។

The array នៃ dependencies មិនត្រូវបានបញ្ជូនជា arguments ទៅកាន់ effect function។ តាមគំនិត, 
ទោះបីជា, នោះហើយជាអ្វីដែលពួកគេតំណាងឱ្យ៖ រាល់តម្លៃដែលបានយោងនៅខាងក្នុង effect function គួរតែ appear ផងដែរនៅក្នុង dependencies array។ នៅពេលអនាគត, sufficiently advanced compiler មួយអាចបង្កើត array នេះដោយស្វ័យប្រវត្តិ។

### `useContext` {#usecontext}

```js
const value = useContext(MyContext);
```

ទទួលយក context object មួយ (តម្លៃដែលបាន return ពី from `React.createContext`) និង returns តម្លៃ context បច្ចុប្បន្ន សម្រាប់ context នេាះ។ តម្លៃ context បច្ចុប្បន្ន​ គឺត្រូវបានកំណត់ដោយ `តម្លៃ` prop នៃ `<MyContext.Provider>` ជិតបំផុតដែលនៅខាងលើ កំពុង call component នៅក្នុង tree។

នៅពេលដែល nearest `<MyContext.Provider>` component ខាងលើធ្វើបច្ចុប្បន្នភាព, Hook នេះនឹង trigger នូវការ rerender ជាមួយ `តម្លៃ` context ចុងក្រោយ ដែលបានបញ្ជូនទៅកាន់ `MyContext` provider នេាះ។ តេាះបីជា ancester ប្រើ [`React.memo`](/docs/react-api.html#reactmemo) ឬ [`shouldComponentUpdate`](/docs/react-component.html#shouldcomponentupdate), rerender 
នឹងនៅតែកើតឡើងចាប់ផ្តើមនៅ component ខ្លួនវាផ្ទាល់ដោយការប្រើ `useContext`។

កុំភ្លេចថា​ argument ទៅកាន់ `useContext` ត្រូវតែជា *context object ខ្លួនវាផ្ទាល់*៖

 * **ត្រឹមត្រូវ:** `useContext(MyContext)`
 * **មិន​ត្រឹមត្រូវ:** `useContext(MyContext.Consumer)`
 * **មិន​ត្រឹមត្រូវ:** `useContext(MyContext.Provider)`

Component ដែលកំពុង call `useContext` នឹងតែងតែ re-render នៅពេលដែល តម្លៃ context ផ្លាស់ប្តូរ។ ប្រសិនបើការ re-render the component គឺ ធ្ងន់, អ្នកអាច [បង្កើនប្រសិទ្ធភាពវាដោយប្រើ memoization](https://github.com/facebook/react/issues/15156#issuecomment-474590693)។

>គន្លឹះ
>
>ប្រសិនបើអ្នកសុាំជាមួយនឹង context API មុន Hooks, `useContext(MyContext)` គឺស្មើនឹង `static contextType = MyContext` នៅក្នុង class មួយ, ឬ `<MyContext.Consumer>`។
>
>`useContext(MyContext)` គ្រាន់តែអនុញ្ញាតឱ្យអ្នក *read* the context និង subscribe ទៅកាន់ការផ្លាស់ប្តូររបស់វា។ អ្នកនៅតែត្រូវការ `<MyContext.Provider>` ខាងលើនៅក្នុង tree ដើម្បី *ផ្តល់* តម្លៃសម្រាប់ context នេះ។

**ដាក់វាបញ្ចូលគ្នាជាមួយ Context.Provider**
```js{31-36}
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);

  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );
}
```
ឧទាហរណ៍នេះត្រូវបានកែប្រែសម្រាប់ hooks ពី ឧទាហរណ៍មុននៅក្នុង [Context Advanced Guide](/docs/context.html), ដែលអ្នកអាចស្វែងរកព័ត៌មានបន្ថែមអំពីពេលវេលានិងរបៀបប្រើ Context។


## Additional Hooks {#additional-hooks}

Hooks ខាងក្រោម គឺជា variants នៃមូលដ្ឋានគ្រឹះពីផ្នែកមុន, ឬត្រូវការសម្រាប់ករណីជាក់លាក់។ កុំតប់ប្រមល់អំពីការរៀនវានៅខាងមុខ។

### `useReducer` {#usereducer}

```js
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

ជំរើសមួយដើម្បី [`useState`](#usestate)។ ទទួលយក reducer មួយនៃប្រភេទ `(state, action) => newState`, ហើយ returns state ដែលបា​នផ្គូផ្គងបច្ចុប្បន្ន (the current state paired) ជាមួយ `dispatch` method។ (ប្រសិនបើអ្នកសុាំជាមួយនឹង Redux, អ្នកដឹងពីរបៀបដែលវាដំណើរការ។)

`useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one. `useReducer` also lets you optimize performance for components that trigger deep updates because [you can pass `dispatch` down instead of callbacks](/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down).

Here's the counter example from the [`useState`](#usestate) section, rewritten to use a reducer:

```js
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

>Note
>
>React guarantees that `dispatch` function identity is stable and won't change on re-renders. This is why it's safe to omit from the `useEffect` or `useCallback` dependency list.

#### Specifying the initial state {#specifying-the-initial-state}

There are two different ways to initialize `useReducer` state. You may choose either one depending on the use case. The simplest way is to pass the initial state as a second argument:

```js{3}
  const [state, dispatch] = useReducer(
    reducer,
    {count: initialCount}
  );
```

>Note
>
>React doesn’t use the `state = initialState` argument convention popularized by Redux. The initial value sometimes needs to depend on props and so is specified from the Hook call instead. If you feel strongly about this, you can call `useReducer(reducer, undefined, reducer)` to emulate the Redux behavior, but it's not encouraged.

#### Lazy initialization {#lazy-initialization}

You can also create the initial state lazily. To do this, you can pass an `init` function as the third argument. The initial state will be set to `init(initialArg)`.

It lets you extract the logic for calculating the initial state outside the reducer. This is also handy for resetting the state later in response to an action:

```js{1-3,11-12,19,24}
function init(initialCount) {
  return {count: initialCount};
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  return (
    <>
      Count: {state.count}
      <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>
        Reset
      </button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

#### Bailing out of a dispatch {#bailing-out-of-a-dispatch}

If you return the same value from a Reducer Hook as the current state, React will bail out without rendering the children or firing effects. (React uses the [`Object.is` comparison algorithm](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#Description).)

Note that React may still need to render that specific component again before bailing out. That shouldn't be a concern because React won't unnecessarily go "deeper" into the tree. If you're doing expensive calculations while rendering, you can optimize them with `useMemo`.

### `useCallback` {#usecallback}

```js
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

Returns a [memoized](https://en.wikipedia.org/wiki/Memoization) callback.

Pass an inline callback and an array of dependencies. `useCallback` will return a memoized version of the callback that only changes if one of the dependencies has changed. This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders (e.g. `shouldComponentUpdate`).

`useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.

> Note
>
> The array of dependencies is not passed as arguments to the callback. Conceptually, though, that's what they represent: every value referenced inside the callback should also appear in the dependencies array. In the future, a sufficiently advanced compiler could create this array automatically.
>
> We recommend using the [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) rule as part of our [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It warns when dependencies are specified incorrectly and suggests a fix.

### `useMemo` {#usememo}

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

Returns a [memoized](https://en.wikipedia.org/wiki/Memoization) value.

Pass a "create" function and an array of dependencies. `useMemo` will only recompute the memoized value when one of the dependencies has changed. This optimization helps to avoid expensive calculations on every render.

Remember that the function passed to `useMemo` runs during rendering. Don't do anything there that you wouldn't normally do while rendering. For example, side effects belong in `useEffect`, not `useMemo`.

If no array is provided, a new value will be computed on every render.

**You may rely on `useMemo` as a performance optimization, not as a semantic guarantee.** In the future, React may choose to "forget" some previously memoized values and recalculate them on next render, e.g. to free memory for offscreen components. Write your code so that it still works without `useMemo` — and then add it to optimize performance.

> Note
>
> The array of dependencies is not passed as arguments to the function. Conceptually, though, that's what they represent: every value referenced inside the function should also appear in the dependencies array. In the future, a sufficiently advanced compiler could create this array automatically.
>
> We recommend using the [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) rule as part of our [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It warns when dependencies are specified incorrectly and suggests a fix.

### `useRef` {#useref}

```js
const refContainer = useRef(initialValue);
```

`useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

A common use case is to access a child imperatively:

```js
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

Essentially, `useRef` is like a "box" that can hold a mutable value in its `.current` property.

You might be familiar with refs primarily as a way to [access the DOM](/docs/refs-and-the-dom.html). If you pass a ref object to React with `<div ref={myRef} />`, React will set its `.current` property to the corresponding DOM node whenever that node changes.

However, `useRef()` is useful for more than the `ref` attribute. It's [handy for keeping any mutable value around](/docs/hooks-faq.html#is-there-something-like-instance-variables) similar to how you'd use instance fields in classes.

This works because `useRef()` creates a plain JavaScript object. The only difference between `useRef()` and creating a `{current: ...}` object yourself is that `useRef` will give you the same ref object on every render.

Keep in mind that `useRef` *doesn't* notify you when its content changes. Mutating the `.current` property doesn't cause a re-render. If you want to run some code when React attaches or detaches a ref to a DOM node, you may want to use a [callback ref](/docs/hooks-faq.html#how-can-i-measure-a-dom-node) instead.


### `useImperativeHandle` {#useimperativehandle}

```js
useImperativeHandle(ref, createHandle, [deps])
```

`useImperativeHandle` customizes the instance value that is exposed to parent components when using `ref`. As always, imperative code using refs should be avoided in most cases. `useImperativeHandle` should be used with [`forwardRef`](/docs/react-api.html#reactforwardref):

```js
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);
```

In this example, a parent component that renders `<FancyInput ref={inputRef} />` would be able to call `inputRef.current.focus()`.

### `useLayoutEffect` {#uselayouteffect}

The signature is identical to `useEffect`, but it fires synchronously after all DOM mutations. Use this to read layout from the DOM and synchronously re-render. Updates scheduled inside `useLayoutEffect` will be flushed synchronously, before the browser has a chance to paint.

Prefer the standard `useEffect` when possible to avoid blocking visual updates.

> Tip
>
> If you're migrating code from a class component, note `useLayoutEffect` fires in the same phase as `componentDidMount` and `componentDidUpdate`. However, **we recommend starting with `useEffect` first** and only trying `useLayoutEffect` if that causes a problem.
>
>If you use server rendering, keep in mind that *neither* `useLayoutEffect` nor `useEffect` can run until the JavaScript is downloaded. This is why React warns when a server-rendered component contains `useLayoutEffect`. To fix this, either move that logic to `useEffect` (if it isn't necessary for the first render), or delay showing that component until after the client renders (if the HTML looks broken until `useLayoutEffect` runs).
>
>To exclude a component that needs layout effects from the server-rendered HTML, render it conditionally with `showChild && <Child />` and defer showing it with `useEffect(() => { setShowChild(true); }, [])`. This way, the UI doesn't appear broken before hydration.

### `useDebugValue` {#usedebugvalue}

```js
useDebugValue(value)
```

`useDebugValue` can be used to display a label for custom hooks in React DevTools.

For example, consider the `useFriendStatus` custom Hook described in ["Building Your Own Hooks"](/docs/hooks-custom.html):

```js{6-8}
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  // Show a label in DevTools next to this Hook
  // e.g. "FriendStatus: Online"
  useDebugValue(isOnline ? 'Online' : 'Offline');

  return isOnline;
}
```

> Tip
>
> We don't recommend adding debug values to every custom Hook. It's most valuable for custom Hooks that are part of shared libraries.

#### Defer formatting debug values {#defer-formatting-debug-values}

In some cases formatting a value for display might be an expensive operation. It's also unnecessary unless a Hook is actually inspected.

For this reason `useDebugValue` accepts a formatting function as an optional second parameter. This function is only called if the Hooks are inspected. It receives the debug value as a parameter and should return a formatted display value.

For example a custom Hook that returned a `Date` value could avoid calling the `toDateString` function unnecessarily by passing the following formatter:

```js
useDebugValue(date, date => date.toDateString());
```
