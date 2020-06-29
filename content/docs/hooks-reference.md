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

`useReducer` ច្រើនតែចូលចិត្ត `useState` នៅពេលអ្នកមាន state logic ស្មុគស្មាញដែលពាក់ព័ន្ធនឹង sub-values ឬ នៅពេល state បន្ទាប់អាស្រ័យនឹង state មុន។ `useReducer` ក៏អនុញ្ញាតឱ្យអ្នកបង្កើនប្រសិទ្ធភាពការអនុវត្តសម្រាប់ components ដែលបង្កឱ្យមានការធ្វើបច្ចុប្បន្នភាពស៊ីជម្រៅ ពីព្រេាះ [អ្នកអាចបញ្ជូន `dispatch` down ជំនួសអោយ callbacks](/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down)។

នេះគឺជា ឧទាហរណ៍ counter ពីផ្នែក [`useState`](#usestate), ដែលបានសរសេរឡើងវិញដោយប្រើ reducer៖

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

>ចំណាំ
>
>React ធានាថា `dispatch` function identity គឺមានស្ថេរភាពនិងមិនផ្លាស់ប្តូរនៅលើការ re-renders។ នេះជាមូលហេតុដែលវាមានសុវត្ថិភាពក្នុងការលុបចេញពី the `useEffect` ឬ `useCallback` បញ្ជី dependency។

#### Specifying the initial state {#specifying-the-initial-state}

មានវិធីពីរយ៉ាងផ្សេងគ្នាដើម្បី initialize `useReducer` state។ អ្នកអាចជ្រើសរើសយកមួយអាស្រ័យលើករណីប្រើប្រាស់។ វិធីសាមញ្ញបំផុតគឺបញ្ជូន the initial state ជា argument ទី២៖

```js{3}
  const [state, dispatch] = useReducer(
    reducer,
    {count: initialCount}
  );
```

>ចំណាំ
>
> React មិនប្រើ the `state = initialState` argument convention ដែលពេញនិយមដោយ Redux។ តម្លៃ initial ជួនកាលត្រូវការការពឹងពាក់លើ props ហើយដូច្នេះត្រូវបានបញ្ជាក់ពីការ call Hook ជំនួសវិញ។ ប្រសិនបើអ្នកមានអារម្មណ៍យ៉ាងខ្លាំងអំពីរឿងនេះ, អ្នកអាច call `useReducer(reducer, undefined, reducer)` ដើម្បីធ្វើត្រាប់តាមឥរិយាបទ Redux, ប៉ុន្តែវាមិនត្រូវបានលើកទឹកចិត្តទេ។

#### Lazy initialization {#lazy-initialization}

អ្នកក៏អាចបង្កើត the initial state lazily។ ដើម្បីធ្វើដូចនេះ, អ្នកអាចបញ្ជូន `init` function មួយជា argument ទីបី។ The initial state នឹងត្រូវបាន set ទៅជា `init(initialArg)`។

វាអនុញ្ញាតឱ្យអ្នក extract the logic សម្រាប់ការគណនា the initial state នៅខាងក្រៅ the reducer។ នេះក៏ងាយស្រួលផងដែរសម្រាប់ការ reset the state នៅពេលក្រោយក្នុងការ response ទៅកាន់ action មួយ៖

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

ប្រសិនបើអ្នក return តម្លៃដូចគ្នាពី Reducer Hook មួយជា the current state, React នឹងចាកចេញដោយមិនមានការ render the children ឬ firing effects។ (React ប្រើ the [`Object.is` comparison algorithm](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#Description)។)

ចំណាំ​ថា React ប្រហែលនឹងត្រូវការ render component ជាក់លាក់នេាះម្តងទៀតមុនពេលការចាកចេញ។ នោះមិនគួរជាការព្រួយបារម្ភទេពីព្រោះ React នឹងមិនចាំបាច់ចូល "ជ្រៅ" ទៅក្នុង the tree ។ ប្រសិនបើអ្នកកំពុងធ្វើការគណនាខ្លាំងកំឡុងពេលការ render, អ្នកអាចបង្កើនប្រសិទ្ធភាពពួកវាជាមួយ `useMemo`។

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

បញ្ជូន inline callback មួយនិង array មួយនៃ dependencies។ `useCallback` នឹង return memoized version មួយនៃ the callback ដែលគ្រាន់តែផ្លាស់ប្តូរ ប្រសិនបើមួយនៃ the dependencies បានផ្លាស់ប្តូរ។ វាមានប្រយោជន៍នៅពេលកំពុងបញ្ជូន callbacks ដើម្បីបង្កើនប្រសិទ្ធភាព child components ដែលពឹងផ្អែកលើ reference ដែលមានសម្ថភាពដើម្បីការពារការ renders ដែលមិនចាំបាច់ (e.g. `shouldComponentUpdate`)។

`useCallback(fn, deps)` គឺស្មើនឹង `useMemo(() => fn, deps)`.

> ចំណាំ
>
> The array នៃ dependencies គឺមិនត្រូវបានបញ្ជូនជា arguments ទៅកាន់ callback។ តាមគំនិត, ទោះបីជា, នោះហើយជាអ្វីដែលពួកគេតំណាងឱ្យ៖ គ្រប់តម្លៃ referenced ដែលនៅខាងក្នុង callback ក៏គួរតែបង្ហាញនៅក្នុង the dependencies array។ នៅពេលអនាគត, advanced compiler គ្រប់គ្រាន់មួយអាចបង្កើត array ដោយស្វ័យប្រវត្តិ។
>
> យើងសូមណែនាំឱ្យប្រើច្បាប់ the [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ជាផ្នែកនៃ [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package របស់យើង។ វាព្រមាននៅពេល dependencies ត្រូវបានបញ្ជាក់មិនត្រឹមត្រូវនិងស្នើឱ្យដោះស្រាយ។

### `useMemo` {#usememo}

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

Returns តម្លៃ [memoized](https://en.wikipedia.org/wiki/Memoization) មួយ។

បញ្ជូន "create" function មួយ និង array នៃ dependencies មួយ។ `useMemo` នឹងគណនាឡើងវិញនូវតម្លៃ memoized នៅពេល dependency មួយនៃ dependencies ទាំងអស់បានផ្លាស់ប្តូរ។ ការបង្កើនប្រសិទ្ធិភាពនេះជួយអោយជៀសវាងការគណនាខ្លាំងទៅលើរាល់ការ render។

ចងចាំ​ថា function ដែលបានបញ្ជូនអោយ `useMemo` runs កំឡុងពេល rendering។ កុំធ្វើអ្វីនៅទីនោះ ដែលអ្នកនឹងមិនធ្វើនៅកំឡុងពេល rendering។ ឧទាហរណ៍, side effects ដែលជាកម្មសិទ្ធិរបស់​ `useEffect`, មិនមែន `useMemo`។

ប្រសិនបើគ្មាន array ត្រូវបានផ្តល់, តម្លៃថ្មីនឹងត្រូវបានគណនាលើរាល់ការ render។

**អ្នកអាច reply លើ `useMemo` ជាការបង្កើនប្រសិទ្ធិភាព, តែមិនមែនជាការធានារលើ logic នេាះទេ.** នៅពេលអនាគត, React អាចជ្រើសរើស "បំភ្លេច" នូវតម្លៃដែលបានចងចាំពីមុន ហើយគណនាពួកវាឡើងវិញលើការ render បន្ទាប់, e.g. ដើម្បី free memory សម្រាប់ offscreen components។ សរសេរ code របស់អ្នកដូច្នេះវានៅតែដំណើរការដោយគ្មាន `useMemo` — ហើយបន្ទាប់មកបន្ថែមវាដើម្បីបង្កើនប្រសិទ្ធភាពប្រតិបត្តិការ។

> ចំណាំ
>
> The array នៃ dependencies មិនត្រូវបានបញ្ជូនជា arguments ទៅកាន់ function។ តាមគំនិត, ទោះយ៉ាងណា, នោះហើយជាអ្វីដែលពួកគេ represent៖ គ្រប់តម្លៃ referenced នៅខាងក្នុង function ក៏គួរបង្ហាញនៅក្នុង the dependencies array។ នៅពេលអនាគត, compliler មួយដែលជឿនលឿនគ្រប់គ្រាន់អាចបង្កើត array នេះដោយស្វ័យប្រវត្តិ។
>
> យើងសូមណែនាំឱ្យប្រើប្រាស់ច្បាប់ [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ជាផ្នែកនៃ [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package របស់យើង។ វាព្រមាននៅពេលភាពអាស្រ័យត្រូវបានបញ្ជាក់មិនត្រឹមត្រូវនិងស្នើឱ្យមានការជួសជុល។

### `useRef` {#useref}

```js
const refContainer = useRef(initialValue);
```

`useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

ករណីប្រើប្រាស់ទូទៅគឺដើម្បី access child ជាបន្ទាន់៖

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

`useDebugValue` អាចត្រូវបានប្រើដើម្បីបង្ហាញ label សម្រាប់ custom hooks នៅក្នុង React DevTools។

ឧទាហរណ៍, ពិចារណាអំពី the `useFriendStatus` custom Hook ដែលបានពិពណ៌នានៅក្នុង ["Building Your Own Hooks"](/docs/hooks-custom.html)៖

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

> គន្លឹះ
>
> យើងមិនណែនាំឱ្យបន្ថែមតម្លៃ debug ទៅអោយគ្រប់ custom Hook ទាំងអស់នេាះទេ។ វាមានតម្លៃបំផុតសម្រាប់ custom Hooks ដែលផ្នែកមួយនៃ shared libraries។

#### Defer formatting debug values {#defer-formatting-debug-values}

ក្នុងករណីខ្លះការ format តម្លៃមួយសម្រាប់ការបង្ហាញអាចជាប្រតិបត្តិការ expensive។ វាក៏មិនចាំបាច់ដែរដរាបណា Hook ត្រូវបានត្រួតពិនិត្យ។

សម្រាប់ហេតុផលនេះ `useDebugValue` ទទួលយក formatting function ជា optional second parameter។ Function នេះ ត្រូវបានហៅតែក្នុងករណីដែល Hooks ត្រូវបានត្រួតពិនិត្យ។ វាទទួល តម្លៃ debug ជា parameter ហើយគួរតែ return តម្លៃបង្ហាញដែលត្រូវបាន format ។

ឧទាហរណ៍ custom Hook ដែល returned តម្លៃ `Date` អាចជៀសវាងការហៅ `toDateString` function ដែលមិនចាំបាច់ដោយការបញ្ជូន formatter ខាងក្រោម៖

```js
useDebugValue(date, date => date.toDateString());
```
