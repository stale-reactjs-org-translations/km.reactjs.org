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

តោះនិយាយថាមាន `<div>` កន្លែងណាមួយនៅក្នុងឯកសារ HTML របស់អ្នក៖

```html
<div id="root"></div>
```

យើងហៅវាថាជា "root" DOM node ពីព្រោះអ្វីគ្រប់យ៉ាងដែលនៅក្នុងវានឹងត្រូវបានគ្រប់គ្រងដោយ React DOM។

កម្មវិធីដែលបានបង្កើតឡើងដោយគ្រាន់តែមានReactធម្មតាមាន root DOM តែមួយ។ ប្រសិនបើអ្នកកំពុងដាក់បញ្ចូល React ទៅក្នុងកម្មវិធីដែលមានស្រាប់ អ្នកប្រហែលជាអាចមាន root DOM ជាច្រើនទៅតាមចំណងចង់បានរបស់អ្នក។

ដើម្បីបង្ហាញ React element ទៅក្នុង root DOM node, បេាះ (pass) វាទាំងពីរទៅឱ្យ [`ReactDOM.render()`](/docs/react-dom.html#render)៖

`embed:rendering-elements/render-an-element.js`

<<<<<<< HEAD
[សាកល្បងវានៅលើ CodePen](codepen://rendering-elements/render-an-element)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/ZpvBNJ?editors=1010)**
>>>>>>> 71cc6be6182418dec43b72f2a9ef464619cb7025

វាបង្ហាញ "ជំរាបសួរពិភពលោក" នៅលើទំព័រនេះ។

## ធ្វើបច្ចុប្បន្នភាពធាតុបង្ហាញ {#updating-the-rendered-element}

ធាតុReact[គឺមិនប្រែប្រួល(immutable)](https://en.wikipedia.org/wiki/Immutable_object)។ នៅពេលអ្នកបង្កើតធាតុមួយអ្នកមិនអាចផ្លាស់ប្តូរ children ឬគុណលក្ខណៈរបស់វាបានទេ។ ធាតុមួយគឺដូចជាស៊ុមតែមួយនៅក្នុងខ្សែភាពយន្ត: វាតំណាងឱ្យចំណុចប្រទាក់អ្នកប្រើនៅចំណុចជាក់លាក់មួយនៅក្នុងពេលណាមួយ។

ជាមួយនឹងចំណេះដឹងរបស់យើងរហូតមកដល់ពេលនេះ, វិធីតែមួយគត់ដើម្បីធ្វើបច្ចុប្បន្នភាព UI គឺបង្កើត element ថ្មី, ហើយបញ្ជូន (pass) វាទៅ [`ReactDOM.render()`](/docs/react-dom.html#render)។

សូមពិចារណាអំពីគំរូម៉ោងនាឡិកានេះ:

`embed:rendering-elements/update-rendered-element.js`

<<<<<<< HEAD
[សាកល្បងវានៅលើ CodePen](codepen://rendering-elements/update-rendered-element)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/gwoJZk?editors=1010)**
>>>>>>> 71cc6be6182418dec43b72f2a9ef464619cb7025

វាហៅ [`ReactDOM.render()`](/docs/react-dom.html#render) រាល់វិនាទី ពី [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) callback។

>**ចំណាំ:**
>
>នៅក្នុងការអនុវត្ត, React apps ភាគច្រើនហៅតែ [`ReactDOM.render()`](/docs/react-dom.html#render) តែម្ដងប៉ុណ្ណោះ។ នៅផ្នែកបន្ទាប់ យើងនឹងរៀនពីរបៀបដែលកូដបែបនេះត្រូវបានបញ្ចូលក្នុង [stateful components](/docs/state-and-lifecycle.html).
>
>យើងផ្ដល់អនុសាសន៍ថាអ្នកមិនរំលងប្រធានបទពីព្រោះពួកគេមានការទាក់ទងគ្នា។

## Reactធ្វើបច្ចុប្បន្នភាពអ្វីដែលចាំបាច់ប៉ុណ្ណោះ {#react-only-updates-whats-necessary}

React DOM React DOM ប្រៀបធៀបធាតុនិងchildrenរបស់វាទៅនឹងធាតុមួយមុន, ហើយអនុវត្តតែការធ្វើឱ្យទាន់សម័យ DOM ដែលចាំបាច់ដើម្បីនាំយក DOM ទៅជា state ដែលចង់បាន។

<<<<<<< HEAD
អ្នកអាចផ្ទៀងផ្ទាត់បានដោយត្រួតពិនិត្យមើល [ឧទាហរណ៍ចុងក្រោយ](codepen://rendering-elements/update-rendered-element)ជាមួយនឹងឧបករណ៍របស់browser:
=======
You can verify by inspecting the [last example](https://codepen.io/gaearon/pen/gwoJZk?editors=1010) with the browser tools:
>>>>>>> 71cc6be6182418dec43b72f2a9ef464619cb7025

![DOM inspector បានបង្ហាញពីភាពទាន់សម័យ](../images/docs/granular-dom-updates.gif)

ទោះបីជាយើងបង្កើត element ពិពណ៌នាអំពីមែកធាង UI ទាំងមូលនៅលើគ្រប់ tick, មានតែ text node ដែលមាតិការបស់វាត្រូវបានផ្លាស់ប្តូរត្រូវបានធ្វើបច្ចុប្បន្នភាពដោយ React DOM ។

តាមបទពិសោធរបស់យើង, ការគិតពីររបៀបដែល UI គួរបង្ហាញនៅពេលណាមួយ, ជាជាងពីរបៀបដែលផ្លាស់ប្តូវវារាល់ពេល, លុបបំបាត់ bugs នៅក្នុង class ទាំងមូល។
