---
id: rendering-elements
title: ការបង្ហាញធាតុ
permalink: docs/rendering-elements.html
redirect_from:
  - "docs/displaying-data.html"
prev: introducing-jsx.html
next: components-and-props.html
---

ធាតុផ្សំគឺជាប្លុកដែលតូចជាងគេបំផុតនៃកម្មវិធីReact។

ធាតុ(element)ពិពណ៌នាអំពីអ្វីដែលអ្នកចង់ឃើញនៅលើអេក្រង់:

```js
const element = <h1>Hello, world</h1>;
```

មិនដូចធាតុbrowser DOM, ធាតុ Reactគឺជាវត្ថុធម្មតាហើយងាយស្រួលក្នុងការដើម្បីបង្កើត។ React DOM យកចិត្តទុកដាក់ធ្វើឱ្យទាន់សម័យ DOM ដើម្បីផ្គូផ្គងធាតុ React ។

>**Note:**
>
>យើងអាចច្រឡំធាតុជាមួយនឹងគំនិតដែលគេស្គាល់កាន់តែច្រើនអំពី "components"។ យើងនឹងណែនាំ components នៅក្នុង [ផ្នែកបន្ទាប់](/docs/components-and-props.html). ធាតុគឺជាអ្វីដែលcomponentsត្រូវបាន "ធ្វើពី", ហើយយើងលើកជំរុញឱ្យអ្នកអានផ្នែកនេះមុនពេលលោតទៅផ្នែកបន្ទាប់។

## ការបង្ហាញធាតុទៅក្នុង DOM {#rendering-an-element-into-the-dom}

តោះនិយាយថាមាន `<div>` កន្លែងណាមួយនៅក្នុងឯកសារ HTML របស់អ្នក:

```html
<div id="root"></div>
```

យើងហៅវាថាជា "root" DOM node ពីព្រោះអ្វីគ្រប់យ៉ាងដែលនៅក្នុងវានឹងត្រូវបានគ្រប់គ្រងដោយ React DOM។

កម្មវិធីដែលបានបង្កើតឡើងដោយគ្រាន់តែមានReactធម្មតាមាន root DOM តែមួយ។ ប្រសិនបើអ្នកកំពុងដាក់បញ្ចូល React ទៅក្នុងកម្មវិធីដែលមានស្រាប់ អ្នកប្រហែលជាអាចមាន root DOM ជាច្រើនទៅតាមចំណងចង់បានរបស់អ្នក។

ដើម្បីបង្ហាញធាតុReactទៅក្នុង root DOM សូមធ្វើការផ្តល់ទៅឱ្យ `ReactDOM.render()`:

`embed:rendering-elements/render-an-element.js`

[សាកល្បងវានៅលើ CodePen](codepen://rendering-elements/render-an-element)

វាបង្ហាញ "ជំរាបសួរពិភពលោក" នៅលើទំព័រនេះ។

## ធ្វើបច្ចុប្បន្នភាពធាតុបង្ហាញ {#updating-the-rendered-element}

ធាតុReact[គឺមិនប្រែប្រួល(immutable)](https://en.wikipedia.org/wiki/Immutable_object)។ នៅពេលអ្នកបង្កើតធាតុមួយអ្នកមិនអាចផ្លាស់ប្តូរ children ឬគុណលក្ខណៈរបស់វាបានទេ។ ធាតុមួយគឺដូចជាស៊ុមតែមួយនៅក្នុងខ្សែភាពយន្ត: វាតំណាងឱ្យចំណុចប្រទាក់អ្នកប្រើនៅចំណុចជាក់លាក់មួយនៅក្នុងពេលណាមួយ។

ជាមួយនឹងចំណេះដឹងរបស់យើង, វិធីតែមួយគត់ដើម្បីធ្វើឱ្យ UI ទាន់សម័យគឺបង្កើតធាតុថ្មីt, ហើយបញ្ជូនវាទៅ `ReactDOM.render()`.

សូមពិចារណាអំពីគំរូម៉ោងនាឡិកានេះ:

`embed:rendering-elements/update-rendered-element.js`

[សាកល្បងវានៅលើ CodePen](codepen://rendering-elements/update-rendered-element)

វាហៅ `ReactDOM.render()` រាល់វិនាទី [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) ត្រូវបានហៅឲត្រលប់វិញ.

>**ចំណាំ:**
>
>នៅក្នុងការអនុវត្ត, React ភាគច្រើនហៅតែ `ReactDOM.render()` តែម្ដងប៉ុណ្ណោះ។ នៅផ្នែកបន្ទាប់ យើងនឹងរៀនពីរបៀបដែលកូដបែបនេះត្រូវបានបញ្ចូលក្នុង [stateful components](/docs/state-and-lifecycle.html).
>
>យើងផ្ដល់អនុសាសន៍ថាអ្នកមិនរំលងប្រធានបទពីព្រោះពួកគេមានការទាក់ទងគ្នា។

## Reactធ្វើបច្ចុប្បន្នភាពអ្វីដែលចាំបាច់ប៉ុណ្ណោះ {#react-only-updates-whats-necessary}

React DOM React DOM ប្រៀបធៀបធាតុនិងchildrenរបស់វាទៅនឹងធាតុមួយមុន, ហើយអនុវត្តតែការធ្វើឱ្យទាន់សម័យ DOM ដែលចាំបាច់ដើម្បីនាំយក DOM ទៅជា state ដែលចង់បាន។

អ្នកអាចផ្ទៀងផ្ទាត់បានដោយត្រួតពិនិត្យមើល [ឧទាហរណ៍ចុងក្រោយ](codepen://rendering-elements/update-rendered-element)ជាមួយនឹងឧបករណ៍របស់browser:

![DOM inspector បានបង្ហាញពីភាពទាន់សម័យ](../images/docs/granular-dom-updates.gif)

<<<<<<< HEAD
ទោះបីជាយើងបង្កើតធាតុពិពណ៌នាអំពីមែកធាង UI ទាំងមូលនៅលើគ្រប់ធី, មានតែ text node ដែលមាតិការបស់វាត្រូវបានផ្លាស់ប្តូរត្រូវបានធ្វើបច្ចុប្បន្នភាពដោយ React DOM ។
=======
Even though we create an element describing the whole UI tree on every tick, only the text node whose contents have changed gets updated by React DOM.
>>>>>>> 821e20726266bc8113353d0c2b6d885f82e584a8

តាមបទពិសោធរបស់យើង, ការគិតអំពីវិធីដែលចំណុចប្រទាក់អ្នកប្រើគួរមើលទៅនៅពេលណាមួយដែលបានផ្តល់ឱ្យជាជាងការផ្លាស់ប្តូរវាតាមពេលវេលាលុបបំបាត់កំហុសទាំងមូល។
