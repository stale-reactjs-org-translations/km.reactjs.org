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

យើងនិងបង្កើតហ្គេមដ៏តូចមួយនៅក្នុង tutorial នេះ។ **អ្នកអាច skip វាបានពីព្រេាះអ្នកមិនមែនជាអ្នកបង្កើតហ្គេមនេាះទេ -- ប៉ុន្តែអ្នកគួរតែសាកល្បងវា។**  Techniques ដែលអ្នកនិងរៀននៅក្នុង tutorial នេះគឺមូលដ្ឋានគ្រឺះដើម្បីបង្កើត React apps, ហើយនិងការយល់ដឹងយ៉ាងសុីជម្រៅពី React។

>ពត៌មានជំនួយ
>
>Tutorial នេះគេ design សម្រាប់អ្នកដែលចូលចិត្ត**រៀនដោយការអនុវត្តន៍**។ ប្រសិនជាអ្នកចង់រៀន concept មូលដ្ឋានតំបូងរបស់​ React, អ្នកអាចឆែកមើល [step-by-step guide](/docs/hello-world.html) របស់យើងបាន។ អ្នកប្រាកដជាយល់ឃើញថា​​ tutorail នេះហើយនិង step-by-step guid គឺបំពេញឱ្យគ្នាទៅវិញទៅមក។

Tutorail នេះត្រូវបានគេបែងចែកជាច្រើនផ្នែក​ដូចខាងក្រោម​៖

* [ការរៀបចំសម្រាប់ ​Tutorial](#setup-for-the-tutorial) នឹងផ្តល់ឱ្យអ្នកនូវ**ចំណុចចាប់ផ្តើមមួយ**ដើម្បីអនុវត្តតាមការបង្រៀន។
* [ទិដ្ឋភាពទូទៅ](#overview) នឹងបង្រៀនអ្នកនូវ**មូលដ្ឋានគ្រឹះ**ពី React ដូចជា៖ components, props, and state។
* [Completing the Game](#completing-the-game) នឹងបង្រៀនអ្នកនូវ**បច្ចេកទេសទូទៅបំផុត**ក្នុងការ develop React។
* [Adding Time Travel](#adding-time-travel) នឹងផ្តល់ឱ្យអ្នកនូវ**ការយល់ដឹងកាន់តែស៊ីជម្រៅ**នៃចំណុចខ្លាំងតែមួយគត់របស់ React។

អ្នកមិនចាំបាច់រៀនគ្រប់ផ្នែកទាំងអស់ក្នុងពេលតែមួយនេាះទេ។ អ្នកអាចរៀនផ្នែកណាមួយតាមតែអ្នកអាចធ្វើទៅបាន -- អ្នកអាចរៀនមួយផ្នែកឬក៏ពីរផ្នែក។

អ្នកអាច copy ហើយ paste កូដនៅពេលដែលអ្នកកំពុងអនុវត្តតាម tutorial, ប៉ុន្តែយើងសូមផ្តល់អនុសាសន៍អោយអ្នកវាយកូដដោយខ្លួនឯងផ្ទាល់។ ព្រេាះវាអាចជួយអ្នកឱ្យកាន់តែចងចាំនិងយល់កាន់តែច្បាស់។

### តើយើងនឹងបង្កើតអ្វី?    {#what-are-we-building}

នៅក្នុង tutorial នេះ, យើងនឹងបង្ហាយពីរបៀបបង្កើតហ្គេម tic-tac-toe ជាមួយនិង React។

អ្នកអាចឃើញអ្វីដែលយើងនឹងបង្កើតនៅទីនេះ៖ **[Final Result](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**។ ប្រសិនជាអ្នកមិនយល់ពីកូដ, ឬក៏អ្នកមិនច្បាស់ជាមួយនិង syntax របស់កូដ, សូមកុំបារម្មណ៏អី! គោលដៅនៃ tutorial នេះគឺជួយអ្នកឱ្យយល់ច្បាស់ពី React ហើយនិង syntax របស់ React។

យើងសូមផ្តល់អនុសាសន៍អោយអ្នកឆែកមើលហ្គេម​ tic-tac-toe នេះជាមុនសិនមុនពេលដែលបន្តជាមួយនិង tutorial ទៅមុខទៀត។ លក្ខណៈពិសេសមួយដែលអ្នកនឹងសម្គាល់គឺថាមានតារាងលេខនៅខាងស្តាំនៃ board របស់ហ្គេម។ តារាងនេះកត់ត្រានូវ history នៃការលេងរបស់ user, ហើយ​ history វានិង update នៅពេលដែលហ្គេមដំណើរការ។

អ្នកអាចបិទហ្គេម tic-tac-toe នេះបាននៅពេលដែលអ្នកយល់ពីដំណើរការរបស់វា។ យើងនឹងចាប់ផ្តើមជាមួយនិង template ដ៏សាមញ្ញមួយនៅក្នុង tutorial នេះ។​​ ជំហានបន្ទាប់របស់យើងគឺរៀបចំអោយអ្នកអាចចាប់ផ្តើមបង្កើតហ្គេមនេះបាន។

### តម្រូវការជាមុន   {#prerequisites}

យើងនឹងសន្មតថាអ្នកមានចំណេះដឹងខ្លះៗពី HTML ហើយនិង JavaScript, ប៉ុន្តែអ្នកគួរតែអាចអនុវត្តវាបានបើទេាះបីជាអ្នកមានចំណេះដឹងពីភាសា programming ផ្សេងៗក៏ដោយ។ យើងនឹងសន្មតផងដែរថាអ្នកមានចំណេះដឹងពី concept របស់ programming ដូចជា៖ functions, objects, arrays, and to a lesser extent, classes។

បើសិនជាអ្នកត្រូវការ review JavaScript, យើងសូមផ្តល់យោបល់ឱ្យអាន [this guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)។ សូមកត់ចំណាំថាយើងនឹងប្រើ features មួយចំនួនរបស់ ES6 ផងដែរ -- កំណែទំរង់ថ្មីរបស់ JavaScript. នៅក្នុង tutorial នេះ, យើងនឹងប្រើ [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), ហើយនិង [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) statements. អ្នកអាចប្រើ [Babel REPL](babel://es5-syntax-example) ដើម្បីឆែកមើលថាតើ code របស់ ES6 នឹង compile ទៅជាអ្វី។

## ការរៀបចំសម្រាប់ ​Tutorial {#setup-for-the-tutorial}

មានពីរវិធីដើម្បីអនុវត្តការសរសេរកូដនៅក្នុង tutorial នេះ៖ អ្នកអាចសរសេរកូដនៅលើ browser របស់អ្នកផ្ទាល់, ឬក៏អ្នកអាចរៀបចំ environment ក្នុងការ development នៅក្នុងកុំព្យូទ័ររបស់អ្នក។

### ជម្រើសទី១៖  សរសេរកូដនៅលើ browser {#setup-option-1-write-code-in-the-browser}

នេះជាវិធីលឿនបំផុតក្នុងការចាប់ផ្តើម!

តំបូង, សូមបើក **[Starter Code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)** នេះនៅក្នុងផ្ទាំងថ្មីមួយរបស់ browser​។ ផ្ទាំថ្មីគួរតែបង្ហាយ board ទទេមួយរបស់ហ្គេម tic-tac-toe ហើយនិងកូដ React. យើងនឹង edit កូដ​ របស់ React នៅក្នុង tutorial នេះ។

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

6. Add these three lines to the top of `index.js` in the `src/` folder:

៦. បន្ថែមកូដបីបន្ទាត់ខាងក្រោមទៅផ្នែកខាងលើគេនៃ `index.js` ដែលស្ថិតនៅក្នុងថតឯកសារ `src/`៖

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

ឥឡូវនេះប្រសិនបើអ្នក run `npm start` នៅក្នុងថតឯកសាររបស់ project ហើយបើក `http://localhost:3000` នៅលើ browser, អ្នកគួរតែឃើញ tic-tac-toe ហ្គេមទទេមួយ។

យើងសូមផ្តល់អនុសាសន៍ [these instructions](https://babeljs.io/docs/editors/) ដើម្បីកំណត់ syntax highlighting សម្រាប់ editor របស់អ្នក។

</details>

### ជំនួយ, ខ្ញុំជាប់គាំងហើយ!   {#help-im-stuck}

ប្រសិនជាអ្នកជាប់គាំង, អ្នកអាចឆែកមើល [community support resources](/community/support.html). ជាពិសេស, [Reactiflux Chat](https://discord.gg/0ZcbPKXt5bZjGY5n) គឺជាវិធីដ៏ល្អមួយដើម្បីទទួលបានជំនួយយ៉ាងឆាប់រហ័ស។ ប្រសិនបើអ្នកមិនទទួលបានចម្លើយទេ, ឬប្រសិនបើអ្នកនៅជាប់គាំង, សូមរាយការណ៍នូវបញ្ហា, ហើយយើងនឹងជួយអ្នក។

## ទិដ្ឋភាពទូទៅ   {#overview}

ឥឡូវនេះអ្នកបានធ្វើការរៀបចំសម្រាប់ tutorial នេះរួចរាល់ហើយ, តេាះចាប់ផ្តើមនូវទិដ្ឋភាពទូទៅរបស់ React!

### តើអ្វីជា React? {#what-is-react}

React គឺជាការប្រកាស, ប្រសិទ្ធិភាព, ហើយនិង JavaScript library ដែល flexible មួយសម្រាប់បង្កើត user interfaces។ វាអនុញ្ញាតឱ្យអ្នកបង្កើត UIs ដែលស្មុគស្មាញ ពីបំណែកតូចៗនិងដាច់ពីគ្នានៃកូដដែលគេហៅថា "components"។

React មាន component ដែលមានប្រភេទផ្សេងៗពីគ្នាផងដែរ, ប៉ុន្តែយើងនឹងចាប់ផ្តើមជាមួយនិង `React.Component` subclasses​៖

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

នេះ, ShoppingList គឺជា **React component class** មួយ, ឬក៏ **React component type** មួយ។ component ទទួលយក parameters, ដែលគេហៅថា `props` (ពាក្យពេញ "properties"), ហើយ returns នូវ hierarchy នៃ views មួយដើម្បីបង្ហាយតាមរយៈ `render` method។

`render` method return នូវ *description* នៃអ្វីដែលអ្នកចង់ឃើញនៅលើអេក្រង់។​ React ទទួលយក description ហើយបង្ហាយលទ្ធផល។ ជាពិសេស, `render` return នូវ **React element** មួយ, ដែលជា description ដ៏ស្រាលមួយដែលត្រូវ render។ React developers ភាគច្រើនប្រើនូវ special syntax ដែលគេហៅថា "JSX"​ ដែលបង្កើតជា structures ងាយស្រួលក្នុងការសរសេរ។  `<div />` syntax គឺត្រូវបានគេបំលែងទៅជា `React.createElement('div')` នៅពេល build time។ ឧទាហរណ៍ខាងលើគឺស្មើទៅនឹង៖

```javascript
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

[See full expanded version.](babel://tutorial-expanded-version)

ប្រសិនជាអ្នកចង់ដឹងចង់ឃើញ, `createElement()` ត្រូវបានគេរៀបរាប់លម្អិតបន្ថែមនៅក្នុង [API reference](/docs/react-api.html#createelement), ប៉ុន្តែយើងនឹងមិនប្រើវានៅក្នុង tutorial នេះទេ។ ផ្ទយទៅវិញ, យើងនឹងបន្តប្រើ JSX.

JSX comes with the full power of JavaScript. You can put *any* JavaScript expressions within braces inside JSX. Each React element is a JavaScript object that you can store in a variable or pass around in your program.

JSX ភ្ជាប់មកជាមួយនូវអានុភាពរបស់ JavaScript។ អ្នកអាចដាក់ expressions *ណាមួយ* របស់ JavaScript នៅក្នុងដង្កៀបខាងក្នុង​ JSX។ React element នីមួយៗគឺជា JavaScript object ដែលអ្នកអាចផ្ទុកនៅក្នុង variable ឬក៏អាច pass នៅក្នុង program របស់អ្នក។

`ShoppingList` component ដែលនៅខាងលើគឺ renders តែ built-in DOM components តែប៉ុណ្ណេះដូចជា `<div />` ហើយនិ `<li />`។ ប៉ុន្តែអ្នកអាចបង្កើតហើយនិង render custom React components ផងដែរ។ ឧទាហរណ៍, ឥឡូវ​នេះយើងអាចយោងទៅលើ shopping list ដោយសរសេរ `<ShoppingList />`។ React component នីមួយៗគឺ encapsulated ហើយនិង
អាចដំណើរការដោយឯករាជ្យ; នេះអនុញ្ញាតឱ្យអ្នកបង្កើត UI ដែលស្មុគ្រស្មាញពី components ដែលសាមញ្ញ។

## ការត្រួតពិនិត្យ   Starter Code {#inspecting-the-starter-code}

បើសិនជាអ្នកនិងធ្វើការលើ tutorial **នៅក្នុង  browser,** បើកកូដនេះក្នុងផ្ទាំងថ្មី៖ **[Starter Code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)**។ បើសិនជាអ្នកនឹងធ្វើការលើ tutorial **នៅក្នុងកុំព្យូទ័ររបស់អ្នក**, បើក `src/index.js` នៅក្នុងថតឯកសាររបស់ project (អ្នកបានប៉ះឯកសារនេះរួចហើយកំឡុងពេល [setup](#setup-option-2-local-development-environment))

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
```

ផ្លាស់ប្តូរ `render` method របស់ Square component ដើម្បីបង្ហាយ value ដោយការជំនួសដោយ `{/* TODO */}` ជាមួយនិង `{this.props.value}`​៖

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

អបអរសាទរ! អ្នកទើបតែបាន "បញ្ជូន prop មួយ" ពី parent Board component ទៅកាន់ child Square component។ ការបញ្ជូន props គឺជារបៀបដែលពត៌មានហូរនៅក្នុង React apps, ពី parent ទៅកាន់ children។

### ការបង្កើត Interactive Component មួយ {#making-an-interactive-component}

តេាះបំពេញ Square component ជាមួយនិង "X" នៅពេលដែលយើង click វា។ តំបូង, ផ្លាស់ប្តូរ button tag ដែលត្រូវបានគេ return ពី `render()` function របស់ Square component​ ដូចខាងក្រោម៖

```javascript{4}
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { alert('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

ប្រសិនជាយើង click លើ Square ឥឡូវ​នេះ, យើងគួរតែទទួលបាននូវ alert មួយនៅក្នុង browser យើង។

សម្រាប់ event handlers 

>ចំណាំ
>
>ដើម្បីជាជំនួយក្នុងការ typing ហើយនិងជៀសវាង [ការភាន់ច្រឡំនូវ behavior របស់ `this`](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/), យើងនឹងប្រើ​ [arrow function syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) សម្រាប់ event handlers នៅទីនេះហើយនិងពេលខាងមុខទៀត៖
>
>```javascript{4}
>class Square extends React.Component {
>  render() {
>    return (
>      <button className="square" onClick={() => alert('click')}>
>        {this.props.value}
>      </button>
>    );
>  }
>}
>```
>
>សូមកត់សម្គាល់ពីបៀបជាមួយ `onClick={() => alert('click')}`, យើងនឹងបញ្ជូន *function មួយ* ជា `onClick` prop។ វា fire តែពេលបន្ទាប់ពី click តែប៉ុណ្ណោះ។ បំភ្លេច `() =>` ហើយសរសេរ `onClick={alert('click')}` គឺជាកំហុសធម្មតា, ហើយនិង fire ការ alert រាល់ពេលដែល component ធ្វើការ re-renders។

ជំហានបន្ទាប់, យើងចង់អោយ Square component "ចងចាំ" ថាវាត្រូវបានគេ click, ហើយនិងបំពេញវាជាមួយនិងសញ្ញា "X"។ ដើម្បី "ចងចាំ" អ្វីមួយ, component ប្រើ **state**។

React components អាចមាន state ដោយការកំណត់ `this.state` នៅក្នុង constructors។ `this.state` គួរតែត្រូវបានចាត់ទុកជា private នៅក្នុង React component។ តេាះរក្សារតម្លៃបច្ចុប្បន្នរបស់ Square នៅក្នុង `this.state`, ហើយផ្លាស់ប្តូរវានៅពេលដែល Square ត្រូវបាន click.

តំបូង, យើងនឹង add constructor មួយទៅអោយ class ដើម្បីកំណត់តម្លៃ state៖

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
      <button className="square" onClick={() => alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

>ចំណាំ
>
>នៅក្នុង [JavaScript classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), អ្នកតម្រូវអោយ call `super` នៅពេលធ្វើការកំណត់ constructor នៃ subclass។ React component classes ទាំងអស់ដែលមាន constructor គួរតែចាប់ផ្តើមជាមួយនិងការ call `super(props)`។

ឥឡូវ​នេះយើងនឹងផ្លាស់ប្តូរ `render` method របស់ Square ដើម្បីបង្ហាយតម្លៃ​បច្ចុប្បន្របស់ state នៅពេលដែលត្រូវបាន click៖

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

តាមរយៈការ call `this.setState` ពី `onClick` handler នៅក្នុង `render` method របស់ Square, យើងប្រាប់ React ធ្វើការ re-render Square គ្រប់ពេលដែល `<button>` ត្រូវបាន click។ បន្ទាប់ពីការ update, `this.state.value` របស់ Square នឹងប្តូរទៅជា `'X'`, ដូច្នេះយើងនឹងឃើញ `X` នៅលើ board របស់ហ្គេម។ បើអ្នក click លើ​​ Square ផ្សេងៗទៀត, `X` គួរតែបង្ហាយ។

នៅពេលដែលអ្នក call `setState` នៅក្នុង component មួយ, React នឹង update child component ដែលនៅក្នុងវាដោយស្វ័យប្រវត្តិ.

**[View the full code at this point](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)**

### Tools របស់ Developer {#developer-tools}

React Devtools extension សម្រាប់ [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) ហើយនិង [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/) អាចអោយអ្នកត្រួតពិនិត្យ React component tree ជាមួយ developer tools របស់ browser បាន។

<img src="../images/tutorial/devtools.png" alt="React Devtools" style="max-width: 100%">

React DevTools អាចអោយអ្នកឆែកមើល props ហើយនិង state របស់ React components បាន។

After installing React DevTools, you can right-click on any element on the page, click "Inspect" to open the developer tools, and the React tab will appear as the last tab to the right.

បន្ទាប់ពីដំឡើង React DevTools, អ្នកអាច right-click លើ element ដែលមាននៅលើ page, click "Inspect" ដើម្បីបើក developer tools, ហើយ React tab នឹងលេចឡើងនៅផ្ទាំងចុងក្រោយខាងស្តាំ។

**ទោះជាយ៉ាងណាក៏ដោយ, សូមកត់សម្គាល់ថាមានជំហានបន្ថែមមួយចំនួនទៀតដើម្បីអោយវាដំណើរការជាមួយ CodePen​៖**

1. ចូល log in ឬក៏ចុះឈ្មោះ ហើយបញ្ជាក់ email របស់អ្នក (ទាមទារដើម្បីទប់ស្កាត់សារឥតបានការ)។
2. Click លើ "Fork" ប៊ូតុង។
3. Click លើ "Change View" ហើយបន្ទាប់មកជ្រើសរើស "Debug mode"។​
4. នៅក្នុងផ្ទាំងថ្មីដែលបើក, devtools ឥឡូវនេះគួរតែមានផ្ទាំង React។

## Completing the Game {#completing-the-game}

ឥឡូវនេះយើងមានមូលដ្ឋានក្នុងការបង្កើត blocks សម្រាប់ tic-tac-toe ហ្គេមរបស់យើង។ ដើម្បីអោយបានហ្គេមមួយអោយពេញលេញ, ឥឡូវនេះយើងត្រូវដាក់ជំនួស "X"s ហើយនិង "O"s ទៅលើ board, ហើយយើងត្រូវការវិធីមួយដើម្បីកំណត់អ្នកឈ្នះ។

### Lifting State Up {#lifting-state-up}

បច្ចុប្បន្ន, Square component នីមួយៗរក្សារនូវ state របស់ហ្គេម។ ដើម្បីពិនិត្យរកអ្នកឈ្នះ, យើងនឹងរក្សារតម្លៃនីមួយៗរបស់ squares ទាំង៩នៅក្នុងទីតាំងមួយ។

យើងប្រហែលជាគិតថា Board គួរតែស្នើរសុំនូវតម្លៃ state របស់Square នីមួយៗ។ បើទោះបីជាវិធីសាស្រ្តនេះគឺអាចធ្វើទៅបាន សម្រាប់ React, យើងមិនលើកទឹកចិត្តអោយធ្វើតាមវិធីនេះទេពីព្រេាះកូដនឹងក្លាយទៅជាពិបាកយល់​, ងាយនិងមាន bugs, ហើយពិបាកក្នុការ refactor។ ជំនួសវិញ, វិធីសាស្រ្តដ៏ល្អបំផុតគឺត្រូវរក្សាទុក state របស់ហ្គេម នៅក្នុង parent Board component ជំនួសអោយការរក្សារទុកនៅក្នុង Square នីមួយៗ។ Board component អាចប្រាប់ Square នីមួយៗនូវអ្វីដែលត្រូវបង្ហាយដោយការបញ្ជូន props មួយ, [just like we did when we passed a number to each Square](#passing-data-through-props)។

**ដើម្បីប្រមូល data ពី children ជាច្រើន, ឬក៏ដើម្បីអោយ child components ២ទំនាក់ទំនងជាមួយគ្នាទៅវិញទៅមក, អ្នកត្រូវ declare state នៅក្នុង parent component។ Parent component អាចបញ្ជូន state ចុះទៅ់ children ដោយការប្រើ props; នេះអាចអោយ child components syn ជាមួយគ្នាទៅវិញទៅមក, ហើយនិង syn ជាមួយ parent component ផងដែរ។**



Lifting state into a parent component is common when React components are refactored -- let's take this opportunity to try it out. We'll add a constructor to the Board and set the Board's initial state to contain an array with 9 nulls. These 9 nulls correspond to the 9 squares:

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

When we fill the board in later, the board will look something like this:

```javascript
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

The Board's `renderSquare` method currently looks like this:

```javascript
  renderSquare(i) {
    return <Square value={i} />;
  }
```

In the beginning, we [passed the `value` prop down](#passing-data-through-props) from the Board to show numbers from 0 to 8 in every Square. In a different previous step, we replaced the numbers with an "X" mark [determined by Square's own state](#making-an-interactive-component). This is why Square currently ignores the `value` prop passed to it by the Board.

We will now use the prop passing mechanism again. We will modify the Board to instruct each individual Square about its current value (`'X'`, `'O'`, or `null`). We have already defined the `squares` array in the Board's constructor, and we will modify the Board's `renderSquare` method to read from it:

```javascript{2}
  renderSquare(i) {
    return <Square value={this.state.squares[i]} />;
  }
```

**[View the full code at this point](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)**

Each Square will now receive a `value` prop that will either be `'X'`, `'O'`, or `null` for empty squares.

Next, we need to change what happens when a Square is clicked. The Board component now maintains which squares are filled. We need to create a way for the Square to update the Board's state. Since state is considered to be private to a component that defines it, we cannot update the Board's state directly from Square.

To maintain the Board's state's privacy, we'll pass down a function from the Board to the Square. This function will get called when a Square is clicked. We'll change the `renderSquare` method in Board to:

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

>Note
>
>We split the returned element into multiple lines for readability, and added parentheses so that JavaScript doesn't insert a semicolon after `return` and break our code.

Now we're passing down two props from Board to Square: `value` and `onClick`. The `onClick` prop is a function that Square can call when clicked. We'll make the following changes to Square:

* Replace `this.state.value` with `this.props.value` in Square's `render` method
* Replace `this.setState()` with `this.props.onClick()` in Square's `render` method
* Delete the `constructor` from Square because Square no longer keeps track of the game's state

After these changes, the Square component looks like this:

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

When a Square is clicked, the `onClick` function provided by the Board is called. Here's a review of how this is achieved:

1. The `onClick` prop on the built-in DOM `<button>` component tells React to set up a click event listener.
2. When the button is clicked, React will call the `onClick` event handler that is defined in Square's `render()` method.
3. This event handler calls `this.props.onClick()`. The Square's `onClick` prop was specified by the Board.
4. Since the Board passed `onClick={() => this.handleClick(i)}` to Square, the Square calls `this.handleClick(i)` when clicked.
5. We have not defined the `handleClick()` method yet, so our code crashes.

>Note
>
>The DOM `<button>` element's `onClick` attribute has a special meaning to React because it is a built-in component. For custom components like Square, the naming is up to you. We could name the Square's `onClick` prop or Board's `handleClick` method differently. In React, however, it is a convention to use `on[Event]` names for props which represent events and `handle[Event]` for the methods which handle the events.

When we try to click a Square, we should get an error because we haven't defined `handleClick` yet. We'll now add `handleClick` to the Board class:

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

After these changes, we're again able to click on the Squares to fill them. However, now the state is stored in the Board component instead of the individual Square components. When the Board's state changes, the Square components re-render automatically. Keeping the state of all squares in the Board component will allow it to determine the winner in the future.

Since the Square components no longer maintain state, the Square components receive values from the Board component and inform the Board component when they're clicked. In React terms, the Square components are now **controlled components**. The Board has full control over them.

Note how in `handleClick`, we call `.slice()` to create a copy of the `squares` array to modify instead of modifying the existing array. We will explain why we create a copy of the `squares` array in the next section.

### Why Immutability Is Important {#why-immutability-is-important}

In the previous code example, we suggested that you use the `.slice()` operator to create a copy of the `squares` array to modify instead of modifying the existing array. We'll now discuss immutability and why immutability is important to learn.

There are generally two approaches to changing data. The first approach is to *mutate* the data by directly changing the data's values. The second approach is to replace the data with a new copy which has the desired changes.

#### Data Change with Mutation {#data-change-with-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

#### Data Change without Mutation {#data-change-without-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}

// Or if you are using object spread syntax proposal, you can write:
// var newPlayer = {...player, score: 2};
```

The end result is the same but by not mutating (or changing the underlying data) directly, we gain several benefits described below.

#### Complex Features Become Simple {#complex-features-become-simple}

Immutability makes complex features much easier to implement. Later in this tutorial, we will implement a "time travel" feature that allows us to review the tic-tac-toe game's history and "jump back" to previous moves. This functionality isn't specific to games -- an ability to undo and redo certain actions is a common requirement in applications. Avoiding direct data mutation lets us keep previous versions of the game's history intact, and reuse them later.

#### Detecting Changes {#detecting-changes}

Detecting changes in mutable objects is difficult because they are modified directly. This detection requires the mutable object to be compared to previous copies of itself and the entire object tree to be traversed.

Detecting changes in immutable objects is considerably easier. If the immutable object that is being referenced is different than the previous one, then the object has changed.

#### Determining When to Re-render in React {#determining-when-to-re-render-in-react}

The main benefit of immutability is that it helps you build _pure components_ in React. Immutable data can easily determine if changes have been made which helps to determine when a component requires re-rendering.

You can learn more about `shouldComponentUpdate()` and how you can build *pure components* by reading [Optimizing Performance](/docs/optimizing-performance.html#examples).

### Function Components {#function-components}

We'll now change the Square to be a **function component**.

In React, **function components** are a simpler way to write components that only contain a `render` method and don't have their own state. Instead of defining a class which extends `React.Component`, we can write a function that takes `props` as input and returns what should be rendered. Function components are less tedious to write than classes, and many components can be expressed this way.

Replace the Square class with this function:

```javascript
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

We have changed `this.props` to `props` both times it appears.

**[View the full code at this point](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)**

>Note
>
>When we modified the Square to be a function component, we also changed `onClick={() => this.props.onClick()}` to a shorter `onClick={props.onClick}` (note the lack of parentheses on *both* sides). In a class, we used an arrow function to access the correct `this` value, but in a function component we don't need to worry about `this`.

### Taking Turns {#taking-turns}

We now need to fix an obvious defect in our tic-tac-toe game: the "O"s cannot be marked on the board.

We'll set the first move to be "X" by default. We can set this default by modifying the initial state in our Board constructor:

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

Each time a player moves, `xIsNext` (a boolean) will be flipped to determine which player goes next and the game's state will be saved. We'll update the Board's `handleClick` function to flip the value of `xIsNext`:

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

With this change, "X"s and "O"s can take turns. Let's also change the "status" text in Board's `render` so that it displays which player has the next turn:

```javascript{2}
  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // the rest has not changed
```

After applying these changes, you should have this Board component:

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

Now that we show which player's turn is next, we should also show when the game is won and there are no more turns to make. We can determine a winner by adding this helper function to the end of the file:

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

We will call `calculateWinner(squares)` in the Board's `render` function to check if a player has won. If a player has won, we can display text such as "Winner: X" or "Winner: O". We'll replace the `status` declaration in Board's `render` function with this code:

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

We can now change the Board's `handleClick` function to return early by ignoring a click if someone has won the game or if a Square is already filled:

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

Congratulations! You now have a working tic-tac-toe game. And you've just learned the basics of React too. So *you're* probably the real winner here.

## Adding Time Travel {#adding-time-travel}

As a final exercise, let's make it possible to "go back in time" to the previous moves in the game.

### Storing a History of Moves {#storing-a-history-of-moves}

If we mutated the `squares` array, implementing time travel would be very difficult.

However, we used `slice()` to create a new copy of the `squares` array after every move, and [treated it as immutable](#why-immutability-is-important). This will allow us to store every past version of the `squares` array, and navigate between the turns that have already happened.

We'll store the past `squares` arrays in another array called `history`. The `history` array represents all board states, from the first to the last move, and has a shape like this:

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

Now we need to decide which component should own the `history` state.

### Lifting State Up, Again {#lifting-state-up-again}

We'll want the top-level Game component to display a list of past moves. It will need access to the `history` to do that, so we will place the `history` state in the top-level Game component.

Placing the `history` state into the Game component lets us remove the `squares` state from its child Board component. Just like we ["lifted state up"](#lifting-state-up) from the Square component into the Board component, we are now lifting it up from the Board into the top-level Game component. This gives the Game component full control over the Board's data, and lets it instruct the Board to render previous turns from the `history`.

First, we'll set up the initial state for the Game component within its constructor:

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

Next, we'll have the Board component receive `squares` and `onClick` props from the Game component. Since we now have a single click handler in Board for many Squares, we'll need to pass the location of each Square into the `onClick` handler to indicate which Square was clicked. Here are the required steps to transform the Board component:

* Delete the `constructor` in Board.
* Replace `this.state.squares[i]` with `this.props.squares[i]` in Board's `renderSquare`.
* Replace `this.handleClick(i)` with `this.props.onClick(i)` in Board's `renderSquare`.

The Board component now looks like this:

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

We'll update the Game component's `render` function to use the most recent history entry to determine and display the game's status:

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

Since the Game component is now rendering the game's status, we can remove the corresponding code from the Board's `render` method. After refactoring, the Board's `render` function looks like this:

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

Finally, we need to move the `handleClick` method from the Board component to the Game component. We also need to modify `handleClick` because the Game component's state is structured differently. Within the Game's `handleClick` method, we concatenate new history entries onto `history`.

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

>Note
>
>Unlike the array `push()` method you might be more familiar with, the `concat()` method doesn't mutate the original array, so we prefer it.

At this point, the Board component only needs the `renderSquare` and `render` methods. The game's state and the `handleClick` method should be in the Game component.

**[View the full code at this point](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)**

### Showing the Past Moves {#showing-the-past-moves}

Since we are recording the tic-tac-toe game's history, we can now display it to the player as a list of past moves.

We learned earlier that React elements are first-class JavaScript objects; we can pass them around in our applications. To render multiple items in React, we can use an array of React elements.

In JavaScript, arrays have a [`map()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) that is commonly used for mapping data to other data, for example:

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```

Using the `map` method, we can map our history of moves to React elements representing buttons on the screen, and display a list of buttons to "jump" to past moves.

Let's `map` over the `history` in the Game's `render` method:

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

For each move in the tic-tac-toes's game's history, we create a list item `<li>` which contains a button `<button>`. The button has a `onClick` handler which calls a method called `this.jumpTo()`. We haven't implemented the `jumpTo()` method yet. For now, we should see a list of the moves that have occurred in the game and a warning in the developer tools console that says:

>  Warning:
>  Each child in an array or iterator should have a unique "key" prop. Check the render method of "Game".

Let's discuss what the above warning means.

### Picking a Key {#picking-a-key}

When we render a list, React stores some information about each rendered list item. When we update a list, React needs to determine what has changed. We could have added, removed, re-arranged, or updated the list's items.

Imagine transitioning from

```html
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

to

```html
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

In addition to the updated counts, a human reading this would probably say that we swapped Alexa and Ben's ordering and inserted Claudia between Alexa and Ben. However, React is a computer program and does not know what we intended. Because React cannot know our intentions, we need to specify a *key* property for each list item to differentiate each list item from its siblings. One option would be to use the strings `alexa`, `ben`, `claudia`. If we were displaying data from a database, Alexa, Ben, and Claudia's database IDs could be used as keys.

```html
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```

When a list is re-rendered, React takes each list item's key and searches the previous list's items for a matching key. If the current list has a key that didn't exist before, React creates a component. If the current list is missing a key that existed in the previous list, React destroys the previous component. If two keys match, the corresponding component is moved. Keys tell React about the identity of each component which allows React to maintain state between re-renders. If a component's key changes, the component will be destroyed and re-created with a new state.

`key` is a special and reserved property in React (along with `ref`, a more advanced feature). When an element is created, React extracts the `key` property and stores the key directly on the returned element. Even though `key` may look like it belongs in `props`, `key` cannot be referenced using `this.props.key`. React automatically uses `key` to decide which components to update. A component cannot inquire about its `key`.

**It's strongly recommended that you assign proper keys whenever you build dynamic lists.** If you don't have an appropriate key, you may want to consider restructuring your data so that you do.

If no key is specified, React will present a warning and use the array index as a key by default. Using the array index as a key is problematic when trying to re-order a list's items or inserting/removing list items. Explicitly passing `key={i}` silences the warning but has the same problems as array indices and is not recommended in most cases.

Keys do not need to be globally unique; they only need to be unique between components and their siblings.


### Implementing Time Travel {#implementing-time-travel}

In the tic-tac-toe game's history, each past move has a unique ID associated with it: it's the sequential number of the move. The moves are never re-ordered, deleted, or inserted in the middle, so it's safe to use the move index as a key.

In the Game component's `render` method, we can add the key as `<li key={move}>` and React's warning about keys should disappear:

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

Clicking any of the list item's buttons throws an error because the `jumpTo` method is undefined. Before we implement `jumpTo`, we'll add `stepNumber` to the Game component's state to indicate which step we're currently viewing.

First, add `stepNumber: 0` to the initial state in Game's `constructor`:

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

Next, we'll define the `jumpTo` method in Game to update that `stepNumber`. We also set `xIsNext` to true if the number that we're changing `stepNumber` to is even:

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

We will now make a few changes to the Game's `handleClick` method which fires when you click on a square.

The `stepNumber` state we've added reflects the move displayed to the user now. After we make a new move, we need to update `stepNumber` by adding `stepNumber: history.length` as part of the `this.setState` argument. This ensures we don't get stuck showing the same move after a new one has been made.

We will also replace reading `this.state.history` with `this.state.history.slice(0, this.state.stepNumber + 1)`. This ensures that if we "go back in time" and then make a new move from that point, we throw away all the "future" history that would now become incorrect.

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

Finally, we will modify the Game component's `render` method from always rendering the last move to rendering the currently selected move according to `stepNumber`:

```javascript{3}
  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // the rest has not changed
```

If we click on any step in the game's history, the tic-tac-toe board should immediately update to show what the board looked like after that step occurred.

**[View the full code at this point](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

### Wrapping Up {#wrapping-up}

Congratulations! You've created a tic-tac-toe game that:

* Lets you play tic-tac-toe,
* Indicates when a player has won the game,
* Stores a game's history as a game progresses,
* Allows players to review a game's history and see previous versions of a game's board.

Nice work! We hope you now feel like you have a decent grasp on how React works.

Check out the final result here: **[Final Result](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**.

If you have extra time or want to practice your new React skills, here are some ideas for improvements that you could make to the tic-tac-toe game which are listed in order of increasing difficulty:

1. Display the location for each move in the format (col, row) in the move history list.
2. Bold the currently selected item in the move list.
3. Rewrite Board to use two loops to make the squares instead of hardcoding them.
4. Add a toggle button that lets you sort the moves in either ascending or descending order.
5. When someone wins, highlight the three squares that caused the win.
6. When no one wins, display a message about the result being a draw.

Throughout this tutorial, we touched on React concepts including elements, components, props, and state. For a more detailed explanation of each of these topics, check out [the rest of the documentation](/docs/hello-world.html). To learn more about defining components, check out the [`React.Component` API reference](/docs/react-component.html).
