---
id: introducing-jsx
title: ការណែនាំស្តីអំពី JSX
permalink: docs/introducing-jsx.html
prev: hello-world.html
next: rendering-elements.html
---

ពិចារណាអំពីការប្រកាសអថេរ(variable):

```js
const element = <h1>Hello, world!</h1>;
```

វាដូចជាកំប្លែងដែលវាក្យសម្ពន្ធ(Syntax)មិនមែនជា String ឬ HTML។

វាត្រូវបានគេហៅថា JSX ហើយវាជាការបន្ថែមវាក្យសម្ព័ន្ធ(Syntax)ទៅក្នុង JavaScript ។ យើងសូមផ្តល់អនុសាសន៍ប្រើវាជាមួយ React ដើម្បីពណ៌នាអំពីអ្វីដែល UI គួរតែមាន។ JSX អាចរំលឹកអ្នកពីភាសាគំរូមួយប៉ុន្តែវាមកជាមួយភាពថាមពលពេញនៃ JavaScript ។

ប្រើ JSX ដើម្បីបង្កើតធាតុ React. យើងនឹងធ្វើការបង្ហាញពួកវាទៅ DOM នៅក្នុង [ផ្នែកបន្ទាប់](/docs/rendering-elements.html)។  ផ្នែកខាងក្រោមនេះអ្នកអាចរកឃើញមូលដ្ឋានគ្រឹះនៃ JSX ដែលចាំបាច់ដើម្បីអាចឱ្យអ្នកចាប់ផ្តើម។
### ហេតុអ្វី JSX? {#why-jsx}

React បានបញ្ចូលនូវផ្នែកគណនានៃការបង្ហាញត្រូវបានផ្សំជាមួយនឹងតក្កវិជ្ជា UI ផ្សេងទៀត: របៀបដែលព្រឹត្តិការណ៍ត្រូវបានដោះស្រាយ របៀបដែល State ផ្លាស់ប្តូរតាមពេលវេលា និង របៀបដែលទិន្នន័យត្រូវបានរៀបចំសម្រាប់ការបង្ហាញ។

ជំនួសឱ្យការបំបែកសិប្បនិម្មិត *បច្ចេកវិទ្យា* ដោយដាក់ការសម្គាល់និងតក្កឬការគណនានៅក្នុងឯកសារដាច់ដោយឡែក, React [បំបែក *ការព្រួយបារម្ភ*](https://en.wikipedia.org/wiki/Separation_of_concerns) ជាមួយនឹងឯកតាគូរលុងដែលហៅថា "components" ដែលមានទាំងពីរ. យើងនឹងត្រលប់ទៅ components វិញ[ផ្នែកបន្ថែមទៀត](/docs/components-and-props.html) ប៉ុន្តែប្រសិនបើអ្នកមិនទាន់មានយល់ច្បាស់អំពីការដាក់ការសម្គាល់នៅក្នុង JS [ការពិភាក្សានេះ](https://www.youtube.com/watch?v=x7cQ3mrcKaY) ដែលអាចធ្វើអោយអ្នកឆាប់យល់បានកាន់តែច្បាស់។

React [មិនត្រូវការ](/docs/react-without-jsx.html) ប្រើប្រាស់ JSX, ប៉ុន្តែមនុស្សភាគច្រើនយល់ឃើញថាវាមានប្រយោជន៍ជាជំនួយនៅពេលធ្វើការជាមួយ UI នៅក្នុងកូដ JavaScript។ វាក៏អនុញ្ញាតឱ្យ React ដើម្បីបង្ហាញពីកំហុសនិងសារព្រមានដែលមានប្រយោជន៍ជាងមុន។

ជាមួយនឹងការណែនាំខាងលើនោះ ចូរយើងចាប់ផ្ដើម!

### ការបង្កប់កន្សោមនៅក្នុង JSX {#embedding-expressions-in-jsx}

នៅក្នុងឧទាហរណ៍ខាងក្រោម យើងប្រកាសអថេរ(variable)ហៅថា `name` ហើយបន្ទាប់មកប្រើវានៅខាងក្នុង JSX ដោយរុំវាក្នុងដង្កៀបអង្កាញ់(curly braces):

```js{1,2}
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

អ្នកអាចដាក់ [កន្សោម JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) ដែលត្រឺមត្រូវទាំងអស់ នៅខាងក្នុងដង្កៀបអង្កាញ់(curly braces) JSX. ឧទាហរណ៍, `2 + 2`, `user.firstName`, or `formatName(user)` ជាកន្សោម JavaScript ត្រឹមត្រូវទាំងអស់។

នៅក្នុងឧទាហរណ៍ខាងក្រោមយើងបានបង្កប់នូវលទ្ធផលនៃការហៅមុខងារ JavaScript `formatName(user)`, ចូលទៅក្នុង `<h1>` ធាតុ.

```js{12}
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[សាកល្បងនៅលើ Codepen](codepen://introducing-jsx)

យើងធ្វើការបំបែក JSX នៅលើបន្ទាត់ជាច្រើនដើម្បីឲមានភាពងាយស្រួលសម្រាប់ការអាន។ ខណៈពេលដែលវាមិនត្រូវបានទាមទារ នៅពេលធ្វើដូចនេះ យើងក៏សូមផ្តល់អនុសាសន៍រុំវានៅក្នុងវង់ក្រចកដើម្បីជៀសវាងពីចំនុចគ្រោះថ្នាក់នៃ [បញ្ចូល semicolon ស្វ័យប្រវត្តិ](https://stackoverflow.com/q/2846283).

### JSX ក៏ជាកន្សោមផងដែរ {#jsx-is-an-expression-too}

បន្ទាប់ពីការចងក្រងកន្សោម JSX ក្លាយជាការហៅមុខងារ JavaScript ធម្មតានិងវាយតម្លៃទៅជាវត្ថុ JavaScript ។

នេះគឺមានន័យថា អ្នកអាចប្រើប្រាស់ JSX នៅខាងក្នុង ប្រយោគ `if`  និង `for` loops ការប្រកាសអថេរ ការទទួលនូវតម្លៃ និងការទទួលពីមុខងារណាមួយ

```js{3,5}
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### ការបញ្ជាក់លក្ខណៈជាមួយ JSX {#specifying-attributes-with-jsx}

You may use quotes to specify string literals as attributes:

```js
const element = <div tabIndex="0"></div>;
```

You may also use curly braces to embed a JavaScript expression in an attribute:

```js
const element = <img src={user.avatarUrl}></img>;
```

Don't put quotes around curly braces when embedding a JavaScript expression in an attribute. You should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute.

>**Warning:**
>
>Since JSX is closer to JavaScript than to HTML, React DOM uses `camelCase` property naming convention instead of HTML attribute names.
>
>For example, `class` becomes [`className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className) in JSX, and `tabindex` becomes [`tabIndex`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/tabIndex).

### ការបញ្ជាក់ Children ជាមួយ JSX {#specifying-children-with-jsx}

ប្រសិនបើស្លាក (Tag) ទទេ អ្នកអាចបិទវាភ្លាមៗជាមួយ `/>` ដូចជា XML:

```js
const element = <img src={user.avatarUrl} />;
```

ស្លាក JSX អាចមាន children:

```js
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### JSX បង្ការការវាយប្រហារ {#jsx-prevents-injection-attacks}

វាគឺមានសុវត្ថិភាពក្នុងការបង្កប់នូវទិន្ន័យរបស់អ្នកប្រើប្រាស់ដែលបានបញ្ចូលទៅក្នុង JSX:

```js
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```

By default, React DOM [escapes](https://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-on-html) any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that's not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent [XSS (cross-site-scripting)](https://en.wikipedia.org/wiki/Cross-site_scripting) attacks.

### JSX វត្ថុតំណាង {#jsx-represents-objects}

Babel  ធ្វើការបំលែង JSX នៅពេល `React.createElement()` ត្រូវបានហៅ។

ឧទាហរណ៍ទាំងពីរនេះគឺដូចគ្នា:

```js
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```js
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

`React.createElement()` ធ្វើការត្រួតពិនិត្យមួយចំនួនដើម្បីជួយអ្នកសរសេរកូដដោយមិនចាំបាច់មានកំហុសប៉ុន្តែសំខាន់វាបង្កើតវត្ថុដូចនេះ:

```js
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

These objects are called "React elements". You can think of them as descriptions of what you want to see on the screen. React reads these objects and uses them to construct the DOM and keep it up to date.

យើងនឹងធ្វើការស្វែងយល់ពីធាតុផ្សំ React ក្នុងការឆ្លើយតបទៅ DOM នៅក្នុងផ្នែកបន្ទាប់។

>**Tip:**
>
>We recommend using the ["Babel" language definition](https://babeljs.io/docs/editors) for your editor of choice so that both ES6 and JSX code is properly highlighted. This website uses the [Oceanic Next](https://labs.voronianski.com/oceanic-next-color-scheme/) color scheme which is compatible with it.
