---
id: hooks-state
title: Using the Effect Hook
permalink: docs/hooks-effect.html
next: hooks-rules.html
prev: hooks-state.html
---

<<<<<<< HEAD
*Hooks* គឺជាការបន្ថែមថ្មីនៅក្នុង React ១៦.៨។ ពួកវាអនុញ្ញាតឱ្យអ្នកប្រើ state និង React features ផ្សេងៗដោយមិនចាំបាច់សរសេរ class។
=======
> Try the new React documentation.
> 
> These new documentation pages teach modern React and include live examples:
>
> - [Synchronizing with Effects](https://beta.reactjs.org/learn/synchronizing-with-effects)
> - [You Might Not Need an Effect](https://beta.reactjs.org/learn/you-might-not-need-an-effect)
> - [`useEffect`](https://beta.reactjs.org/reference/react/useEffect)
>
> The new docs will soon replace this site, which will be archived. [Provide feedback.](https://github.com/reactjs/reactjs.org/issues/3308)

*Hooks* are a new addition in React 16.8. They let you use state and other React features without writing a class.
>>>>>>> ba290ad4e432f47a2a2f88d067dacaaa161b5200

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

នៅក្នុង React class, អ្នកនឹងធម្មតា set up a subscription ក្នុង `componentDidMount`, ហើយ clean up វានៅក្នុង `componentWillUnmount`។ ឧទាហរណ៍, ឧបមាថាយើងមាន `ChatAPI` module ដែលអនុញ្ញាតឱ្យយើង subscribe ទៅកាន់ online status របស់ friend។ នេះជារបៀបដែលយើងអាច subscribe និងបង្ហាញ status នេាះដោយការប្រើ class៖

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

សូមកត់សម្គាល់ពីរបៀបដែល `componentDidMount` និង `componentWillUnmount` ត្រូវការឆ្លុះគ្នា។ Lifecycle methods បង្ខំយើងបំបែក logic នេះទេាះបីជាតាមគំនិតរបស់កូដដែលនៅក្នុងពួកវាទាំងពីគឹជាប់ពាក់ពន្ធ័ effect ដូចគ្នាឬតែមួយ។

>ចំណាំ
>
>អ្នកអានដែលមានភ្នែកឥន្ទ្រី (Eagle-eyed readers) អាចកត់សម្គាល់ថាឧទាហរណ៍នេះក៏ត្រូវការផងដែរនូវ `componentDidUpdate` method ដើម្បីឱ្យបានត្រឹមត្រូវពេញលេញ។ 
យើងនឹងមិនអើពើ (ignore) នឹងវាសម្រាប់ពេលនេះទេប៉ុន្តែយើងនឹងត្រឡប់មករកវានៅក្នុង [ផ្នែកក្រោយ](#explanation-why-effects-run-on-each-update) នៃទំព័រនេះ។

### Example Using Hooks {#example-using-hooks-1}

តោះមើលពីរបៀបដែលយើងអាចសរសេរ component ជាមួយ Hooks។

អ្នកប្រហែលកំពុងគិតថា យើងនឹងត្រូវការបំបែក effect ដើម្បីអនុវត្ត cleanup។ ប៉ុន្តែកូដសម្រាប់ការបន្ថែមនិងការយកចេញ subscription គឺទាក់ទងយ៉ាងខ្លាំងជាមួយ `useEffect` ដែលត្រូវបាន design ដើម្បីរក្សារវាជាមួយគ្នា។ ប្រសិនបើ effect របស់អ្នក return a function, React នឹង run វានៅពេលវាជាពេលដែលត្រូវ clean up៖

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

**ហេតុអ្វីយើងបាន return a function ពី effect របស់យើង?** នេះគឺជាយន្តការ optional cleanup សម្រាប់ effects។ រាល់ effect ប្រហែល return a function ដែល clearns up បន្ទាប់ពីវា។ នេះអនុញ្ញាតឱ្យយើងរក្សា logic សម្រាប់ការបន្ថែមនិងការយកចេញនូវ subscriptions នៅជិតគ្នា។ ពួកវាជាផ្នែកមួយនៃ effect ដូចគ្នា។

**តើពេលណាពិតប្រាកដដែល React clean up effect?** React អនុវត្ត cleanup នៅពេល component unmounts។ ទោះយ៉ាងណាក៏ដោយ, ដូចដែលយើងបានរៀនមុននេះ, effects run សម្រាប់រាល់ render និងមិនមែនគ្រាន់តែមួយទេ។ នេះ​ជាហេតុ React cleans up effect ពី previous render មុនពេល ការ run effect ពេលបន្ទាប់ *ផងដែរ*។ 
យើងនឹងពិភាក្សា [ហេតុអ្វីបានជាវាជួយជៀសវាង bugs](#explanation-why-effects-run-on-each-update) និង [របៀបក្នុងការដកខ្លួនចេញពីអាកប្បកិរិយានេះក្នុងករណីដែលវាបង្កើតជាបញ្ហានៃការអនុវត្ត](#tip-optimizing-performance-by-skipping-effects) ពេលក្រោយនៅខាងក្រោម។

>ចំណាំ
>
>យើងមិនចាំបាច់ត្រូវ return named function មួយពី effect។ យើងហៅវាថា `clearnup` នៅទីនេះដើម្បីបញ្ជាក់ពីគោលបំណងរបស់វា, ប៉ុន្តែអ្នកអាច return arrow function មួយ ឬ call អ្វីផ្សេង។

## Recap {#recap}

យើងបានរៀននិងយល់ហើយថា `useEffect` អនុញ្ញាតឱ្យយើងបង្ហាញប្រភេទផ្សេងៗគ្នានៃ side effects បន្ទាប់ពី component renders។ effects មួយចំនួន ប្រហែលទាមទារអោយ cleanup ដូច្នេះពួកវា return function៖

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

effects ផ្សេងទៀត ប្រហែលជាមិនមានតំណាក់កាល cleanup, ហើយមិន return អ្វីទាំងអស់។

```js
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

Effect Hook បង្រួមករណីប្រើទាំងពីរជាមួយ API តែមួយ។

-------------

**ប្រសិនបើអ្នកមានអារម្មណ៍ថាអ្នកមានការចាប់យកបានយ៉ាងសមរម្យទៅលើរបៀបដែល Effect Hook ដំណើរការ, ឬប្រសិនបើអ្នកមានអារម្មណ៍ថាធុញទ្រាន់, អ្នកអាចក្រឡេកទៅមើ់ល [ទំព័របន្ទាប់អំពីច្បាប់នៃ Hooks](/docs/hooks-rules.html) ឥឡូវ​នេះ។**

-------------

## Tips for Using Effects {#tips-for-using-effects}

យើងនឹងបន្តទំព័រនេះដោយមើលឱ្យស៊ីជម្រៅលើទិដ្ឋភាពមួយចំនួននៃ `useEffect` ដែល experienced React users នឹងទំនងជាចង់ដឹងចង់ឃើញអំពីវា។ កុំមានអារម្មណ៍ថាមានកាតព្វកិច្ចដើម្បីជីកចូលពួកគេឥឡូវនេះ។ អ្នកអាចត្រលប់មកទំព័រនេះវិញដើម្បីរៀនព័ត៌មានលម្អិតបន្ថែមអំពី Effect Hook។

### Tip: Use Multiple Effects to Separate Concerns {#tip-use-multiple-effects-to-separate-concerns}

បញ្ហាមួយក្នុងចំណោមបញ្ហាដែលយើងបានលើកឡើងនៅក្នុង [Motivation](/docs/hooks-intro.html#complex-components-become-hard-to-understand) សម្រាប់ Hooks គឺថា class lifecycle methods ជាញឹកញាមាន logic ដែលមិនទាក់ទងគ្នា, logic ដែលទាក់ទងគ្នា នឹងត្រូវបានបំបែកទៅជា methods ជាច្រើន។ នេះគឺជា component ដែលរួមបញ្ចូលគ្នារវាង counter និង friend status indicator logic ពី ឧទាហរណ៍មុន៖


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

ចំណាំរបៀប logic ដែល sets `document.title` ត្រូវបានបំបែករវាង `componentDidMount` និង `componentDidUpdate`។ Subscription logic ក៏ត្រូវបានពង្រឺកផងដែររវាង `componentDidMount` និង `componentWillUnmount`។ ហើយ `componentDidMount` មានកូដសម្រាប់ tasks ទាំងពីរ។

ដូច្នេះតើ Hooks អាចដោះស្រាយបញ្ហានេះយ៉ាងដូចម្តេច? គ្រាន់តែដូច [អ្នកអាចប្រើ *State* Hook ច្រើនជាងមួយ](/docs/hooks-state.html#tip-using-multiple-state-variables), អ្នកក៏អាចប្រើ effects ច្រើនផងដែរ។ នេះអនុញ្ញាតឱ្យយើងបែងចែក logic ដែលមិនមានទំនាក់ទំនងគ្នា ទៅកាន់ effects ផ្សេងៗគ្នា៖

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

**Hooks អនុញ្ញាតឱ្យយើងបំបែកកូដដោយផ្អែកលើអ្វីដែលវាកំពុងធ្វើ** ជាជាង lifecycle method name។ React នឹង apply *រាល់* effect ដែលបានប្រើយដោយ component, ក្នុងគោលបំណងដែលពួកវាត្រូវបានបញ្ជាក់។

### Explanation: Why Effects Run on Each Update {#explanation-why-effects-run-on-each-update}

ប្រសិនបើអ្នកធ្លាប់ប្រើ claasses, អ្នកប្រហែលជាកំពុងឆ្ងល់ថា ហេតុអ្វីបានជាតំណាក់កាល effect cleanup កើតឡើងបន្ទាប់ពីរាល់ពេល re-render, ហើយមិនត្រឹមតែម្តងកំឡុងពេល unmounting។ សូមក្រឡេកមើលឧទាហរណ៍ជាក់ស្តែង ដើម្បីមើលថាហេតុអ្វីបានជាការ design នេះជួយយើងបង្កើត component ដែលមាន bugs តិចជាង។

[មុននេះបន្តិចនៅលើទំព័រនេះ](#example-using-classes-1), យើងបានណែនាំឧទាហរណ៍មួយ `FriendStatus` component ដែលបង្ហាញ ទាំង friend ដែល online ឬ friend ដែលមិន online។ Class របស់យើង reads `friend.id` ពី​ `this.props`, subscribes ទៅកាន់ friend status បន្ទាប់ពី component mounts, ហើយ unsubscribes កំឡុងពេល unmounting៖

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

**ប៉ុន្តែ តើអ្វីក់ើតឡើងបើសិន `friend` prop ផ្លាស់ប្តូរ** កំឡុងពេល component គឺនៅលើអេក្រង់? Component របស់យើងនឹងបន្តការបង្ហាញ online status នៃ friend ផ្សេងៗ។ នេះគឺជា bug។ យើងក៏នឹងបង្កឱ្យមាន memory leak ឬក៏ crash នៅពេល unmounting ដែល unsubscribe call នឹងប្រើខុស friend ID ។

នៅក្នុង class component, យើងនឹងត្រូវការបន្ថែម `componentDidUpdate` ដើម្បី handle ករណីនេះ៖

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

ការភ្លេច handle `componentDidUpdate` គឺជាប្រភពទូទៅនៃ bugs នៅក្នុង React applications។

ឥឡូវពិចារណាពី version នៃ component នេះដែលប្រើ Hooks៖

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

វាមិនទទួលរងពី bug នេះទេ។ (ប៉ុន្តែយើងក៏មិនបានធ្វើការផ្លាស់ប្តូរអ្វីដែរ។)

មិនមានកូដអ្វីពិសេសម្រាប់ការ handle updates ពីព្រេាះ `useEffect` handles ពួកវា *by default*។ វា cleans up effect ពីមុនៗ មុនពេល apply effects បន្ទាប់។ ដើម្បីបង្ហាញរឿងនេះ, នេះគឺជាលំដាប់នៃ subscribe និង unsubscribe calls ដែល component នេះអាចផលិតលើសម៉ោង៖

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

ឥរិយាបថនេះធានានូវភាពស្ថិតស្ថេរ by default និង រារាំង bugs ដែលធម្មតា នៅក្នុង class components ដោយសារតែបាត់ update logic។

### Tip: Optimizing Performance by Skipping Effects {#tip-optimizing-performance-by-skipping-effects}

ករណី​ខ្លះ, cleaning up ឬ applying the effect បន្ទាប់ពីរាល់ពេល render អាចបង្កើតបញ្ហាការអនុវត្ត។ នៅក្នុង class components, យើងអាចដោះស្រាយវាដោយការសរសេរបន្ថែមនូវការប្រៀបធៀបជាមួយ `prevProps` ឬ `prevState` ដែលនៅខាងក្នុង `componentDidUpdate`៖

```js
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `You clicked ${this.state.count} times`;
  }
}
```

តំរូវការនេះគឺជារឿងធម្មតាដែលវាត្រូវបានបង្កើតឡើងនៅក្នុង `useEffect` Hook API។ អ្នកអាចប្រាប់ React ដើម្បី *skip* ការ apply effect ប្រសិនបើតម្លៃជាក់លាក់មិនបានផ្លាស់ប្តូររវាងការ re-renders។ ដើម្បីធ្វើដូច្នេះ, បញ្ជូន (pass) array មួយជា optional second argument មួយអោយទៅ `useEffect`៖

```js{3}
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

ក្នុងឧទាហរណ៍ខាងលើ, យើងបញ្ជូន `[count]` ជា argument ទីពីរ។ តើ​នេះ​មានន័យថា​ម៉េច​? ប្រសិនបើ `count` គឺ `5`, ហើយបន្ទាប់ component របស់យើង re-renders ជាមួយ `count` រហូតស្មើរនឹង `5`, React នឹងប្រៀបធៀប `[5]` ពី previous rende និង `[5]` ពី next render។ ពីព្រេាះ items ទាំងអស់នៅក្នុង arreay គឺដូចទៅនឹង (`5 === 5`), React នឹង skip the effect។ នោះហើយជាការបង្កើនប្រសិទ្ធភាពរបស់យើង។

នៅពេលយើង render ជាមួយ `count` បានធ្វើបច្ចុប្បន្នភាពទៅជា `6`, React នឹងប្រៀបធៀប items ក្នុង `[5]` array ពី previous render ជាមួយ items ក្នុង `[6]` array ពី next render។ លើកនេះ, React នឹង re-apply the effect ពីព្រេាះ `5 !== 6`។ ប្រសិនបើមាន items ច្រើននៅក្នុង array, React នឹង re-run the effect សូម្បី ប្រសិនបើមួយនៃពួកវាគឺខុសគ្នា។

នេះក៏ដំណើរការដែរសម្រាប់ effects ដែលមាន តំណាក់កាល cleanup មួយ៖

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

នៅពេលអនាគត, argument ទីពីរប្រហែលត្រូវបានបន្ថែមដោយស្វ័យប្រវត្តិដោយ build-time transformation មួយ។

>ចំណាំ
>
>ប្រសិនបើអ្នកប្រើការបង្កើនប្រសិទ្ធិភាពនេះ, ​ប្រាកដថា array រួមបញ្ចូល **តម្លៃទាំងអស់ពី component scope (ដូចជា props និង state) ដែលផ្លាស់ប្តូរគ្រប់ពេលវេលា និង ដែលត្រូវបានប្រើដោយ effect**។ បើមិនដូច្នេះទេ, កូដរបស់អ្នកនឹង យោងលើតម្លៃ state ពី previous renders។ ស្វែងយល់បន្ថែមអំពី [របៀបដោះស្រាយជាមួយ functions](/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) និង [អ្វីដែលត្រូវធ្វើនៅពេល​ array ផ្លាស់ប្តូរញឹកញាប់](/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often)។
>
>ប្រសិនបើអ្នកចង់ run effect និង clean up វា តែម្តង (លើ mount និង unmount), អ្នកអាចបញ្ជូន (pass) empty array (`[]`) ជា argument ទីពីរ។ នេះប្រាប់ React ថា effect របស់អ្នក មិនអាស្រ័យលើតម្លៃ *ណាមួយ* ពី props ឬ state, ដូច្នេះវាមិនចាំបាច់ re-run ទេ។ នេះមិនត្រូវបានដោះស្រាយជាករណីពិសេសទេ -- វាធ្វើតាមដោយផ្ទាល់ពីរបៀបដែល dependencies array តែងតែដំណើរការ។
>
>ប្រសិនបើអ្នកបញ្ជូន (pass) empty array (`[]`), props និង state នៅខាងក្នុង effect នឹងតែងតែមានតម្លៃតំបូងរបស់ពួកវា។ កំឡុងពេលបញ្ជូន (passing) `[]` ជា argument ទីពីរ គឺកាន់តែជិតនឹង `componentDidMount` និង `componentWillUnmount` mental model, តែងតែមាន [ដំណេាះស្រាយ](/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often) [ល្អប្រសើរ](/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) ដើម្បីជៀសវាង re-running effect ញឹកញាប់ពេក។ កុំភ្លេចថា React រារាំង ការ run `useEffect` រហូត បន្ទាប់ពី browser បាន painted, ដូច្នេះការធ្វើការងារបន្ថែមគឺមិនមានបញ្ហាទេ។
>
>យើងសូមណែនាំឱ្យប្រើច្បាប់ [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ដែលជាផ្នេកមួយនៃ [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package។ វាព្រមាន (warns) នៅពេល dependencies ត្រូវបានបញ្ជាក់មិនត្រឹមត្រូវនិងស្នើឱ្យមានការជួសជុល។

## Next Steps {#next-steps}

សូមអបអរសាទរ! នេះជាទំព័រមួយដ៏វែង, ប៉ុន្តែសង្ឃឹមថានៅចុងបញ្ចប់ សំណួរភាគច្រើនរបស់អ្នកអំពី effects ត្រូវបានឆ្លើយ។ អ្នកបានរៀននិងយល់ដឹងទាំង State Hook និង Effect Hook, ហើយនៅមាន *ច្រើន* ទៀតដែលអ្នកអាចធ្វើបានជាមួយពួកវាទាំងពីរនៅពេលរួមបញ្ចូលគ្នា។ ពួកវា cover ភាគច្រើនលើករណីនៃការប្រើប្រាស់​ classes -- និងកន្លែងដែលពួកវាមិនប្រើ, អ្នកប្រហែលយល់ឃើញថា [additional Hooks](/docs/hooks-reference.html) មានប្រយោជន៍។

យើងក៏ចាប់ផ្តើមមើលពីរបៀបដែល Hooks ដោះស្រាយបញ្ហាដែលបានគូសបញ្ជាក់នៅក្នុង [Motivation](/docs/hooks-intro.html#motivation)។ យើងបានឃើញពីរបៀបដែល effect cleanup ជៀសវាងការ duplicate នៅក្នុង `componentDidUpdate` និង `componentWillUnmount`, នាំយកកូដដែលទាក់ទងគ្នាអោយកាន់តែជិតឌិត, និងជួយយើងជៀសវាង bugs, យើងក៏បានឃើញផងដែរពីរបៀបដែលយើងអាចបំបែក effect ដោយគោលបំណងរបស់ពួកវា, ដែលគឺជាអ្វីមួយដែលយើងមិនអាចធ្វើនៅក្នុង classes ទាំងអស់។

នៅពេលនេះអ្នកអាចនឹងត្រូវបានចោទសួរពីរបៀបដែល Hooks ដំណើរការ។ តើធ្វើដូចម្តេចទើប React អាចដឹងថាការ call `useSate` មួយណាត្រូវនឹង state variable មួយណារវាង re-renders? តើ React "ផ្គូរផ្គង (match up)" effects ពីមុននិងបន្ទាប់នៅលើរាល់ការធ្វើបច្ចុប្បន្នភាពយ៉ាងដូចម្តេច? **នៅទំព័របន្ទាប់យើងនឹងរៀនអំពី [វិធាននៃ Hooks](/docs/hooks-rules.html) ពួកវាចាំបាច់ក្នុងការធ្វើឱ្យ Hooks ធ្វើការ។**
