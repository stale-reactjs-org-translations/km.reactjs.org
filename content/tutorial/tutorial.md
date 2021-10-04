---
id: tutorial
title: "Tutorial: ការណែនាំអំពី React"
layout: tutorial
sectionid: tutorial
permalink: tutorial/tutorial.html
redirect_from:
  - "docs/tutorial.html"
  - "docs/why-react.html"
  - "docs/tutorial-ja-JP.html"
  - "docs/tutorial-ko-KR.html"
  - "docs/tutorial-zh-CN.html"
---

Tutorial នេះសម្រាប់ទាំងអ្នកដែលមានហើយនិងគ្មានចំណេះដឹងពី React ទាល់តែសេាះ។

## មុនពេលដែលយើងចាប់ផ្តើម tutorial {#before-we-start-the-tutorial}

យើងនិងបង្កើតហ្គេមដ៏តូចមួយនៅក្នុង tutorial នេះ។ **អ្នកអាច skip វាបានពីព្រេាះអ្នកមិនមែនជាអ្នកបង្កើតហ្គេមនេាះទេ -- ប៉ុន្តែអ្នកគួរតែសាកល្បងវា។**  Techniques ដែលអ្នកនិងរៀននៅក្នុង tutorial នេះគឺមូលដ្ឋានគ្រឺះដើម្បីបង្កើត React apps ហើយនិងការយល់ដឹងយ៉ាងសុីជម្រៅពី React។

>ពត៌មានជំនួយ
>
>tutorial នេះគេ design សម្រាប់អ្នកដែលចូលចិត្ត**រៀនដោយការអនុវត្តន៍**។ ប្រសិនជាអ្នកចង់រៀន concept មូលដ្ឋានតំបូងរបស់​ React, អ្នកអាចឆែកមើល [step-by-step guide](/docs/hello-world.html) របស់យើងបាន។ អ្នកប្រាកដជាយល់ឃើញថា​​ tutorial នេះហើយនិង step-by-step guide គឺបំពេញឱ្យគ្នាទៅវិញទៅមក។

Tutorial នេះត្រូវបានគេបែងចែកជាច្រើនផ្នែក​ដូចខាងក្រោម​៖

* [ការរៀបចំសម្រាប់ ​Tutorial](#setup-for-the-tutorial) នឹងផ្តល់ឱ្យអ្នកនូវ**ចំណុចចាប់ផ្តើមមួយ**ដើម្បីអនុវត្តតាមការបង្រៀន។
* [ទិដ្ឋភាពទូទៅ](#overview) នឹងបង្រៀនអ្នកនូវ**មូលដ្ឋានគ្រឹះ**ពី React ដូចជា៖ components, props, និង state។
* [Completing the Game](#completing-the-game) នឹងបង្រៀនអ្នកនូវ**បច្ចេកទេសទូទៅបំផុត**ក្នុងការ develop React។
* [Adding Time Travel](#adding-time-travel) នឹងផ្តល់ឱ្យអ្នកនូវ**ការយល់ដឹងកាន់តែស៊ីជម្រៅ**នៃចំណុចខ្លាំងតែមួយគត់របស់ React។

អ្នកមិនចាំបាច់រៀនគ្រប់ផ្នែកទាំងអស់ក្នុងពេលតែមួយនេាះទេ។ អ្នកអាចរៀនផ្នែកណាមួយតាមតែអ្នកអាចធ្វើទៅបាន -- អ្នកអាចរៀនមួយផ្នែកឬក៏ពីរផ្នែក។

អ្នកអាច copy ហើយ paste កូដនៅពេលដែលអ្នកកំពុងអនុវត្តតាម tutorial, ប៉ុន្តែយើងសូមផ្តល់អនុសាសន៍អោយអ្នកវាយកូដដោយខ្លួនឯងផ្ទាល់។ ព្រេាះវាអាចជួយអ្នកឱ្យកាន់តែចងចាំនិងយល់កាន់តែច្បាស់។

### តើយើងនឹងបង្កើតអ្វី?    {#what-are-we-building}

នៅក្នុង tutorial នេះ យើងនឹងបង្ហាញពីរបៀបបង្កើតហ្គេម tic-tac-toe ជាមួយនិង React។

អ្នកអាចឃើញអ្វីដែលយើងនឹងបង្កើតនៅទីនេះ៖ **[Final Result](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**។ ប្រសិនជាអ្នកមិនយល់ពីកូដ, ឬក៏អ្នកមិនច្បាស់ជាមួយនិង syntax របស់កូដ សូមកុំបារម្មណ៏អី! គោលដៅនៃ tutorial នេះគឺជួយអ្នកឱ្យយល់ច្បាស់ពី React ហើយនិង syntax របស់ React។

យើងសូមផ្តល់អនុសាសន៍អោយអ្នកឆែកមើលហ្គេម​ tic-tac-toe នេះជាមុនសិនមុនពេលដែលបន្តជាមួយនិង tutorial ទៅមុខទៀត។ លក្ខណៈពិសេសមួយដែលអ្នកនឹងសម្គាល់គឺថាមានតារាងលេខនៅខាងស្តាំនៃ board របស់ហ្គេម។ តារាងនេះកត់ត្រានូវ history នៃការលេងរបស់ user ហើយ​ history វានិង update នៅពេលដែលហ្គេមដំណើរការ។

អ្នកអាចបិទហ្គេម tic-tac-toe នេះបាននៅពេលដែលអ្នកយល់ពីដំណើរការរបស់វា។ យើងនឹងចាប់ផ្តើមជាមួយនិង template ដ៏សាមញ្ញមួយនៅក្នុង tutorial នេះ។​​ ជំហានបន្ទាប់របស់យើងគឺរៀបចំអោយអ្នកអាចចាប់ផ្តើមបង្កើតហ្គេមនេះបាន។

### តម្រូវការជាមុន   {#prerequisites}

យើងនឹងសន្មត់ថាអ្នកមានចំណេះដឹងខ្លះៗពី HTML ហើយនិង JavaScript ប៉ុន្តែអ្នកគួរតែអាចអនុវត្តវាបានបើទេាះបីជាអ្នកមានចំណេះដឹងពីភាសា programming ផ្សេងៗក៏ដោយ។ យើងនឹងសន្មតផងដែរថាអ្នកមានចំណេះដឹងពី concept របស់ programming ដូចជា៖ functions, objects, arrays, and to a lesser extent, classes។

បើសិនជាអ្នកត្រូវការ review JavaScript យើងសូមផ្តល់យោបល់ឱ្យអាន [this guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)។ សូមកត់ចំណាំថាយើងនឹងប្រើ features មួយចំនួនរបស់ ES6 ផងដែរ -- កំណែទំរង់ថ្មីរបស់ JavaScript។ នៅក្នុង tutorial នេះ យើងនឹងប្រើ [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) ហើយនិង [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) statements។ អ្នកអាចប្រើ [Babel REPL](babel://es5-syntax-example) ដើម្បីឆែកមើលថាតើ code របស់ ES6 នឹង compile ទៅជាអ្វី។

## ការរៀបចំសម្រាប់ ​Tutorial {#setup-for-the-tutorial}

មានពីរវិធីដើម្បីអនុវត្តការសរសេរកូដនៅក្នុង tutorial នេះ៖ អ្នកអាចសរសេរកូដនៅលើ browser របស់អ្នកផ្ទាល់, ឬក៏អ្នកអាចរៀបចំ environment ក្នុងការ development នៅក្នុងកុំព្យូទ័ររបស់អ្នក។

### ជម្រើសទី១៖  សរសេរកូដនៅលើ browser {#setup-option-1-write-code-in-the-browser}

នេះជាវិធីលឿនបំផុតក្នុងការចាប់ផ្តើម!

តំបូង, សូមបើក **[Starter Code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)** នេះនៅក្នុងផ្ទាំងថ្មីមួយរបស់ browser​។ ផ្ទាំថ្មីគួរតែបង្ហាញ board ទទេមួយរបស់ហ្គេម tic-tac-toe ហើយនិងកូដ React. យើងនឹង edit កូដ​ របស់ React នៅក្នុង tutorial នេះ។

ឥឡូវអ្នកអាចរំលងជម្រើសទី២ក្នុងការតំឡើង, ហើយចូលទៅក្នុងផ្នែក [ទិដ្ឋភាពទូទៅ](#overview) ដើម្បីទទួលបាននូវមូលដ្ឋានគ្រឹះពី React។

### ជម្រើសទី២៖  តំឡើង environment ក្នុងការ development នៅក្នុងកុំព្យូទ័រ {#setup-option-2-local-development-environment}

នេះគឺជាជម្រើសដែលមិនចាំបាច់សម្រាប់ tutorial នេះទេ! ហើយក៏មិនតម្រូវអោយអ្នកត្រូវតែធ្វើការតំឡើងវាដែរ!

<br>

<details>

<summary><b>Optional: សេចក្តីណែនាំខាងក្រោមគឺភ្ជាប់ជាមួយការប្រើ text editor ដែលអ្នកចូលចិត្តនៅក្នុងកុំព្យូទ័ររបស់អ្នក</b></summary>

ការតំឡើងនេះតម្រូវអោយអ្នកធ្វើការងារធ្ងន់បន្តិច ប៉ុន្តែអាចអោយអ្នកអនុវត្តការសរសេរកូដនៅក្នុង tutorial នេះដោយប្រើ​ text editor ដែលអ្នកចូលចិត្តបាន។ ខាងក្រោមគឺជាជំហានដែលត្រូវអនុវត្តតាម៖

១. ត្រូវប្រាកដថាអ្នកបាន install [Node.js](https://nodejs.org/en/) ដែលមានកំណែទំរង់ថ្មី។
<br>
២. អនុវត្តតាម [installation instructions for Create React App](/docs/create-a-new-react-app.html#create-react-app) ដើម្បីបង្កើត project ថ្មីមួយ។

```bash
npx create-react-app my-app
```

៣. លុប files ទាំងអស់នៅក្នុងថតឯកសារ `src/` របស់ project ថ្មីនេាះ

> ចំណាំ៖
>
>**កុំលុបថតថតឯកសារ `src` ទាំងមូល, លុបតែ files ដែលនៅក្នុងវាទៅបានហើយ។**  យើងនឹងជំនួសឯកសារដើមដោយឧទាហរណ៍វិញសម្រាប់ project មួយនេះ។

```bash
cd my-app
cd src

# ប្រសិនជាអ្នកប្រើ Mac ឬក៏Linux៖
rm -f *

# ឬក៏, អ្នកប្រើ Window៖
del *

# បន្ទាប់មក, ត្រឡប់ទៅកាន់ថតឯកសាររបស់ project វិញ
cd ..
```

៤. បន្ថែម file មួយដោយដាក់ឈ្មេាះថា `index.css` ចូលទៅក្នុងថតឯកសារ `src/` ជាមួយនិង [this CSS code](https://codepen.io/gaearon/pen/oWWQNa?editors=0100)។

៥. បន្ថែម file មួយដោយដាក់ឈ្មេាះថា `index.js` ចូលទៅក្នុងថតឯកសារ `src/` ជាមួយនិង [this JS code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)។

៦. បន្ថែមកូដបីបន្ទាត់ខាងក្រោមទៅផ្នែកខាងលើគេនៃ `index.js` ដែលស្ថិតនៅក្នុងថតឯកសារ `src/`៖

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

ឥឡូវនេះប្រសិនបើអ្នក run `npm start` នៅក្នុងថតឯកសាររបស់ project ហើយបើក `http://localhost:3000` នៅលើ browser អ្នកគួរតែឃើញ tic-tac-toe ហ្គេមទទេមួយ។

យើងសូមផ្តល់អនុសាសន៍ [these instructions](https://babeljs.io/docs/editors/) ដើម្បីកំណត់ syntax highlighting សម្រាប់ editor របស់អ្នក។

</details>

### ជំនួយ, ខ្ញុំជាប់គាំងហើយ!   {#help-im-stuck}

ប្រសិនជាអ្នកជាប់គាំង អ្នកអាចឆែកមើល [community support resources](/community/support.html)។ ជាពិសេស [Reactiflux Chat](https://discord.gg/reactiflux) គឺជាវិធីដ៏ល្អមួយដើម្បីទទួលបានជំនួយយ៉ាងឆាប់រហ័ស។ ប្រសិនបើអ្នកមិនទទួលបានចម្លើយទេ ឬប្រសិនបើអ្នកនៅជាប់គាំង សូមរាយការណ៍នូវបញ្ហា ហើយយើងនឹងជួយអ្នក។

## ទិដ្ឋភាពទូទៅ   {#overview}

ឥឡូវនេះអ្នកបានធ្វើការរៀបចំសម្រាប់ tutorial នេះរួចរាល់ហើយ តេាះចាប់ផ្តើមនូវទិដ្ឋភាពទូទៅរបស់ React!

### តើអ្វីជា React? {#what-is-react}

React គឺជាការប្រកាស ប្រសិទ្ធិភាព ហើយនិង JavaScript library ដែល flexible មួយសម្រាប់បង្កើត user interfaces។ វាអនុញ្ញាតឱ្យអ្នកបង្កើត UIs ដែលស្មុគស្មាញ ពីបំណែកតូចៗនិងដាច់ពីគ្នានៃកូដដែលគេហៅថា "components"។

React មាន component ដែលមានប្រភេទផ្សេងៗពីគ្នាផងដែរ ប៉ុន្តែយើងនឹងចាប់ផ្តើមជាមួយនិង `React.Component` subclasses​៖

```javascript
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

យើងនឹងទទួលបាននូវ tags ដែលដូចទៅនិង XML tags។ យើងប្រើ components ដើម្បីប្រាប់ React នូវអ្វីដែលយើងចង់ឃើញនៅលើ screen។ នៅពេលដែល data ផ្លាស់ប្តូរ, React នឹង update ហើយនិង re-render components របស់យើង។

នេះ ShoppingList គឺជា **React component class** មួយ, ឬក៏ **React component type** មួយ។ component ទទួលយក parameters ដែលគេហៅថា `props` (ពាក្យពេញ "properties") ហើយ returns នូវ hierarchy នៃ views មួយដើម្បីបង្ហាញតាមរយៈ `render` method។

`render` method return នូវ *description* នៃអ្វីដែលអ្នកចង់ឃើញនៅលើអេក្រង់។​ React ទទួលយក description ហើយបង្ហាញលទ្ធផល។ ជាពិសេស `render` return នូវ **React element** មួយ ដែលជា description ដ៏ស្រាលមួយដែលត្រូវ render។ React developers ភាគច្រើនប្រើនូវ special syntax ដែលគេហៅថា "JSX"​ ដែលបង្កើតជា structures ងាយស្រួលក្នុងការសរសេរ។  `<div />` syntax គឺត្រូវបានគេបំលែងទៅជា `React.createElement('div')` នៅពេល build time។ ឧទាហរណ៍ខាងលើគឺស្មើទៅនឹង៖

```javascript
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

[See full expanded version.](babel://tutorial-expanded-version)

ប្រសិនជាអ្នកចង់ដឹងចង់ឃើញ, `createElement()` ត្រូវបានគេរៀបរាប់លម្អិតបន្ថែមនៅក្នុង [API reference](/docs/react-api.html#createelement), ប៉ុន្តែយើងនឹងមិនប្រើវានៅក្នុង tutorial នេះទេ។ ផ្ទយទៅវិញ យើងនឹងបន្តប្រើ JSX។

JSX ភ្ជាប់មកជាមួយនូវអានុភាពរបស់ JavaScript។ អ្នកអាចដាក់ expressions *ណាមួយ* របស់ JavaScript នៅក្នុងដង្កៀបខាងក្នុង​ JSX។ React element នីមួយៗគឺជា JavaScript object ដែលអ្នកអាចផ្ទុកនៅក្នុង variable ឬក៏អាច pass នៅក្នុង program របស់អ្នក។

`ShoppingList` component ដែលនៅខាងលើគឺ renders តែ built-in DOM components តែប៉ុណ្ណេះដូចជា `<div />` ហើយនិ `<li />`។ ប៉ុន្តែអ្នកអាចបង្កើតហើយនិង render custom React components ផងដែរ។ ឧទាហរណ៍ ឥឡូវ​នេះយើងអាចយោងទៅលើ shopping list ដោយសរសេរ `<ShoppingList />`។ React component នីមួយៗគឺ encapsulated ហើយនិង
អាចដំណើរការដោយឯករាជ្យ; នេះអនុញ្ញាតឱ្យអ្នកបង្កើត UI ដែលស្មុគ្រស្មាញពី components ដែលសាមញ្ញ។

<<<<<<< HEAD
## ការត្រួតពិនិត្យ   Starter Code {#inspecting-the-starter-code}
=======
### Inspecting the Starter Code {#inspecting-the-starter-code}
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

បើសិនជាអ្នកនិងធ្វើការលើ tutorial **នៅក្នុង  browser** បើកកូដនេះក្នុងផ្ទាំងថ្មី៖ **[Starter Code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)**។ បើសិនជាអ្នកនឹងធ្វើការលើ tutorial **នៅក្នុងកុំព្យូទ័ររបស់អ្នក** បើក `src/index.js` នៅក្នុង project folder (អ្នកបានប៉ះឯកសារនេះរួចហើយកំឡុងពេល [setup](#setup-option-2-local-development-environment))។

Starter Code នេះគឺជាមូលដ្ឋាននៃអ្វីដែលយើងនឹងបង្កើត។ យើងបានផ្តល់នូវ CSS styling ដូច្នេះអ្នកត្រូវតែផ្តោតលើការរៀន React ហើយនិង programming ហ្គេម tic-tac-toe។

តាមរយៈការត្រួតពិនិត្យកូដ, អ្នកនឹងកត់សម្គាល់ថាយើងមាន React components ចំនួន៣៖

* Square
* Board
* Game

Square component renders `<button>` តែមួយហើយ Board renders squares ចំនួន៩។ Game component render board មួយជាមួយនិង តម្លៃរបស់ placeholder ដែលយើងនឹងកែប្រែនៅពេលក្រោយ។ បច្ចុប្បន្នគឺអត់ទាន់មាន interactive components ទេ។

### ការបញ្ជូន  Data តាមរយៈ  Props {#passing-data-through-props}

ចាប់ផ្តើមទទួលបានបទពិសោធ, តេាះសាកល្បងបញ្ជូន data ពី Board component ទៅកាន់ Square component។

នៅក្នុង `renderSquare` method របស់ Board component, ផ្លាស់ប្តូរកូដដើម្បីបញ្ជូន props មួយដែលមានឈ្មេាះ `value` ទៅកាន់ Square component។

```js{3}
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
```

ផ្លាស់ប្តូរ `render` method របស់ Square component ដើម្បីបង្ហាញ value ដោយការជំនួសដោយ `{/* TODO */}` ជាមួយនិង `{this.props.value}`​៖

```js{5}
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

ពីមុន​៖

![React Devtools](../images/tutorial/tictac-empty.png)

អ្នកគួរតែឃើញលេខនៅក្នុង square នីមួយៗចំនួន១នៅក្នុងលទ្ធផលបង្ហាញ។

![React Devtools](../images/tutorial/tictac-numbers.png)

**[View the full code at this point](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)**

អបអរសាទរ! អ្នកទើបតែបាន "បញ្ជូន prop មួយ" ពី parent Board component ទៅកាន់ child Square component។ ការបញ្ជូន props គឺជារបៀបដែលពត៌មានហូរនៅក្នុង React apps ពី parent ទៅកាន់ children។

### ការបង្កើត Interactive Component មួយ {#making-an-interactive-component}

តេាះបំពេញ Square component ជាមួយនិង "X" នៅពេលដែលយើង click វា។ តំបូង, ផ្លាស់ប្តូរ button tag ដែលត្រូវបានគេ return ពី `render()` function របស់ Square component​ ដូចខាងក្រោម៖

```javascript{4}
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { console.log('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

<<<<<<< HEAD
ប្រសិនជាយើង click លើ Square ឥឡូវ​នេះ យើងគួរតែទទួលបាននូវ alert មួយនៅក្នុង browser យើង។
=======
If you click on a Square now, you should see 'click' in your browser's devtools console.
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

សម្រាប់ event handlers

>ចំណាំ
>
>ដើម្បីជាជំនួយក្នុងការ typing ហើយនិងជៀសវាង [ការភាន់ច្រឡំនូវ behavior របស់ `this`](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/) យើងនឹងប្រើ​ [arrow function syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) សម្រាប់ event handlers នៅទីនេះហើយនិងពេលខាងមុខទៀត៖
>
>```javascript{4}
>class Square extends React.Component {
>  render() {
>    return (
>      <button className="square" onClick={() => console.log('click')}>
>        {this.props.value}
>      </button>
>    );
>  }
>}
>```
>
<<<<<<< HEAD
>សូមកត់សម្គាល់ពីបៀបជាមួយ `onClick={() => alert('click')}`, យើងនឹងបញ្ជូន *function មួយ* ជា `onClick` prop។ វា fire តែពេលបន្ទាប់ពី click តែប៉ុណ្ណោះ។ បំភ្លេច `() =>` ហើយសរសេរ `onClick={alert('click')}` គឺជាកំហុសធម្មតា, ហើយនិង fire ការ alert រាល់ពេលដែល component ធ្វើការ re-renders។
=======
>Notice how with `onClick={() => console.log('click')}`, we're passing *a function* as the `onClick` prop. React will only call this function after a click. Forgetting `() =>` and writing `onClick={console.log('click')}` is a common mistake, and would fire every time the component re-renders.
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

ជំហានបន្ទាប់, យើងចង់អោយ Square component "ចងចាំ" ថាវាត្រូវបានគេ click ហើយនិងបំពេញវាជាមួយនិងសញ្ញា "X"។ ដើម្បី "ចងចាំ" អ្វីមួយ, component ប្រើ **state**។

React components អាចមាន state ដោយការកំណត់ `this.state` នៅក្នុង constructors។ `this.state` គួរតែត្រូវបានចាត់ទុកជា private នៅក្នុង React component។ តេាះរក្សារតម្លៃបច្ចុប្បន្នរបស់ Square នៅក្នុង `this.state` ហើយផ្លាស់ប្តូរវានៅពេលដែល Square ត្រូវបាន click.

ដំបូង, យើងនឹង add constructor មួយទៅអោយ class ដើម្បីកំណត់តម្លៃ state៖

```javascript{2-7}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => console.log('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

>ចំណាំ
>
>នៅក្នុង [JavaScript classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) អ្នកតម្រូវអោយ call `super` នៅពេលធ្វើការកំណត់ constructor នៃ subclass។ React component classes ទាំងអស់ដែលមាន constructor គួរតែចាប់ផ្តើមជាមួយនិងការ call `super(props)`។

ឥឡូវ​នេះយើងនឹងផ្លាស់ប្តូរ `render` method របស់ Square ដើម្បីបង្ហាញតម្លៃ​បច្ចុប្ប​ន្នរបស់ state នៅពេលដែលត្រូវបាន click៖

* ជំនួស `this.props.value` ជាមួយនិង `this.state.value` នៅខាងក្នុង `<button>` tag។
* ជំនួស `() => alert()` event handler ជាមួយនិង `() => this.setState({value: 'X'})`។
* ដាក់ `className` ហើយនិង `onClick` props នៅលើបន្ទាត់ដាច់ដោយឡែកសម្រាប់ភាពងាយស្រួលក្នុងការអាន។

បន្ទាប់ពីការផ្លាស់ប្តូរទាំងនេះ, `<button>` tag ដែលត្រូវបាន return ដោយ `render` method របស់ Square នឹងមើលទៅដូចនេះ៖

```javascript{12-13,15}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

តាមរយៈការ call `this.setState` ពី `onClick` handler នៅក្នុង `render` method របស់ Square យើងប្រាប់ React ធ្វើការ re-render Square គ្រប់ពេលដែល `<button>` ត្រូវបាន click។ បន្ទាប់ពីការ update `this.state.value` របស់ Square នឹងប្តូរទៅជា `'X'` ដូច្នេះយើងនឹងឃើញ `X` នៅលើ board របស់ហ្គេម។ បើអ្នក click លើ​​ Square ផ្សេងៗទៀត `X` គួរតែបង្ហាញ។

នៅពេលដែលអ្នក call `setState` នៅក្នុង component មួយ React នឹង update child component ដែលនៅក្នុងវាដោយស្វ័យប្រវត្តិ។

**[View the full code at this point](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)**

### Tools របស់ Developer {#developer-tools}

React Devtools extension សម្រាប់ [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) ហើយនិង [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/) អាចអោយអ្នកត្រួតពិនិត្យ React component tree ជាមួយ developer tools របស់ browser បាន។

<img src="../images/tutorial/devtools.png" alt="React Devtools" style="max-width: 100%">

React DevTools អាចអោយអ្នកឆែកមើល props ហើយនិង state របស់ React components បាន។

បន្ទាប់ពីដំឡើង React DevTools, អ្នកអាច right-click លើ element ដែលមាននៅលើ page, click "Inspect" ដើម្បីបើក developer tools, ហើយ React tab ("⚛️ Components" និង "⚛️ Profiler") នឹងលេចឡើងនៅផ្ទាំងចុងក្រោយខាងស្តាំ។ ប្រើ "⚛️ Components" ដើម្បី inspect មើល component tree។

**ទោះជាយ៉ាងណាក៏ដោយ, សូមកត់សម្គាល់ថាមានជំហានបន្ថែមមួយចំនួនទៀតដើម្បីអោយវាដំណើរការជាមួយ CodePen​៖**

1. ចូល log in ឬក៏ចុះឈ្មោះ ហើយបញ្ជាក់ email របស់អ្នក (ទាមទារដើម្បីទប់ស្កាត់សារឥតបានការ)។
2. Click លើ "Fork" ប៊ូតុង។
3. Click លើ "Change View" ហើយបន្ទាប់មកជ្រើសរើស "Debug mode"។​
4. នៅក្នុងផ្ទាំងថ្មីដែលបើក devtools ឥឡូវនេះគួរតែមានផ្ទាំង React។

## Completing the Game {#completing-the-game}

ឥឡូវនេះយើងមានមូលដ្ឋានក្នុងការបង្កើត blocks សម្រាប់ tic-tac-toe ហ្គេមរបស់យើង។ ដើម្បីអោយបានហ្គេមមួយអោយពេញលេញ ឥឡូវនេះយើងត្រូវដាក់ជំនួស "X"s ហើយនិង "O"s ទៅលើ board ហើយយើងត្រូវការវិធីមួយដើម្បីកំណត់អ្នកឈ្នះ។

### Lifting State Up {#lifting-state-up}

បច្ចុប្បន្ន Square component នីមួយៗរក្សារនូវ state របស់ហ្គេម។ ដើម្បីពិនិត្យរកអ្នកឈ្នះ យើងនឹងរក្សារតម្លៃនីមួយៗរបស់ squares ទាំង៩នៅក្នុងទីតាំងមួយ។

យើងប្រហែលជាគិតថា Board គួរតែស្នើរសុំនូវតម្លៃ state របស់Square នីមួយៗ។ បើទោះបីជាវិធីសាស្រ្តនេះគឺអាចធ្វើទៅបាន សម្រាប់ React, យើងមិនលើកទឹកចិត្តអោយធ្វើតាមវិធីនេះទេពីព្រេាះកូដនឹងក្លាយទៅជាពិបាកយល់​ ងាយនិងមាន bugs ហើយពិបាកក្នុងការ refactor។ ជំនួសវិញ វិធីសាស្រ្តដ៏ល្អបំផុតគឺត្រូវរក្សាទុក state របស់ហ្គេម នៅក្នុង parent Board component ជំនួសអោយការរក្សារទុកនៅក្នុង Square នីមួយៗ។ Board component អាចប្រាប់ Square នីមួយៗនូវអ្វីដែលត្រូវបង្ហាញដោយការបញ្ជូន props មួយ [just like we did when we passed a number to each Square](#passing-data-through-props)។

**ដើម្បីប្រមូល data ពី children ជាច្រើន ឬក៏ដើម្បីអោយ child components ២ទំនាក់ទំនងជាមួយគ្នាទៅវិញទៅមក, អ្នកត្រូវ declare state នៅក្នុង parent component។ Parent component អាចបញ្ជូន state ចុះទៅ់ children ដោយការប្រើ props; នេះអាចអោយ child components syn ជាមួយគ្នាទៅវិញទៅមក, ហើយនិង syn ជាមួយ parent component ផងដែរ។**

ការយក​ state ដាក់ចូលទៅក្នុង parent component គឺជាការធម្មតា​ នៅពេលដែល React components ត្រូវបាន refactor -- សូមឆ្លៀតឱកាសនេះដើម្បីសាកល្បងវា។ យើងនឹងបន្ថែម constructor ទៅអោយ Board ហើយនិងកំណត់តម្លៃ state របស់ Board ដោយផ្ទុកនូវ array មួយជាមួយនិង​ nulls ចំនួន៩។ nulls ទាំង៩នេះទាក់ទងទៅនឹង៩ squares៖

```javascript{2-7}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  renderSquare(i) {
    return <Square value={i} />;
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

នៅពេលដែលយើងបំពេញ board នៅពេលក្រោយ board នឹងមើលទៅដូចនេះ៖

```javascript
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

`renderSquare` method របស់ Board បច្ចុប្បន្នមើលទៅដូចនេះ៖

```javascript
  renderSquare(i) {
    return <Square value={i} />;
  }
```

នៅពេលចាប់ផ្តើម យើង[បានបញ្ជូន `value` របស់ prop ចុះក្រោម](#passing-data-through-props)ពី Board ដើម្បីបង្ហាញចំនួនលេខពី០ទៅ៨នៅក្នុង Square ទាំងអស់។ នៅក្នុងជំហានមុនផ្សេងគ្នា, យើងបានជំនួសលេខដោយសញ្ញា "X" [determined by Square's own state](#making-an-interactive-component)។ នេះជាមូលហេតុដែល Square បច្ចុប្បន្នមិនអើពើ `value` របស់ prop ដែលបានបញ្ជួនអោយវាដោយ Board។

ឥលូវយើងនឹងប្រើប្រាស់យន្ដការក្នុងការបញ្ជូន​ props ម្តងទៀត។ យើងនឹងកែប្រែ Board ដើម្បីណែនាំដល់ Square នីមួយៗពីតម្លៃបច្ចុប្បន្នរបស់វា (`'X'`, `'O'`, ឬក៏ `null`)។ យើងបានកំណត់រួចហើយនូវ `squares` array នៅក្នុង constructor របស់ Board, ហើយយើងនឹងកែប្រែ `renderSquare` method របស់ Board ដើម្បីអានពីវា៖


```javascript{2}
  renderSquare(i) {
    return <Square value={this.state.squares[i]} />;
  }
```

**[View the full code at this point](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)**

Square នីមួយៗនឹងទទួលបាននូវ `value` របស់ props ដែលអាចជា `'X'`, `'O'`, ឬក៏ `null` សម្រាប់ squares ទទេ។

បន្ទាប់មកទៀត យើងត្រូវការផ្លាស់ប្តូរអ្វីដែលកើតឡើងនៅពេលដែល Square ត្រូវបាន click។ ឥឡូវនេះ Board component រក្សារទុកនូវ squares ដែលត្រូវបានបំពេញ។​ យើងត្រូវបង្កើតវិធីដើម្បីអោយ Square អាច update state របស់ Board បាន។ ដែល state ត្រូវបានចាត់ទុកជា private សម្រាប់ component យើងមិនអាច update state របស់ Board ដោយផ្ទាល់ពី Square។

ដើម្បីរក្សារភាពឯកជនរបស់ state ដែលមាននៅក្នុង Board យើងនឹងបញ្ជួន function មួយពី Board ចុះទៅ Square។ function នេះនឹងត្រូវបានហៅនៅពេលដែល​ Square ត្រូវបាន click។ យើងនឹងផ្លាស់ប្តូរ `renderSquare` method ដែលមាននៅក្នុង Board ផងដែរ៖

```javascript{5}
  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }
```

>ចំណាំ
>
>យើងបំបែកការ return element ទៅជាច្រើនបន្ទាត់ដើម្បីងាយស្រួលក្នុងការអាន, ហើយបានបន្ថែមវង់ក្រចកដូច្នេះ JavaScript មិនបញ្ចូលសញ្ញា semicolon បន្ទាប់ពី `return` ហើយនិង break កូដ របស់យើង។

ឥឡូវ​នេះយើងកំពុងបញ្ជួនចុះនូវ props ចំនួន២ពី Board ទៅកាន់ Square៖ `value` ហើយនិង `onClick`។ `onClick` គឺជា function ដែល Square អាចហៅនៅពេលត្រូវបាន click។ យើងនឹងធ្វើការផ្លាស់ប្តូរ Square ដូចខាងក្រោម៖

* ជំនួស `this.state.value` ជាមួយ `this.props.value` នៅក្នុង `render` method របស់ Square
* ជំនួស `this.setState()` ជាមួយ `this.props.onClick()` នៅក្នុង `render` method របស់ Square
* លុប `constructor` ពី Square ពីព្រេាះ Square លែងបន្តតាមដាន state របស់ហ្គេម

បន្ទាប់ពីការផ្លាស់ប្តូរទាំងនេះ, Square component មើលទៅដូចនេះ៖

```javascript{1,2,6,8}
class Square extends React.Component {
  render() {
    return (
      <button
        className="square"
        onClick={() => this.props.onClick()}
      >
        {this.props.value}
      </button>
    );
  }
}
```

នៅពេលដែល Square ត្រូវបាន click `onClick` function ដែលត្រូវបានផ្តល់ដោយ Board ត្រូវបានហៅ។
នេះគឺជាការពិនិត្យឡើងវិញនូវរបៀបដែលវាសម្រេច៖

<<<<<<< HEAD
១. `onClick` prop នៅលើ built-in DOM `<button>` component ប្រាប់ React ដើម្បីបង្កើត click event listener មួយ។<br>
២. នៅពេលដែល​ button ត្រូវបាន click React នឹងហៅ `onClick` event handler ដែលបានកំណត់នៅក្នុង `render()` method របស់ Square។<br>
៣. event handler នេះហៅថា `this.props.onClick()`។ `onClick` prop របស់ Square ត្រូវបានបញ្ជាក់ដោយ Board។<br>
៤. ដែល Board ​បានបញ្ជូន `onClick={() => this.handleClick(i)}` ទៅអោយ Square Square ហៅ `this.handleClick(i)` ត្រូវបាន click។<br>
៥. យើងមិនបានកំណត់ `handleClick()` method នៅឡើយទេ ដូច្នេះកូដរបស់យើងគាំង។
=======
1. The `onClick` prop on the built-in DOM `<button>` component tells React to set up a click event listener.
2. When the button is clicked, React will call the `onClick` event handler that is defined in Square's `render()` method.
3. This event handler calls `this.props.onClick()`. The Square's `onClick` prop was specified by the Board.
4. Since the Board passed `onClick={() => this.handleClick(i)}` to Square, the Square calls the Board's `handleClick(i)` when clicked.
5. We have not defined the `handleClick()` method yet, so our code crashes. If you click a square now, you should see a red error screen saying something like "this.handleClick is not a function".
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

>ចំណាំ
>
>គុណលក្ខណៈ `onClick` របស់ DOM `<button>` element មានអត្ថន័យពិសេសចំពោះ React ពីព្រេាះវាគឺជា built-in component។ សម្រាប់ custom components ដូច Square, ការដាក់ឈ្មោះគឺអាស្រ័យលើអ្នក។ យើងអាចដាក់ឈ្មេាះ `onClick` prop របស់ Square ឬក៏ `handleClick` method របស់ Board ខុសគ្នាបាន។ នៅក្នុង React, ទោះជាយ៉ាងណា, វាគឺជា convention ដើម្បីប្រើឈ្មេាះ `on[Event]` សម្រាប់ props ដែលតំណាងអោយ events ហើយនិង `handle[Event]` សម្រាប់ methods ដែល handle events.

នៅពេលយើងព្យាយាម click Square មួយ, យើងគួរតែទទួលបាន error មួយពីព្រេាះយើងមិនបានកំណត់ `handleClick` នៅឡើយទេ។ ឥឡូវនេះយើងនឹងបន្ថែម `handleClick` អោយ Board class៖

```javascript{9-13}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = 'X';
    this.setState({squares: squares});
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[View the full code at this point](https://codepen.io/gaearon/pen/ybbQJX?editors=0010)**

បន្ទាប់ពីការផ្លាស់ប្តូរទាំងនេះ យើងអាច click ម្តងទៀតទៅលើ Squares ដើម្បីបំពេញពួកវា។​ ទោះយ៉ាងណា ឥឡូវ​នេះ state ត្រូវបានរក្សារទុកនៅក្នុង Board component ជំនួសអោយការរក្សារទុកនៅក្នុង Square components នីមួយៗ។ នៅពេលដែល state របស់ Board ផ្លាស់ប្តូរ Square components re-render ដោយស្វ័យប្រវត្តិ។ ការរក្សារ state របស់ squares ទាំងអស់នៅក្នុង Board component នឹងអនុញ្ញាតឱ្យវាកំណត់អ្នកឈ្នះនៅថ្ងៃអនាគត។

នៅពេលដែល Square components លែងរក្សា state Square components ទទួលបានតម្លៃពី Board component និងជូនដំណឹងអោយ Board component នៅពេលពួកវាត្រូវបាន click។ នៅក្នុង React terms ឥឡូវ​នេះ Square components គឺជា **controlled components**។ Board មានការគ្រប់គ្រងពេញលេញលើពួកវា។

ចំណាំរបៀបនៅក្នុង `handleClick` យើងហៅ `.slice()` ដើម្បីបង្កើតច្បាប់ចម្លង `squares` array ដើម្បីកែប្រែ ជំនួសអោយការកែប្រែ array ដែលមានស្រាប់។ យើងនឹងពន្យល់ពីមូលហេតុដែលយើងបង្កើតច្បាប់ចម្លង `squares` array នៅផ្នែកបន្ទាប់។

### ហេតុអ្វីបានជាភាពមិនអាចប្រែប្រួលបានមានសារះសំខាន់?        {#why-immutability-is-important}

<<<<<<< HEAD
នៅក្នុងឧទាហរណ៍របស់កូដមុន យើងបានស្នើឱ្យអ្នកប្រើ `.slice()` operator ដើម្បីបង្កើតច្បាប់ចម្លងនៃ `squares` array ដើម្បីកែប្រែជំនួសអោយការកែប្រែ array ដែលមានស្រាប់។ ឥឡូវនេះយើងនឹងពិភាក្សាគ្នាអំពីភាពមិនចេះប្រែប្រួលហើយហេតុអ្វីក៏ភាពមិនប្រែប្រួលជាការសំខាន់ក្នុងការរៀនសូត្រ។
=======
In the previous code example, we suggested that you create a copy of the `squares` array using the `slice()` method instead of modifying the existing array. We'll now discuss immutability and why immutability is important to learn.
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

មានវិធីពីរយ៉ាងក្នុងការផ្លាស់ប្តូរទិន្នន័យ។ វិធីសាស្រ្តដំបូងគឺ *ផ្លាស់ប្តូរ* ទិន្នន័យ ដោយការផ្លាស់ប្តូរតម្លៃទិន្នន័យដោយផ្ទាល់។ វិធីសាស្ត្រទីពីរគឺជំនួសទិន្នន័យជាមួយច្បាប់ចម្លងថ្មីដែលមានការផ្លាស់ប្តូរតាមដែលអ្នកចង់បាន។

#### ការផ្លាស់ប្តូរទិន្នន័យជាមួយការផ្លាស់ប្តូរដោយផ្ទាល់         {#data-change-with-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

#### ការផ្លាស់ប្តូរទិន្នន័យដោយគ្មានការផ្លាស់ប្តូរដោយផ្ទាល់         {#data-change-without-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}

// Or if you are using object spread syntax proposal, you can write:
// var newPlayer = {...player, score: 2};
```

លទ្ធផលចុងក្រោយគឺដូចគ្នាប៉ុន្តែដោយមិនផ្លាស់ប្តូរដោយផ្ទាល់ (ឬការផ្លាស់ប្តូរទិន្នន័យមូលដ្ឋាន), យើងទទួលអត្ថប្រយោជន៍ជាច្រើនដូចបានរៀបរាប់ខាងក្រោម។

#### លក្ខណៈពិសេសស្មុគស្មាញក្លាយជាធម្មតា      {#complex-features-become-simple}

ភាពមិនចេះប្រែប្រួលធ្វើឱ្យ features ដែលស្មុគ្រស្មាញកាន់តែងាយស្រួលក្នុងការ implement។ នៅក្នុង tutorial បន្ទាប់ យើងនឹង implement "time travel" feature ដែលអនុញ្ញាតឱ្យយើងពិនិត្យឡើងវិញនូវ history របស់ tic-tac-toe ហ្គេម ហើយនិង "jump back" ត្រឡប់ទៅកាន់ការផ្លាស់ទីពីមុន។ មុខងារនេះមិនជាក់លាក់ចំពោះហ្គេមទេ -- សមត្ថភាពក្នុងការ undo ហើយនិង redo ដែលជាសកម្មភាពជាក់លាក់គឺជាតម្រូវការទូទៅនៅក្នុង​ applications។ ការជៀសវាងការផ្លាស់ប្តូរទិន្នន័យដោយផ្ទាល់អនុញ្ញាតឱ្យយើងរក្សាកំណែមុននៃ history របស់ហ្គេមអោយនៅដដែល ហើយប្រើវាឡើងវិញនៅពេលក្រោយ។

#### ការរកឃើញការផ្លាស់ប្តូរ    {#detecting-changes}

រកឃើញការផ្លាស់ប្តូរនៅក្នុង objects ដែលអាចប្ដូរបានគឺពិបាកពីព្រោះពួកគេត្រូវបានកែប្រែដោយផ្ទាល់។ ការរកឃើញនេះទាមទារអោយ objects ដែលអាចប្ដូរបានប្រៀបធៀបទៅនឹងច្បាប់ចម្លងពីមុនរបស់ខ្លួន ហើយនិង object tree ទាំងមូលត្រូវបាន traverse។

ការរកឃើញការផ្លាស់ប្តូរ objects ដែល​មិនប្រែប្រួលគឺចាត់ទុកថាងាយស្រួលជាង។ ប្រសិនជា objects ដែល​មិនប្រែប្រួលដែលកំពុងតែ reference គឺខុសពីមុន អញ្ចឹង object ត្រូវបានផ្លាស់ប្តូ។

#### ការកំណត់នៅពេល re-render នៅក្នុង React {#determining-when-to-re-render-in-react}

<<<<<<< HEAD
អត្ថប្រយោជន៍សំខាន់នៃភាពមិនប្រែប្រួលគឺថាវាជួយអ្នកបង្កើត _pure components_ នៅក្នុង React។ ទិន្នន័យដែលអាចផ្លាស់ប្តូរបានអាចកំណត់បានយ៉ាងងាយស្រួលប្រសិនបើការផ្លាស់ប្តូរត្រូវបានធ្វើឡើងដែលជួយកំណត់នៅពេល component តម្រូវការ re-rendering។
=======
The main benefit of immutability is that it helps you build _pure components_ in React. Immutable data can easily determine if changes have been made, which helps to determine when a component requires re-rendering.
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

អ្នកអាចស្វែងយល់បន្ថែមអំពី `shouldComponentUpdate()` និងរបៀបដែលអ្នកអាចបង្កើត *pure components* ដោយការអាន [Optimizing Performance](/docs/optimizing-performance.html#examples)។

### Function Components {#function-components}

ឥឡូវនេះយើងនឹងផ្លាស់ប្តូរ Square អោយក្លាយជា **function component**។

នៅក្នុង React **function components** គឺជាវិធីសាមញ្ញក្នុងការសរសេរ components ដែលមានតែ `render` method ហើយមិនមាន state ដែលជារបស់ពួកគេផ្ទាល់។ ជំនួសឱ្យការកំណត់ class មួយដែល extends `React.Component`, យើងអាចសរសេរ function មួយដែលទទួល `props` ជា input ហើយ returns នូវអ្វីដែលគួរត្រូវបាន​ render។ Function components
មានការធុញទ្រាន់តិចតួចក្នុងការសរសេរជាង classes និង components ជាច្រើនអាចត្រូវបានបញ្ជាក់តាមវិធីនេះ។

Replace the Square class with this function:

ជំនួស Square class ជាមួយ function នេះ៖

```javascript
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

យើងបានផ្លាស់ប្តូរ `this.props` ជា `props` ចំនួនពីរ។

**[View the full code at this point](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)**

>ចំណាំ
>
>នៅពេលយើងបានកែប្រែ Square អោយក្លាយជា function component យើងក៏បានផ្លាស់ប្តូរផងដែរនូវ `onClick={() => this.props.onClick()}` អោយទៅជាខ្លី `onClick={props.onClick}` (ចំណាំការខ្វះវង់ក្រចក*ទាំងពីរ*ខាង)។ នៅក្នុង class, យើងបានប្រើ arrow function មួយដើម្បីចូលប្រើ តម្លៃ `this` ដែលត្រឹមត្រូវ បន្តែនៅក្នុង function component
យើងមិនចាំបាច់ព្រួយបារម្ភពី `this` ទេ។

### Taking Turns {#taking-turns}

ឥឡូវនេះយើងចាំបាច់ត្រូវជួសជុលកំហុសឆ្គងជាក់ស្តែងនៅក្នុង tic-tac-toe ហ្គេមរបស់យើង៖ "O"s មិនអាចត្រូវបានសម្គាល់នៅលើក្តារ។

យើងនឹងកំណត់ការផ្លាស់ប្តូរដំបូងឱ្យក្លាយជា "X" ជាលំនាំដើម។ យើងអាចកំណត់លំនាំដើមនេះដោយការកែប្រែ initial state នៅក្នុង constructor របស់​ Board៖

```javascript{6}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

រាល់ពេលដែលអ្នកលេងផ្លាស់ទី `xIsNext` (a boolean) នឹងត្រូវបានត្រឡប់ដើម្បីកំណត់ថាអ្នកលេងណាម្នាក់ទៅបន្ទាប់ហើយ state របស់ game និងត្រូវបានស​​ save។ យើងនឹង update `handleClick` function របស់ Board ដើម្បីត្រឡប់តម្លៃរបស់ `xIsNext`៖

```javascript{3,6}
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

ជាមួយនឹងការផ្លាស់ប្តូរនេះ, "X"s និង "O"s អាចផ្លាស់ប្តូរគ្នា។ ចូរផ្លាស់ប្តូរផងដែរនូវ "status" text នៅក្នុង​ `render` របស់ Board ដូច្នេះវាបង្ហាញថាវេនបន្ទាប់ជារបស់អ្នកលេងម្នាក់ណា៖

```javascript{2}
  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // the rest has not changed
```

បន្ទាប់ពីអនុវត្តការផ្លាស់ប្តូរទាំងនេះអ្នកគួរតែមាន Board component នេះ៖

```javascript{6,11-16,29}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[View the full code at this point](https://codepen.io/gaearon/pen/KmmrBy?editors=0010)**

### Declaring a Winner {#declaring-a-winner}

ឥឡូវនេះយើងបង្ហាញអ្នកលេងដែលមានវេនបន្ទាប់ យើងក៏គួរបង្ហាញផងដែរថានៅពេលដែលហ្គេមត្រូវបានឈ្នះ ហើយមិនមានវេនបន្ទាប់ទៀតទេ។ យើងអាចកំណត់អ្នកឈ្នះដោយបន្ថែម function ជំនួយមួយនេះទៅចុងបញ្ចប់នៃ files៖

```javascript
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

យើងនឹងហៅ `calculateWinner(squares)` នៅក្នុង `render` function របស់ Board ដើម្បីពិនិត្យថាតើអ្នកលេងបានឈ្នះឬយ៉ាងណា។ ប្រសិនបើអ្នកលេងបានឈ្នះ យើងអាចបង្ហាញអត្ថបទដូចជា "អ្នកឈ្នះ: X" ឬ "អ្នកឈ្នះ: អូរ"។ យើងនឹងជំនួសការប្រកាស `status` នៅក្នុង `render` function របស់ Board ជាមួយកូដនេះ៖

```javascript{2-8}
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // the rest has not changed
```

ឥឡូវនេះយើងអាចផ្លាស់ប្តូរ `handleClick` function របស់Board ដើម្បី​​​ return early ដោយការមិនអើពើការ click ប្រសិនជាអ្នកណាម្នាក់បាន​ឈ្នះការប្រកួតឬក៏ Square ត្រូវបានបំពេញរួចហើយ៖

```javascript{3-5}
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

**[View the full code at this point](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)**

សូមអបអរសាទរ! ឥឡូវអ្នកមាន tic-tac-toe ហ្គេមមួយដែលកំពុងដំណើរការ។ ហើយអ្នកទើបតែរៀនពីមូលដ្ឋានគ្រឹះនៃ React ផងដែរ។ ដូច្នេះ *អ្នកគឺ* ប្រហែលជាអ្នកឈ្នះពិតប្រាកដនៅទីនេះ។

## Adding Time Travel {#adding-time-travel}

នេះជាលំហាត់ចុងក្រោយ សូមធ្វើឱ្យវាអាចទៅរួច "ត្រឡប់ទៅពេលវេលាមួយ" ទៅកាន់ការផ្លាស់ប្តូរពីមុននៅក្នុងហ្គេម។

### Storing a History of Moves {#storing-a-history-of-moves}

ប្រសិនបើយើងបានផ្លាស់ប្តូរ `squares` array, ការ implement time travel នឹងមានការលំបាកខ្លាំងណាស់។

ទោះយ៉ាងណា យើងបានប្រើ `slice()` ដើម្បីបង្កើតច្បាប់ចម្លងថ្មី នៃ `squares` array បន្ទាប់ពីរាល់ការ move​ និង [ចាត់ទុកវាជាមិនប្រែប្រួល](#why-immutability-is-important)។ នេះនឹងអនុញ្ញាតិឱ្យយើងរក្សាទុករាល់កំណែដែលកន្លងមកនៃ `squares` array និងរុករករវាងវេនដែលបានកើតឡើងរួចហើយ។

យើងនឹងរក្សាទុកអតីតកាលរបស់ `squares` arrays នៅក្នុង array ផ្សេងដែលបានហៅថា `history`។ `history` array តំណាងអោយ board states ទាំងអស់, ពីដំបូងទៅការផ្លាស់ទីចុងក្រោយ និងមានរាងដូចនេះ៖

```javascript
history = [
  // Before first move
  {
    squares: [
      null, null, null,
      null, null, null,
      null, null, null,
    ]
  },
  // After first move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, null,
    ]
  },
  // After second move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, 'O',
    ]
  },
  // ...
]
```

ឥឡូវនេះយើងត្រូវសម្រេច component មួយណាគួរតែជាម្ចាស់ `history` state។

### Lifting State Up, Again {#lifting-state-up-again}

យើងនឹងចង់បាន top-level Game component ដើម្បីបង្ហាញបញ្ជីនៃការផ្លាស់ប្តូរពីមុន។ វានឹងត្រូវការសិទ្ធិចូលប្រើ `history` ដើម្បីធ្វើដូច្នោះ ដូច្នេះយើងនឹងដាក់ `history` state ទៅក្នុង top-level Game component។

ការដាក់ `history` state ចូលក្នុង Game component អនុញ្ញាតឱ្យយើងដកចេញ `squares` state ពី child Board component។ ដូចជាយើង ["lifted state up"](#lifting-state-up) ពី Square component ទៅក្នុង Board component ឥឡូវនេះយើងកំពុងលើកវាឡើងពី Board ទៅ top-level Game component។ នេះផ្តល់ឱ្យ Game component នូវការគ្រប់គ្រងពេញលេញទៅលើ data របស់ Board និងអនុញ្ញាតឱ្យវាណែនាំ Board អោយ render វេនមុន ពី `history`។

ដំបូង យើងនឹងរៀបចំ initial state សម្រាប់ Game component នៅក្នុង constructor របស់ខ្លួនវា៖

```javascript{2-10}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      xIsNext: true,
    };
  }

  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}
```

បន្ទាប់មកទៀត យើងនឹងមាន Board component ដែលទទួលយក `squares` ហើយនិង `onClick` props ពី Game component។ ដែលឥឡូវនេះយើងមាន​ click handler តែមួយក្នុង Board សម្រាប់ Squares ជាច្រើន, យើងនឹងត្រូវតែ pass ទីតាំងនៃ Square នីមួយៗទៅក្នុង `onClick` handler ដើម្បីបង្ហាញថា Square មួយណាដែលត្រូវបាន click។ នេះគឺជាជំហានចាំបាច់ដើម្បីផ្លាស់ប្តូរ Board component៖

* លុប `constructor` ក្នុង Board។
* ជំនួស `this.state.squares[i]` ជាមួយ `this.props.squares[i]` ក្នុង `renderSquare` របស់ Board។
* ជំនួស `this.handleClick(i)` ជាមួយ `this.props.onClick(i)` ក្នុង `renderSquare` របស់ Board។

Board component ឥឡូវនេះមើលទៅដូចនេះ៖

```javascript{17,18}
class Board extends React.Component {
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.props.squares[i]}
        onClick={() => this.props.onClick(i)}
      />
    );
  }

  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

យើងនឹងធ្វើបច្ចុប្បន្នភាព​ `render` function របស់ Game component ដើម្បី history entry ថ្មី​បំផុតដើម្បីកំណត់និងបង្ហាញ status របស់ game៖

```javascript{2-11,16-19,22}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
```

Game component ឥឡូវ​នេះគឺកំពុង render status របស់ game, យើងអាចដកចេញកូដដែលត្រូវគ្នាពី `render` method របស់ Board។ បន្ទាប់ពីការ refactor `render` function របស់​​ Board មើលទៅដូចនេះ៖

```js{1-4}
  render() {
    return (
      <div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
```

ទីបំផុត យើងត្រូវផ្លាស់ទី `handleClick` method ពី Board component ទៅក្នុង Game component។ យើងក៏ត្រូវកែប្រែ `handleClick` ផងដែរពីព្រេាះ state របស់ Game component គឺត្រូវបានរៀបរចនាសម្ព័ន្ធខុសគ្នា។ នៅក្នុង `handleClick` method របស់ Game យើងបានដាក់បញ្ចូលនូវ history ថ្មីទៅក្នុង `history`។

```javascript{2-4,10-12}
  handleClick(i) {
    const history = this.state.history;
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares,
      }]),
      xIsNext: !this.state.xIsNext,
    });
  }
```

>ចំណាំ
>
>មិន​ដូច array `push()` method ដែលអ្នកអាចនឹងស្គាល់កាន់តែច្បាស់ជាមួយ, `concat()` method មិនផ្លាស់ប្តូរ original array ដូច្នេះយើងចូលចិត្តវា។

នៅចំណុចនេះ Board component ត្រូវការតែ `renderSquare` ហើយនិង `render` methods។ State របស់ game ហើយនិង `handleClick` method គួរតែនៅក្នុង Game component។

**[View the full code at this point](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)**

### Showing the Past Moves {#showing-the-past-moves}

យើងកំពុងថតទុកនូវ history របស់ tic-tac-toe​ ហ្គេម ឥឡូវនេះយើងអាចបង្ហាញវាដល់អ្នកលេងជា list នៃការផ្លាស់ប្តូរពីមុនៗ។

យើងបានរៀនពីមុនមកហើយថា React elements គឺជា first-class JavaScript objects; យើងអាចបញ្ជូនពួកវាទៅវិញទៅមកក្នុង applications របស់យើង។ ដើម្បី render items ច្រើនក្នុង React យើងអាចប្រើ array នៃ React elements។

ក្នុង JavaScript arrays មាន [`map()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) មួយដែលត្រូវបានប្រើជាទូទៅសម្រាប់ការ map data ទៅកាន់ data ផ្សេងទៀត៖

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```

ការប្រើ `map` method យើងអាច​​ map history នៃការផ្លាស់ទី history ទៅកាន់ React elements ដែលតំណាងឱ្យប៊ូតុងនៅលើអេក្រង់ ហើយនិងបង្ហាញ list នៃប៊ូតុងដើម្បី "លោត" ទៅកាន់ការផ្លាស់ប្តូរពីមុនៗ។

តោះ `map` ទៅលើ `history` ក្នុង `render` method របស់ Game៖

```javascript{6-15,34}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{moves}</ol>
        </div>
      </div>
    );
  }
```

**[View the full code at this point](https://codepen.io/gaearon/pen/EmmGEa?editors=0010)**

<<<<<<< HEAD
សម្រាប់ការផ្លាស់ប្តូរនីមួយៗក្នុង history របស់ tic-tac-toes ហ្គេម យើងបង្កើត list នៃ item `<li>` ដែលមានប៊ូតុងមួយ `<button>`។ ប៊ូតុងមាន `onClick` handler មួយដែល calls method មួយមានឈ្មេាះថា `this.jumpTo()`។ យើងមិនបាន implement `jumpTo()` method នៅឡើយទេ។ សម្រាប់ពេលនេះយើងគួរតែមើលឃើញ list នៃការផ្លាស់ទីដែលបានកើតឡើងនៅក្នុងហ្គេមហើយនិង warning ក្នុង developer tools console ដែលនិយាយថា៖
=======
For each move in the tic-tac-toe game's history, we create a list item `<li>` which contains a button `<button>`. The button has a `onClick` handler which calls a method called `this.jumpTo()`. We haven't implemented the `jumpTo()` method yet. For now, we should see a list of the moves that have occurred in the game and a warning in the developer tools console that says:
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

>  Warning:
>  Each child in an array or iterator should have a unique "key" prop. Check the render method of "Game".

ចូរពិភាក្សាថាតើ warning ខាងលើមានន័យយ៉ាងដូចម៉្តេច។

### Picking a Key {#picking-a-key}

នៅពេលដែលយើង render list មួយ React រក្សារទុកព័ត៌មានមួយចំនួនពី list item នីមួយៗដែលបាន render។ នៅពេលយើងធ្វើបច្ចុប្បន្នភាព list React ត្រូវការកំណត់នូវអ្វីដែលបានផ្លាស់ប្តូរ។ យើងអាចបន្ថែមបាន៖ យកចេញបាន រៀបចំឡើងវិញបាន ឬក៏ធ្វើបច្ចុប្បន្នភាពបាននូវ​ items របស់​​ list។

ស្រមៃពីការផ្លាស់ប្តូរពី

```html
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

ទៅជា

```html
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

បន្ថែមពីលើការធ្វើបច្ចុប្បន្នភាព counts, នៅពេលដែលអ្នកណាម្នាក់អានវាប្រហែលជានិយាយថា យើងបានផ្លាស់ប្តូរតម្រៀបរបស់ Alex និង Ben ហើយបានបញ្ចូល Claudia នៅចន្លេាះ Alexa និង Ben។ ទោះយ៉ាងណា React គឺជា computer program និង មិនដឹងថាយើងចង់បានអ្វីទេ។ ពីព្រេាះ React មិនអាចដឹងពីបំណងរបស់យើងទេ, ជម្រើសមួយគឺត្រូវប្រើ strings `alexa`, `ben`, `claudia`។ ប្រសិនបើយើងបង្ហាញ data ពី database, database IDs របស់ Alexa, Ben, និង Claudia អាចត្រូវបានប្រើជា keys។

```html
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```

នៅពេលដែល list ត្រូវបាន re-render React ទទួលយក key របស់ item list នីមួយៗហើយស្វែងរក items របស់ list ពីមុនៗសម្រាប់ការផ្គូផ្គង key។ ប្រសិនបើ list ​បច្ចុប្បន្នមាន key ដែលមិនមានពីមុនមក React នឹងបង្កើត component មួយ។ ប្រសិនបើ list ​បច្ចុប្បន្នមិនមាន key ដែលមានក្នុង list ពីមុនៗ React នឹងបំផ្លាញ component ពីមុន។ ប្រសិនបើ keys ផ្គូផ្គងត្រូវ component ដែលត្រូវគ្នាត្រូវបានផ្លាស់ប្តូរ។ Keys ប្រាប់ React ពីអត្តសញ្ញាណនៃ component នីមួយៗដែលអនុញ្ញាតឱ្យ React រក្សាទុក state នៅពេល re-renders។ ​ប្រសិនបើ key របស់ component ផ្លាស់ប្តូរ component នឹងត្រូវបានបំផ្លាញហើយនិងត្រូវបានបង្កើតឡើងវិញជាមួយ state ថ្មី។

`key` គឺ property ដែលពិសេសនៅក្នុង React (ភ្ជាប់មកជាមួយ `ref`, លក្ខណៈពិសេសកម្រិតខ្ពស់)។ នៅពេលដែល element ត្រូវបានបង្កើត React ទាញយក `key` property ហើយនិងរក្សារទុក key ដោយផ្ទាល់នៅលើ element ដែលត្រូវបាន return។ ទោះ​បី​ជា `key` អាចមើលទៅដូចជាវាស្ថិតនៅក្នុង `props`, `key` មិនអាចត្រូវបាន reference ដោយការប្រើ `this.props.key`។ React ប្រើ `key` ដោយស្វ័យប្រវត្តិដើម្បីសម្រេចថាតើ componenet មួយណាដែលត្រូវធ្វើបច្ចុប្បន្នភាព។ Component មិនអាចសួរអំពី `key` របស់ខ្លួនវាទេ។

**វាត្រូវបានផ្ដល់អនុសាសន៍យ៉ាងមុតមាំថាអ្នក assign proper keys គ្រប់ពេលដែលអ្នកបង្កើត dynamic list។** ប្រសិនបើអ្នកមិនមាន key ដែលសមរម្យអាចប្រើការបាន អ្នកប្រហែលចង់ពិចារណារៀបចំរចនាសម្ព័ន្ធទិន្នន័យរបស់អ្នកឡើងវិញដូច្នេះអ្នកធ្វើវាទៅ។

ប្រសិនបើមិនមាន key ត្រូវបានបញ្ជាក់ React នឹងបង្ហាញការព្រមាននិងការប្រើប្រាស់ array index ជា key ដោយ default។ ការប្រើ array index ជា key គឺមានបញ្ហានៅពេលព្យាយាម re-order items របស់ list ឬក៏ បញ្ចូល/យកចេញ នូវ list items។ ជាក់ស្តែងការបញ្ជូន `key={i}` អាចបំបាត់ការព្រមាន ប៉ុន្តែមានបញ្ហាដូចគ្នាដូចជា array indices ហើយនិងមិនត្រូវបានណែនាំនៅក្នុងករណីភាគច្រើន។

Keys មិនចាំបាច់ជា globally unique; ពួកគេគ្រាន់តែត្រូវការជា unique រវាង components ហើយនិង siblings របស់ពួកវា។


### Implementing Time Travel {#implementing-time-travel}

នៅក្នុង history រ​បស់ tic-tac-toe ហ្គេម រាល់ការផ្លាស់ទីនីមួយៗពីមុនគឺមាន unique ID ដែលទាក់ទងជាមួយវា៖ វាជាចំនួនលេខតគ្នានៃការផ្លាស់ទី។
ការផ្លាស់ទីគឺមិនដែលត្រូវបាន re-order  លុប ឬបញ្ចូលនៅកណ្តាល ដូច្នេះវាមានសុវត្ថិភាពក្នុងការប្រើ move index ជា key។

នៅក្នុង `render` method របស់ Game component យើងអាចបន្ថែម key ដូចនេះ `<li key={move}>` ហើយការព្រមានរបស់ React ពី keys គួរតែបាត់៖

```js{6}
    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li key={move}>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });
```

**[View the full code at this point](https://codepen.io/gaearon/pen/PmmXRE?editors=0010)**

ការចុចប៊ូតុងណាមួយរបស់ item នៅក្នុង list វានឹងបោះនូវ error ពីព្រេាះ `jumpTo` method មិនត្រូវបានកំណត់។​ មុនពេលដែលយើង implement `jumpTo`, យើងនឹងបន្ថែម `stepNumber` ទៅកាន់ state របស់ Game component ដើម្បីចង្អុលបង្ហាញថាជំហានមួយណាដែលយើងកំពុងមើល។

ដំបូង, បន្ថែម `stepNumber: 0` ជា state ដំបូងនៅក្នុង `constructor` របស់ Game៖

```js{8}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      stepNumber: 0,
      xIsNext: true,
    };
  }
```

បន្ទាប់មកទៀត, យើងនឹងកំណត់ `jumpTo` method ក្នុង Game ដើម្បី update `stepNumber`។ យើងក៏កំណត់ `xIsNext` ជា true ផងដែរប្រសិនបើលេខដែលយើងកំពុងផ្លាស់ប្តូរ `stepNumber` ជាចំនួនសេស៖

```javascript{5-10}
  handleClick(i) {
    // this method has not changed
  }

  jumpTo(step) {
    this.setState({
      stepNumber: step,
      xIsNext: (step % 2) === 0,
    });
  }

  render() {
    // this method has not changed
  }
```

ឥឡូវនេះយើងនឹងធ្វើការផ្លាស់ប្តូរមួយចំនួនជាមួយនិង `handleClick` method របស់ Game ដែលវានិង fires នៅពេលដែលអ្នកចុចលើ square។

`stepNumber` state ដែលយើងបានបន្ថែម វាឆ្លុះបញ្ចាំងពីការផ្លាស់ទីដែលបានបង្ហាញដល់អ្នកប្រើប្រាស់ឥឡូវនេះ។ បន្ទាប់ពីយើងធ្វើការផ្លាស់ទីថ្មី, យើងត្រូវ update `stepNumber` ដោយបន្ថែម `stepNumber: history.length` ជាផ្នែកមួយនៃ `this.setState` argument។ នេះធានាថាយើងមិនជាប់គាំងក្នុងការបង្ហាញការផ្លាស់ទី​ដូចគ្នាបន្ទាប់ពីការផ្លាស់ទីថ្មីមួយត្រូវបានបង្កើត។

យើងក៏នឹងជំនួស `this.state.history` ជាមួយ `this.state.history.slice(0, this.state.stepNumber + 1)`។ នេះធានាថា ប្រសិនបើយើង "ត្រឡប់ទៅវិញទាន់ពេល" ហើយបន្ទាប់មកទៀតបង្កើតការផ្លាស់ទីថ្មីពីចំនុចនេាះ, យើងបោះចោលនូវ "future" history ដែលនឹងក្លាយទៅជាមិនត្រឹមត្រូវពេលឥឡូវ​នេះ។

```javascript{2,13}
  handleClick(i) {
    const history = this.state.history.slice(0, this.state.stepNumber + 1);
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares
      }]),
      stepNumber: history.length,
      xIsNext: !this.state.xIsNext,
    });
  }
```

ទីបំផុត យើងនឹងកែប្ `render` method របស់ Game component ដែលតែងតែ render ការផ្លាស់ទីចុងក្រោយ ទៅជា render ការផ្លាស់ទីដែលត្រូវបានជ្រើសរើសដោយយោងតាម `stepNumber`៖

```javascript{3}
  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // the rest has not changed
```

ប្រសិនបើយើងចុចលើជំហានណាមួយនៅក្នុង history របស់ game, tic-tac-toe board គួរធ្វើបច្ចុប្បន្នភាពភ្លាមៗដើម្បីបង្ហាញថា board មើលទៅដូចជាអ្វីបន្ទាប់ពីជំហាននោះបានកើតឡើង។

**[View the full code at this point](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

### Wrapping Up {#wrapping-up}

សូមអបអរសាទរ! អ្នកបានបង្កើតហ្គេម tic-tac-toe មួយដែល៖

* អនុញ្ញាតឱ្យអ្នកលេង tic-tac-toe
* បង្ហាញប្រាប់នៅពេលដែលអ្នកលេងបានឈ្នះការប្រកួត
* រក្សារ history របស់ហ្គេមដែលជាដំណើរការហ្គេម
* អនុញ្ញាតឱ្យអ្នកលេងពិនិត្យឡើងវិញនូវ history របស់ហ្គេម ហើយនិងមើលឃើញនូវ versions នៃ board របស់ហ្គេ​ម។

<<<<<<< HEAD
ការងារល្អ! យើងសង្ឃឹមថាឥឡូវនេះអ្នកមានអារម្មណ៍ថាអ្នកមានការយល់ដឹងសមរម្យពីរបៀបដែល React ធ្វើការ។
=======
Nice work! We hope you now feel like you have a decent grasp of how React works.
>>>>>>> 23d03a854ba21aeea0a03a0bd5185e0def9237d6

មើលលទ្ធផលចុងក្រោយនៅទីនេះ៖ **[Final Result](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**។

ប្រសិនបើអ្នកមានពេលបន្ថែមឬចង់អនុវត្តជំនាញថ្មី React របស់អ្នក នៅទីនេះគឺមានគំនិតមួយចំនួនសម្រាប់ការប្រសើរឡើងរបស់អ្នក អ្នកអាចបង្កើត tic-tac-toe ហ្គេម ដែលត្រូវបានមានការបង្កើនការលំបាកដូចខាងក្រោម៖

1. បង្ហាញទីតាំងនៃការផ្លាស់ប្តូរទីជាមួយទំរង់ (ជួរឈរ, ជួរដេក) នៅក្នុងបញ្ជី history នៃការផ្លាស់ប្តូរទី។
2. Bold នូវ item ដែលបានកំពុង​ select នៅក្នុង list។
3. សរសេរ Board ឡើងវិញដោយប្រើ loops ពីរដើម្បីបង្កើត squares ជំនួសអោយ hardcoding ពួកវា។
4. បន្ថែមប៊ូតុងបិទ/បើកមួយ ដែលអនុញ្ញាតឱ្យអ្នកតម្រៀបការផ្លាស់ទីក្នុងលំដាប់ឡើងឬចុះក្រោម។
5. នៅពេលមានអ្នកណាម្នាក់ឈ្នះ highlight squares បី ដែលបណ្តាលឱ្យឈ្នះ។
6. នៅពេលគ្មាននរណាម្នាក់ឈ្នះ បង្ហាញសារអំពីលទ្ធផលស្មើ។

តាមរយៈ tutorial នេះ យើងបានប៉ះ React concepts រួមទាំង elements, components, props, and state។ សម្រាប់ការពន្យល់លម្អិតបន្ថែមលើប្រធានបទនីមួយៗ សូមឆែក [the rest of the documentation](/docs/hello-world.html)។ ដើម្បីស្វែងយល់បន្ថែមពីការកំណត់ components សូមឆែក [`React.Component` API reference](/docs/react-component.html)។
