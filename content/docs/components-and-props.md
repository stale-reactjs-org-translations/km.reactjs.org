---
id: components-and-props
title: Components និង Props
permalink: docs/components-and-props.html
redirect_from:
  - "docs/reusable-components.html"
  - "docs/reusable-components-zh-CN.html"
  - "docs/transferring-props.html"
  - "docs/transferring-props-it-IT.html"
  - "docs/transferring-props-ja-JP.html"
  - "docs/transferring-props-ko-KR.html"
  - "docs/transferring-props-zh-CN.html"
  - "tips/props-in-getInitialState-as-anti-pattern.html"
  - "tips/communicate-between-components.html"
prev: rendering-elements.html
next: state-and-lifecycle.html
---

Componentsអនុញ្ញាតឱ្យអ្នកបំបែក UI ទៅជាបំណែកឯករាជ្យ ដែលអាចប្រើឡើងវិញបាន ហើយគិតអំពីបំណែកនីមួយៗនៅក្នុងភាពឯកោ(isolation)។ ទំព័រនេះផ្តល់ការណែនាំអំពីគំនិតនៃcomponents. អ្នកអាចរក [លំអិត component API លំអិតនៅទីនេះ](/docs/react-component.html).

គំនិត, components គឺដូចមុខងារ JavaScript. ពួកគេទទួលយកធាតុចូល (ហៅថា "props") ហើយត្រឡប់ធាតុ React ពិពណ៌នាអំពីអ្វីដែលគួរលេចឡើងនៅលើអេក្រង់។

## Function និង Class Components {#function-and-class-components}

វិធីសាមញ្ញបំផុតដើម្បីកំណត់ component គឺត្រូវសរសេរមុខងារ JavaScript:

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

មុខងារនេះគឺជា React component ត្រឹមត្រូវ ដោយសារតែវាទទួលយក "props" តែមួយ(ដែលតំណាងឱ្យអចលនទ្រព្យ) objectជាមួយទិន្នន័យនិងត្រឡប់ធាតុReact ។ យើងហៅcomponentsដូចជា "function components" ដោយសារតែពួកគេគឺជាមុខងារព្យញ្ជនៈ JavaScript ។
អ្នកក៏អាចប្រើ[ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) ដើម្បីកំណត់component:

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

components ពីរខាងលើនេះគឺសមមូលនឹងទស្សនៈរបស់ React ។

Function និង Classes មានលក្ខណៈពិសេសបន្ថែមមួយចំនួនដែលយើងនឹងពិភាក្សានៅក្នុង[ផ្នែកបន្ទាប់](/docs/state-and-lifecycle.html).

## ការបង្កើតComponent {#rendering-a-component}

កាលពីមុនយើងទើបតែជួបReactធាតុដែលតំណាងឱ្យស្លាក(tags) DOM:

```js
const element = <div />;
```

ទោះយ៉ាងណាធាតុក៏អាចតំណាងឱ្យcomponentsដែលកំណត់ដោយអ្នកប្រើ:

```js
const element = <Welcome name="Sara" />;
```

នៅពេលដែល React មើលឃើញ element ដែលតំណាងឱ្យ component ដែលកំណត់ដោយអ្នកប្រើប្រាស់, វាបញ្ជូន (passes) JSX attributes និង children ទៅអោយ component នេះជា single object។ យើងហៅ object នេះថា "props"។

ឧទាហរណ៏, កូដនេះធ្វើការមំលែងទៅជា "Hello, Sara" នៅលើទំព័រ:

```js{1,5}
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(element);
```

<<<<<<< HEAD
[សាកល្បងនៅលើ CodePen](codepen://components-and-props/rendering-a-component)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/YGYmEG?editors=1010)**
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

ចូរយើងសង្ខេបនូវអ្វីដែលកើតឡើងនៅក្នុងឧទាហរណ៍នេះ:

<<<<<<< HEAD
1. យើង​ហៅ `ReactDOM.render()` ជាមួយនឹង `<Welcome name="Sara" />` ធាតុ។
2. React ហៅ `Welcome` component ជាមួយ `{name: 'Sara'}` ជា props។
3. `Welcome` component របស់យើង ត្រឡប់ជាមួយ `<h1>Hello, Sara</h1>` ជាលទ្ធផល។
4. React DOM ធ្វើឱ្យទាន់សម័យមានប្រសិទ្ធិភាព DOM ដើម្បីផ្គូផ្គង `<h1>Hello, Sara</h1>`.
=======
1. We call `root.render()` with the `<Welcome name="Sara" />` element.
2. React calls the `Welcome` component with `{name: 'Sara'}` as the props.
3. Our `Welcome` component returns a `<h1>Hello, Sara</h1>` element as the result.
4. React DOM efficiently updates the DOM to match `<h1>Hello, Sara</h1>`.
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

>**ចំណាំ:** តែងតែចាប់ផ្ដើមឈ្មោះ component ជាមួយអក្សរធំ។
>
>Reactទាក់ទងនឹងcomponentsដែលចាប់ផ្ដើមដោយអក្សរតូចជាស្លាក DOM។ ឧទាហរណ៍ `<div />` តំណាងឱ្យស្លាក HTML div ប៉ុន្តែ `<Welcome />` តំណាងឱ្យcomponentនិងតម្រូវ `Welcome` នៅក្នុង scope។
>
>ដើម្បីរៀនថែមទៀតអំពីហេតុផលដែលនៅពីក្រោយអនុសញ្ញានេះ, សូម​អាន [JSX In Depth](/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized).

## Composing Components {#composing-components}

ComponentsអាចសំដៅទៅលើComponentsផ្សេងៗនៅក្នុងលទ្ធផលរបស់វា។ នេះអនុញ្ញាតឱ្យយើងប្រើ component abstraction ដូចគ្នាសម្រាប់កម្រិតលម្អិត។ ប៊ូតុង សំណុំបែបបទ dialog អេក្រង់: ក្នុងកម្មវិធីReactទាំងអស់ ដែលត្រូវបានគេបញ្ជាក់ជាទូទៅថាជាcomponents។

ឧទាហរណ៍, យើងអាចបង្កើត `App` component ដែលបង្ហាញ `Welcome`ជា​ច្រើន​ដង:

```js{8-10}
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
```

<<<<<<< HEAD
[សាកល្បងនៅលើ CodePen](codepen://components-and-props/composing-components)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/KgQKPr?editors=1010)**
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

ជាធម្មតា, កម្មវិធី React ថ្មីមាន `App` component តែមួយនៅកំពូលបំផុត. ទោះយ៉ាងណា, ប្រសិនបើអ្នកធ្វើសមាហរណកម្មបញ្ចូលគ្នាទៅក្នុងកម្មវិធីដែលមានស្រាប់ អ្នកអាចចាប់ផ្តើមពីតូចឡើងដោយមាន component តូចមួយដូចជា `Button` ហើយជាបណ្តើរដំណើរ វិធីរបស់អ្នកទៅកំពូលនៃឋានានុក្រមទិដ្ឋភាព។

## Extracting Components {#extracting-components}

កុំខ្លាចការចែក components ជា components តូចៗ។

ឧទាហរណ៍, ពិចារណា `Comment` component នេះ:

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

<<<<<<< HEAD
[សាកល្បងនៅលើ CodePen](codepen://components-and-props/extracting-components)
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/VKQwEo?editors=1010)**
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

វាទទួលយក author (ជាវត្ថុ) text (ជាអក្សរ) និង date (ជាកាលបរិច្ឆេទ) ជាprops ហើយពិពណ៌នាអំពីមតិយោបល់នៅលើគេហទំព័រប្រព័ន្ធផ្សព្វផ្សាយសង្គមមួយ។

componentនេះអាចត្រូវបានផ្លាស់ប្តូរដោយសារតែnestingទាំងអស់, ហើយវាក៏លំបាកផងដែរក្នុងការប្រើឡើងវិញនូវផ្នែកមួយៗរបស់វា។ ចូរដកស្រង់componentsមួយចំនួនពីវា។

ដំបូងយើងនឹងស្រង់ `Avatar`:

```js{3-6}
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

Avatar មិនចាំបាច់ដឹងថាវាកំពុងត្រូវបានបង្ហាញនៅ`Comment` នេះហើយជាមូលហេតុដែលយើងបានផ្តល់ឈ្មោះថ្មីរបស់ខ្លួនបន្ថែមទៀត `user` ជាជាង `author`.

យើងសូមផ្តល់យោបល់ដល់អ្នកប្រើឈ្មោះ props ពីចំណុចផ្ទាល់របស់ component ជាជាងបរិបទដែលវាកំពុងប្រើ។

ឥឡូវនេះយើងអាចមានភាពងាយស្រួលជាងមុនបន្តិច `Comment`:

```js{5}
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

បន្ទាប់, យើងនឹងស្រង់ចេញនូវcomponent `UserInfo` ដែលបង្ហាញ `Avatar` នៅជាប់នឹងឈ្មោះអ្នកប្រើ:

```js{3-8}
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

នេះអនុញ្ញាតឱ្យយើងធ្វើឱ្ យ`Comment` ងាយៗបន្ថែម:

```js{4}
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

<<<<<<< HEAD
[សាកល្បងនៅលើ CodePen](codepen://components-and-props/extracting-components-continued)

ការទាញយក components អាចមើលទៅដូចជាការងារដ៏ធុញទ្រាន់នៅពេលដំបូង ប៉ុន្តែវាមានភាពទូលំទូលាយនៃការប្រើ components ឡើងវិញ នៅក្នុងកម្មវិធីធំៗ។ ច្បាប់ល្អគឺថា ប្រសិនបើផ្នែកនៃ UI របស់អ្នកត្រូវបានប្រើច្រើនដង (`Button`, `Panel`, `Avatar`) ឬស្មុគ្រស្មាញគ្រប់គ្រាន់ដោយ Component ខ្លួនឯង(`App`, `FeedStory`, `Comment`) វាជាបេក្ខជនដ៏ល្អដើម្បីក្លាយជាcomponentប្រើម្តងទៀត។
=======
**[Try it on CodePen](https://codepen.io/gaearon/pen/rrJNJY?editors=1010)**

Extracting components might seem like grunt work at first, but having a palette of reusable components pays off in larger apps. A good rule of thumb is that if a part of your UI is used several times (`Button`, `Panel`, `Avatar`), or is complex enough on its own (`App`, `FeedStory`, `Comment`), it is a good candidate to be extracted to a separate component.
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

## Props គឺមិនអាចកែសម្រួល {#props-are-read-only}

ថាតើអ្នកប្រកាស component ជា [មុខងារ ឬ class](#function-and-class-components), វាមិនត្រូវផ្លាស់ប្តូរpropsរបស់វាទេ។ ពិចារណាលើមុខងារ `sum` នេះ:

```js
function sum(a, b) {
  return a + b;
}
```

មុខងារបែបនេះត្រូវបានហៅ ["pure"](https://en.wikipedia.org/wiki/Pure_function) ដោយសារតែពួកគេមិនបានព្យាយាមផ្លាស់ប្តូរធាតុចូលរបស់ពួកគេ, ហើយតែងតែត្រឡប់លទ្ធផលដដែលៗសម្រាប់ធាតុបញ្ចូលដូចគ្នា។

ផ្ទុយ​មកវិញ មុខងារនេះគឺមិនប្រឡាក់ទេព្រោះវាផ្លាស់ប្តូរការបញ្ចូលរបស់វាផ្ទាល់:

```js
function withdraw(account, amount) {
  account.total -= amount;
}
```

Reactមានភាពបត់បែនណាស់ប៉ុន្តែវាក៏មានច្បាប់តឹងតែងមួយដែរ:

**React components ទាំងអស់ត្រូវតែដើរតួរឆ្លើយតបដូចជាមុខងារ pure ដែលទាក់ទងទៅនឹង props របស់ពួកគេ។**

ជាការពិតកម្មវិធី UI របស់កម្មវិធីគឺមានថាមភាពនិងផ្លាស់ប្តូរតាមពេលវេលា។ ក្នុង [ផ្នែកបន្ទាប់](/docs/state-and-lifecycle.html), យើងនឹងណែនាំគំនិតថ្មីនៃ "state"។ State អនុញ្ញាតឱ្យ components ធ្វើសកម្មភាពផ្លាស់ប្តូរលទ្ធផលរបស់ខ្លួនក្នុងពេលឆ្លើយតបទៅនឹងសកម្មភាពរបស់អ្នកប្រើ ការឆ្លើយតបបណ្តាញ និងអ្វីផ្សេងទៀតដោយគ្មានការរំលោភលើច្បាប់នេះ។
