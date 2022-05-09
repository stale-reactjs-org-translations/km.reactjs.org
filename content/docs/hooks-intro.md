---
id: hooks-intro
title: ការណែនាំអំពី Hooks
permalink: docs/hooks-intro.html
next: hooks-overview.html
---

*Hooks* គឺជាមុខងារថ្មីមួយនៅក្នុងជំនាន់ React 16.8 វាមានលក្ខណៈពិសេសដែលអាចឲ្យអ្នកប្រើប្រាស់ State និងមុខងារ React ដទៃទៀតដោយមិនចាំបាច់ class។

```js{4,5}
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

`useState` គឺជាមុខងារដំបូងរបស់ "Hook" ដែលយើងនឹងរៀនអំពីវាហើយឧទាហរណ៍ខាងលើនេះគ្រាន់តែគម្រូត្រួសៗតែប៉ុណ្ណោះ។ កុំទាន់ភ័យប្រសិនបើមិនទាន់យល់អំពីវា!

**អ្នកអាចរៀនអំពី Hooks [នៅទំព័របន្ទាប់](/docs/hooks-overview.html)។** នៅក្នុងទំព័រនេះ ពួកយើងនឹងពន្យល់អំពីហេតុផលដែលពួកយើងច្របាច់បញ្ចូល Hooks ទៅក្នុង React ព្រមទាំងវិធីសាស្ត្រនិងតិចនិចប្រើប្រាស់មួយចំនួនដែលអាចពន្លឿនដល់ការសរសេរកម្មវិធីមួយឲ្យកាន់តែអស្ចារ្យ។

>បញ្ជាក់
>
>React ១៦.៨.០ គឺជាកំណែរប្រែរដំបូងបំផុតដែលអាចប្រើប្រាស់ជាមួយ Hooks។ នៅពេលកំពុង upgrade, កុំភ្លេច update packages ទាំងអស់, រួមទាំង React DOM។
>React Native អាចប្រើប្រាស់ Hooks បានតាំងពី [React Native ជំនាន់ ០.៥៩](https://reactnative.dev/blog/2019/03/12/releasing-react-native-059)។

## វីដេអូនៃការណែនាំ {#video-introduction}

កាលពី React Conf 2018 Sophie Alpert ហើយនិង Dan Abramov បានបង្ហាញនិងណែនាំអំពី Hooks បន្ទាប់មកទៀត Ryan Florence បានឡើងមកបង្ហាញអំពីតិចនិចក្នុងការ refactor an application ដើម្បីអាចប្រើប្រាស់ជាមួយវា។ ទស្សនាវីដេអូនៅត្រង់នេះ៖

<br>

<iframe width="650" height="366" src="//www.youtube.com/embed/dpw9EHDh2bM" frameborder="0" allowfullscreen></iframe>

## No Breaking Changes {#no-breaking-changes}

មុនពេលបន្តទៅមុខទៀត គួរចំណាំថា Hooks គឺ៖

* **Completely opt-in** អ្នកអាចសាកល្បងជាមួយ Hooks នៅក្នុង components មួយចំនួនដោយមិនចាំបាច់សរសេរកូដឡើងវិញនោះទេ។ ហើយណាមួយ អ្នកក៏មិនចាំបាច់ត្រូវរៀន ឬក៏ប្រើប្រាស់វាឥលូវនេះដែរ ប្រសិនបើអ្នកមិនទាន់ចង់។
* **100% backwards-compatible** Hooks មិនមានផ្ទុក breaking changes ណាមួយទៅលើកំណែមុនៗនោះទេ។
* **Available now** Hooks អាចប្រើប្រាស់បានជាមួយកំណែ v16.8.0។

**វាគ្មានគម្រោងជាក់លាក់ណាមួយឡើយសម្រាប់ការដក classes ចេញពី React។** អ្នកអាចឆ្លៀតពេលអានអំពីវិធីសាស្ត្រនិងតិចនិករបស់ Hooks នៅ [ផ្នែកខាងក្រោម](#gradual-adoption-strategy) នៃទំព័រនេះ។

**Hooks មិនបានផ្លាស់ប្តូរ concepts ដែលអ្នកធ្លាប់ប្រើជាមួយ React នោះទេ។** ផ្ទុយទៅវិញ Hooks បានបន្ថែម direct API ទៅលើ React concepts ដែលយើងធ្លាប់បានប្រើមានដូចជា៖ props, state, context, refs, ហើយនិង lifecycle។ ពួកយើងនិងបង្ហាញនៅពេលក្រោយអំពីភាពដ៏អស្ចារ្យនៃការច្របាច់បញ្ចូលគ្នាជាមួយ Hooks។

**ប្រសិនបើអ្នកចង់ចាប់ផ្តើមរៀនអំពី Hooks។ ចុចត្រង់នេះ [ដើម្បីទៅកាន់ទំព័របន្ទាប់!](/docs/hooks-overview.html)** អ្នកអាចបន្តការអាននៅទំព័រនេះដើម្បីស្វែងយល់អំពីហេតុផលពីក្រោយនៃការច្របាច់បញ្ចូល Hooks ហើយនិងអំពីវិធីសាស្ត្រក៏ដូចជាតិចនិកមួយចំនួនដែលអាចឲ្យយើងប្រើប្រាស់វាដោយមិនចាំបាច់សរសេរកូដឡើងវិញ។

## ការជំរុញលើកទឹកចិត្ត {#motivation}

Hooks ដោះស្រាយ a wide variety of seemingly unconnected problems នៅក្នុង React ដែលពួកយើងបានជួបប្រទះជាងប្រាំឆ្នាំនៃការសរសេរ ក៏ដូចជាការ maintaining រាប់ពាន់ components។ ដូច្នេះមិនថាអ្នកកំពុងរៀន React ឬ កំពុងប្រើប្រាស់វា ឬក៏ប្រើ library ផ្សេងដែលស្រដៀងនិង component model របស់ React ក៏ដោយ អ្នកប្រហែលជាធ្លាប់ស្គាល់បញ្ហាទាំងនេះ។

### វាពិតជាពិបាកខ្លាំងមែនទែននៅពេលដែលចង់ប្រើ stateful logic ជាមួយនិង components ផ្សេងទៀត {#its-hard-to-reuse-stateful-logic-between-components}

React មិនបានផ្តល់នូវវិធី "attach" reusable behavior ទៅនិង component ទេ (ឧទាហរណ៍ connecting it to a store)។ ប្រសិនបើអ្នកធ្វើការជាមួយ React ពីមុនមក អ្នកប្រហែលជាធ្លាប់ឃើញ patterns ខ្លះៗដូចជា [render props](/docs/render-props.html) ហើយនិង [higher-order components](/docs/higher-order-components.html) ជាដើម ដែលវាបានព្យាយាមដោះស្រាយបញ្ហាទាំងអស់នេះ។ ក៏ប៉ុន្តែ patterns ទាំងនេះតម្រូវឲ្យ restructure components របស់អ្នកនៅពេលដែលត្រូវការវា ដែលវាធ្វើឲ្យកូដមើលទៅរៀងរញ៉េរញ៉ៃហើយពិបាកនិងតាម។ ប្រសិនបើអ្នកក្រឡេកទៅមើល a typical React application នៅក្នុង React DevTools អ្នកប្រាកដជាឃើញ a "wrapper hell" នៃ components ដែលហុំព័ទ្ធទៅដោយ layers of providers, consumers, higher-order components, render props, ហើយនិង abstractions មួយចំនួន។ អំឡុងពេលដែលយើងអាច  [filter them out in DevTools](https://github.com/facebook/react-devtools/pull/503) ត្រង់នេះហើយដែលជាចំនុចរសើបនៃ បញ្ហាដែលកប់នៅក្នុង React។ ដូច្នេះហើយ React ត្រូវការកែកុនឲ្យប្រសើរជាងមុនក្នុងការ sharing stateful logic។

ជាមួយនិង Hooks អ្នកអាច extract stateful logic ចេញពី component បាន ដូច្នេះវាធ្វើឲ្យមានភាពងាយស្រួលក្នុងការប្រតិបត្តិ tested independently ក៏ដូចជា reused ជាដើម។ **Hooks អាចឲ្យយើងប្រើប្រាស់ stateful logic ម្តងទៀតដោយមិនបាច់កែ component hierarchy** អញ្ចឹងហើយវាធ្វើឲ្យមានភាពងាយស្រួលក្នុងការចែករំលែក Hooks ទៅកាន់ components ដទៃទៀត ឬក៏ជាមួយនិង community ជាដើម។

ពួកយើងនឹងពិភាក្សាបន្ថែមអំពីវានៅក្នុង [Building Your Own Hooks](/docs/hooks-custom.html)។

### Complex components នឹងធ្វើឲ្យមានភាពស្មុគស្មាញហើយពិបាកយល់ {#complex-components-become-hard-to-understand}

ពួកយើងធ្លាប់ maintain components ជាច្រើន តាំងពីសាមញ្ញៗ រហូតដល់ថ្នាក់រញ៉េរញ៉ៃពិបាកគ្រប់គ្រង stateful logic ហើយនឹង side effects។ រាល់ lifecycle method តែងតែផ្ទុក a mix of unrelated logic។ ឧទាហរណ៍ជាក់ស្តែង components ធ្វើការទាញ data មួយចំនួននៅក្នុង `componentDidMount` ហើយនឹង `componentDidUpdate`។ ក៏ប៉ុន្តែ `componentDidMount` method ក៏មាន unrelated logic ខ្លះសម្រាប់ធ្វើការ sets up event listeners ហើយនិង cleanup performed នៅក្នុង `componentWillUnmount`។ កូដដែលពាក់ព័ន្ធគ្នា ត្រូវបានញែកទៅកន្លែងផ្សេងៗដាច់ពីគ្នា ចំណែកឯ កូដដែលមិនពាក់ព័ន្ទគ្នាសោះ ទុកបញ្ជៀតគ្នានៅក្នុង a single method។ ដូចនេះហើយវាធ្វើឱ្យមាន bugs ស្រួលបំផុត ហើយមើលទៅវា inconsistencies។

វាមានករណីផ្សេងៗគ្នា ហើយករណីមួយចំនួននោះគឺមិនអាចបំបែកទៅជា component តូចៗបានពីព្រោះមកពី stateful logic គឺមាននៅគ្រប់ទីកន្លែងទាំងអស់។ វាធ្វើឲ្យមានភាពពិបាកមែនទែនក្នុងការប្រតិបត្តិ test ម្តងៗ។ អញ្ចឹងហើយវាគឺជាហេតុផលមួយដែលអ្នកសរសេរ React ភាគច្រើនងាកទៅរក state management library។ ម្យ៉ាងទៀត ធ្វើអញ្ចឹងទៅវាមើលទៅរញ៉េរញ៉ៃខ្លាំងមែនទែន ដែលតម្រូវឲ្យអ្នក jump between different files ហើយនិងធ្វើឲ្យ ការប្រើប្រាស់ component ម្តងៗទៀតមានភាពពិបាក។

ដើម្បីដោះស្រាយបញ្ហានេះ **Hooks អាចឲ្យយើងចែក component ទៅជា functions តូចៗផ្អែកទៅលើតួនាទីរបស់វាតែប៉ុណ្ណោះ (មានដូចជា ការ setting up a subscription ឬក៏ fetching data ជាដើម)** ជៀសជាងការបំបែកនៅលើ lifecycle methods។ ម្យ៉ាងទៀត អ្នកក៏អាចចូលទៅក្នុង component យក local state របស់វាយកមកប្រើជាមួយនិង reducer តែម្តង ដែលវិធីនេះធ្វើឲ្យមានភាពងាយស្រួលមែនទែន។

ពួកយើងនឹងពិភាក្សាបន្ថែមអំពីវានៅក្នុង [Using the Effect Hook](/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns)។

### Classes ធ្វើឲ្យមានភាពភ័ណ្ឌច្រឡំទាំងអ្នកសរសេរនិងម៉ាស៊ីន {#classes-confuse-both-people-and-machines}

ជាក់ស្តែង ដើម្បីធ្វើឲ្យកូដ reuse ហើយ organize ឲ្យមានសណ្តាប់ធ្នាប់ល្អគឺវាពិតជាពិបាកខ្លាំងណាស់។ ពួកយើងយល់ឃើញថា classes គឺជាឧបសគ្គដ៏ធំមួយសម្រាប់ការរៀន React។ អ្នកគួរតែយល់ដឹងអំពីពាក្យ `this` ដែលជាតួអង្គសំខាន់មួយនៅក្នុងភាសា JavaScript ហើយក៏ប្រហែលជាខុសគ្នាឆ្ងាយអំពីតួនាទីរបស់វានៅក្នុងភាសាដទៃទៀត។ អ្នកគួរតែចំណាំអំពីរបៀប bind the event handlers។ Without unstable [syntax proposals](https://babeljs.io/docs/en/babel-plugin-transform-class-properties/) the code is very verbose។ យើងអាចយល់អំពី props, state, និង top-down data flow យ៉ាងច្បាស់ប៉ុន្តែនៅមានឧបសគ្គបន្តិចបន្តួចជាមួយ classes។ ភាពខុសគ្នារវាង function ហើយនឹង class components នៅក្នុង React។ ហើយកាលៈទេសៈក្នុងការប្រើវាអាចនិងមិនមានការយល់ស្របរវាង experienced React developers។

ថ្វីបើ React ត្រូវបានដាក់ឲ្យប្រើប្រាស់រយៈពេល ៥ ឆ្នាំមកហើយ ក៏ពួកយើងចង់ឲ្យវា ត្រូវបានគេប្រើប្រាស់ ៥ ឆ្នាំទៅមុខទៀត។ ជាក់ស្តែង [Svelte](https://svelte.technology/), [Angular](https://angular.io/), [Glimmer](https://glimmerjs.com/), ហើយនឹង [ahead-of-time compilation](https://en.wikipedia.org/wiki/Ahead-of-time_compilation) នៃ components មានសក្តានុពលច្រើននាពេលអនាគត។ ជាពិសេសប្រសិនបើវាមិនកំណត់ចំពោះ templates។ ថ្មីៗកន្លងមកនេះ យើងបានពិសោធជាមួយ [component folding](https://github.com/facebook/react/issues/7323) ដែលបានប្រើ [Prepack](https://prepack.io/) ហើយយើងបានឃើញលទ្ធផលដំបូងទទួលបានជោគជ័យ។ However យើងបានរកឃើញ class components អាច encourage unintentional patterns ដែលអាចធ្វើឲ្យ optimizations ត្រឡប់ទៅ slower path។ Classes present issues for today's tools too។ ឧទាហរណ៍ classes មិនបាន minify ល្អឥតខ្ចោះនោះទេ ដែលអាចធ្វើឲ្យ hot reloading flaky ហើយនឹង unreliable។ យើងចង់ណែនាំ API មួយដែលអាចធ្វើឲ្យកូដស្ថិតនៅលើ optimizable path។

ដើម្បីដោះស្រាយបញ្ហាទាំងនេះ **Hooks អនុញ្ញាតឱ្យអ្នកប្រើ features នៅក្នុង React បន្ថែមដោយពុំចាំបាច់ classes។** React components តែងតែជិតដិតជាមួយនិង functions។ Hooks embrace functions but without sacrificing the practical spirit of React។ Hooks អាចចូលទៅប្រើ imperative escape hatches ដោយពុំទាមទារឲ្យអ្នករៀនអំពី complex functional ឬក៏ reactive programming techniques។

>ឧទាហរណ៍
>
>[Hooks មួយភ្លេត](/docs/hooks-overview.html) ជាកន្លែងដ៏ល្អសម្រាប់ការរៀន Hooks។

## យុទ្ធសាស្រ្តអនុម័តបន្តិចបន្តួច {#gradual-adoption-strategy}

>**TLDR: វាគ្មានគម្រោងជាក់លាក់ណាមួយឡើយសម្រាប់ការដក classes ចេញពី React។**

ពួកយើងយល់អំពី React developers ដែលផ្តោតទៅលើ shipping products ហើយមិនសូវជាមានពេលសិក្សាបន្ថែមអំពី new API ដែលចេញមកថ្មីៗ។ Hooks គឺថ្មីស្រឡាងតែម្តង ហើយវាប្រហែលជាល្អដែរ ប្រសិនបើយើងរង់ចាំគំរូឧទាហរណ៍បន្ថែម ក៏ដូចជាគន្លឹះខ្លះៗ មុនពេលដែលយើងចាប់ផ្តើមប្រើវា។

ពួកយើងយល់អំពីការដាក់បញ្ចូល new primitive ទៅលើ React គឺអាចមានហានិភ័យខ្លាំង។ សម្រាប់អ្នកអានដែលចង់ដឹងខ្លាំងអំពីវា យើងបានរៀបចំ [detailed RFC](https://github.com/reactjs/rfcs/pull/68) ដែលស៊ីជម្រៅជាមួយពត៌មានពិស្តារ ហើយនិងផ្តល់នូវទស្សនវិស័យបន្ថែមទៅលើការសំរេចចិត្តនិងភាពទាក់ទិនគ្នា។

<<<<<<< HEAD
**Crucially, Hooks ដំណើរការជាមួយនិងកូដដែលអ្នកធ្លាប់សរសេរ ដូច្នេះអ្នកអាចចាប់ផ្តើមប្រើវាបន្តិចម្តងៗ។** មិនបាច់ប្រញាប់ប្រញាល់ migrate ទៅ Hooks នោះទេ។ មួយទៀតគួរតែជៀសពី "big rewrites" ជាពិសេសសម្រាប់កូដដែលមើលទៅស្មុគស្មាញជាមួយ class components។ វាត្រូវការពេលបន្តិចបន្តួចដើម្បីចាប់ផ្តើមជាមួយនិងផ្នត់គំនិតនេះ "thinking in Hooks"។ សម្រាប់បទពិសោធន៍របស់ពួកយើងផ្ទាល់ វាជាពេលមួយដ៏ល្អសម្រាប់ ការប្រើប្រាស់ Hooks នៅក្នុង components ថ្មីៗក៏ដូចជា components មួយចំនួនដែលមិនសូវសំខាន់ហើយមិនស្មុគស្មាញ ពីព្រោះសមាជិកផ្សេងៗនៅក្នុងក្រុមរបស់អ្នកឆាប់ងាយយល់អំពីវា។ បន្ទាប់ពីអ្នកសាក Hooks រួចហើយ ពេលទំនេរអាច [send us feedback](https://github.com/facebook/react/issues/new) ទោះជាវិជ្ជមានឬអវិជ្ជមានក៏ដោយ។
=======
**Crucially, Hooks work side-by-side with existing code so you can adopt them gradually.** There is no rush to migrate to Hooks. We recommend avoiding any "big rewrites", especially for existing, complex class components. It takes a bit of a mind shift to start "thinking in Hooks". In our experience, it's best to practice using Hooks in new and non-critical components first, and ensure that everybody on your team feels comfortable with them. After you give Hooks a try, please feel free to [send us feedback](https://github.com/facebook/react/issues/new), positive or negative.
>>>>>>> 26a870e1c6e232062b760d37620d85802750e985

យើងមានបំណងចង់ឲ្យ Hooks អាចប្រើប្រាស់បានជាមួយករណីដែលមានស្រាប់ទាំងអស់ជាមួយនឹង classes។ ប៉ុន្តែ **ពួកយើងនៅតែបន្តគាំទ្រ class components សម្រាប់ថ្ងៃអនាគត** នៅ Facebook យើងមានរាប់ពាន់ components ដែលបានសរសេរជាមួយ classes ហើយពួកយើងពិតជាគ្មានគម្រោងថានឹងសរសេរវាឡើងវិញនោះទេ។ ផ្ទុយទៅវិញ យើងចាប់ផ្តើមប្រើ Hooks នៅក្នុងកូដថ្មី side by side ជាមួយនិង classes។

## សំនួរដែលមានគេសួរច្រើន {#frequently-asked-questions}

ពួកយើងក៏បានរៀបចំ [ទំព័រ FAQ របស់ Hooks](/docs/hooks-faq.html) ដែលបានឆ្លើយនូវសំនួរល្អៗដែលមានគេសួរច្រើនអំពី Hooks។

## ទំព័របន្ទាប់ {#next-steps}

មកដល់ត្រង់នេះ ពួកយើងច្បាស់ថា អ្នកប្រាកដជាមានគំនិតខ្លះៗទៅលើ Hooks ហើយនិងតិចនិកមួយចំនួនដែលអាចដោះស្រាយបញ្ហាជាមួយវាបាន ប៉ុន្តែសម្រាប់ខ្លឹមសារអត្ថបទមួយចំនួនដែលអ្នកអានខាងលើពីរបីដងហើយ នៅតែមិនសូវច្បាស់។ មិនជាថ្វីទេ! **ចុចត្រង់នេះដើម្បីទៅ [ទំព័របន្ទាប់](/docs/hooks-overview.html) ដែលជាកន្លែងដ៏សម្បូរបែបក្នុងការរៀនអំពី Hooks ជាមួយនិងគំរូឧទាហរណ៍ងាយៗ។**
