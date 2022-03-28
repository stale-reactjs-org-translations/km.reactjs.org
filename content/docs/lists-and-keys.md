---
id: lists-and-keys
title: Lists and Keys
permalink: docs/lists-and-keys.html
prev: conditional-rendering.html
next: forms.html
---

ដំបូងសូមពិនិត្យឡើងវិញពីរបៀបដែលអ្នកផ្លាស់ប្តូរ (transform) lists នៅក្នុង JavaScript។​

កូដត្រូវបានផ្តល់អោយដូចខាងក្រោម, យើងប្រើ [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) function ដើម្បីទទួលបាន array នៃ `numbers` មួយហើយទ្វេដងតំលៃរបស់ពួកវា។ យើង assign array ថ្មីដែលបាន​​ return ដោយ `map()` ទៅអោយ variable `doubled` ហើយនិងធ្វើការ log វា៖

```javascript{2}
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

កូដនេះ logs `[2, 4, 6, 8, 10]` ទៅកាន់ console។

នៅក្នុង React, ការផ្លាស់ប្តូរ (transforming) arrays ចូលទៅក្នុង lists នៃ [elements](/docs/rendering-elements.html) គឺស្ទើរតែដូចគ្នាបេះបិទ។

### Rendering Multiple Components {#rendering-multiple-components}

អ្នកអាចបង្កើត collections នៃ elements និង [បញ្ចូលពួកវាទៅក្នុង JSX](/docs/introducing-jsx.html#embedding-expressions-in-jsx) ដោយការប្រើដង្កៀប​អង្កាញ់ (curly braces) `{}`។

កូដខាងក្រោមនេះ យើងធ្វើការ loop `numbers` array ដោយការប្រើ JavaScript [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) function។ យើង return `<li>` element មួយសម្រាប់ item នីមួយៗ។ ទីបំផុត, យើង assign លទ្ធផល array នៃ elements ទៅអោយ `listItems`៖

```javascript{2-4}
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

យើងរួមបញ្ចូល `listItems` array ទាំងមូលដែលនៅខាងក្នុង `<ul>` element មួយ ហើយនិង [render វាទៅកាន់ DOM](/docs/rendering-elements.html#rendering-an-element-into-the-dom)៖

```javascript{2}
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/GjPyQr?editors=0011)

កូដនេះបង្ហាញ (displays) bullet list មួយនៃតួលេខចន្លេាះពី១និង៥។

### Basic List Component {#basic-list-component}

ជាធម្មតាអ្នកនឹង render lists នៅខាងក្នុង [component](/docs/components-and-props.html) មួយ។

យើងអាច refactor ឧទាហរណ៍មុនទៅក្នុង component មួយដែលទទួលយក array នៃ `numbers` ហើយនិង បង្ហាញលទ្ធផល (outputs) list នៃ elements មួយ។

```javascript{3-5,7,13}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

នៅពេលដែលអ្នក run កូដនេះ អ្នកនឹងទទួលបានការព្រមាន (warning) មួយថា​ key គួរត្រូវបានផ្តល់ជូនសម្រាប់ list items។ "key" គឺជា string attribute ពិសេសមួយដែលអ្នកត្រូវតែរួមបញ្ចូលនៅពេលកំពុងបង្កើត lists នៃ elements។ យើងនឹងពិភាក្សាគ្នាពីមូលហេតុដែលវាសំខាន់នៅក្នុងផ្នែកបន្ទាប់។

តេាះ assign `key` មួយទៅអោយ list items របស់យើងដែលនៅខាងក្នុង `numbers.map()` ហើយនិងដេាះស្រាយបញ្ហាដែលបាត់ key។

```javascript{4}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/jrXYRR?editors=0011)

## Keys {#keys}

Keys ជួយ React កំណត់អត្តសញ្ញាណថាតើ items មួយណាដែលបានផ្លាស់ប្តូរ, បានបន្ថែម, ឬក៏បានលុបចេញ។ Keys គួរតែត្រូវបានផ្តល់ទៅឱ្យ elements នៅខាងក្នុង array ដើម្បីផ្តល់ឱ្យ elements នូវអត្តសញ្ញាណដែលមានស្ថិរភាពមួយ៖

```js{3}
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

វិធីល្អបំផុតដើម្បីជ្រើសរើស key គឺប្រើ string កំណត់អត្តសញ្ញាណតែមួយគត់នូវ item របស់ list មួយក្នុងចំណោម siblings វា។ ភាគច្រើនអ្នកនឹងប្រើ IDs ទិន្នន័យរបស់អ្នកជា keys៖

```js{2}
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

នៅពេលដែលអ្នកមិនមាន IDs មានស្ថេរភាពសម្រាប់ render items អ្នកប្រហែល index របស់ item ជា key ដែលជាជម្រើសចុងក្រោយ៖

```js{2,3}
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);
```

យើងមិនណែនាំឱ្យប្រើ indexes សម្រាប់ keys នេាះទេប្រសិនបើលំដាប់ (order) របស់ items ប្រហែលអាចត្រូវបានផ្លាស់ប្តូរតម្លៃ។ នេះអាចផ្តល់ផលប៉ះពាល់អវិជ្ជមានដល់ដំណើរការ ហើយនិងអាចបណ្តាលឱ្យមានបញ្ហាដល់ state របស់ component។ ពិនិត្យមើលអត្ថបទរបស់ Robin Pokorny សម្រាប់ [ការពន្យល់ស៊ីជម្រៅលើផលប៉ះពាល់អវិជ្ជមាននៃការប្រើប្រាស់ index ជា key](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)។ 
ប្រសិនបើអ្នកជ្រើសរើសមិន assign key ជាក់លាក់មួយទៅអោយ items របស់ list បន្ទាប់មក React នឹងប្រើ indexes ជា keys ដោយ default។

នេះគឺជា [ការពន្យល់យ៉ាងស៊ីជម្រៅអំពីហេតុអ្វី keys គឺចាំបាច់](/docs/reconciliation.html#recursing-on-children) ប្រសិនបើអ្នកចាប់អារម្មណ៍ចង់រៀនបន្ថែម។

### Extracting Components with Keys {#extracting-components-with-keys}

Keys ប្រើតែនៅក្នុង context ដែលមានការប្រើ array។

ឧទាហរណ៍ ប្រសិនបើអ្នក [extract](/docs/components-and-props.html#extracting-components) `ListItem` component មួយ អ្នកគួរតែរក្សារ key នៅលើ `<ListItem />` elements នៅក្នុង array ជាជាងនៅលើ `<li>` element នៅក្នុង `ListItem` ខ្លួនវា។

**ឧទាហរណ៍៖ ការប្រើប្រាស់ Key មិនបានត្រឹមត្រូវ**

```javascript{4,5,14,15}
function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

**ឧទាហរណ៍៖ ការប្រើប្រាស់ Key បានត្រឹមត្រូវ**

```javascript{2,3,9,10}
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/ZXeOGM?editors=0010)

ច្បាប់មួយដ៏ល្អនេាះគឺថា elements ដែលនៅខាងក្នុង `map()` ចាំបាច់ត្រូវការ keys។

### Keys Must Only Be Unique Among Siblings {#keys-must-only-be-unique-among-siblings}

<<<<<<< HEAD
Keys ដែលត្រូវបានប្រើក្នុង arrays គួរតែមានតែមួយគត់ (unique) ក្នុងចំណោម siblings រ​បស់ពួកវា។ ទោះជាយ៉ាងណា ពួកវាមិនចាំបាច់មានតែមួយគត់ (unique) ជាលក្ខណះ global នេាះទេ។ យើងអាចប្រើ keys ដូចគ្នានៅពេលដែលយើងបង្កើត arrays ពីរផ្សេងគ្នា៖
=======
Keys used within arrays should be unique among their siblings. However, they don't need to be globally unique. We can use the same keys when we produce two different arrays:
>>>>>>> 5e9d673c6bc1530c901548c0b51af3ad3f91d594

```js{2,5,11,12,19,21}
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/NRZYGN?editors=0010)

Keys ប្រើជាពត៌មានជំនួយអោយ React ប៉ុន្តែពួកវាមិនត្រូវបាន passed ឆ្លង់ទៅកាន់ components របស់អ្នកទេ។ ប្រសិនបើអ្នកត្រូវការតម្លៃដូចគ្នានៅក្នុង component របស់អ្នក, pass វាជា props ជាមួយឈ្មេាះផ្សេងគ្នា៖

```js{3,4}
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

ជាមួយឧទាហរណ៍ខាងលើ `Post` component អាចអាន `props.id` ប៉ុន្តែមិនអាចអាន `props.key`។

### Embedding map() in JSX {#embedding-map-in-jsx}

នៅក្នុងឧទាហរណ៍ខាងលើ យើងបានប្រកាសនូវ `listItems` variable ដាច់ដោយឡែកហើយនិងបានបញ្ចូលវានៅក្នុង JSX៖

```js{3-6}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX អនុញ្ញាតនូវ [ការបង្កប់ (embedding) expression មួយចំនួន](/docs/introducing-jsx.html#embedding-expressions-in-jsx) ក្នុងដង្កៀប​អង្កាញ់ (curly braces) ដូច្នេះយើងអាច inline លទ្ធផលរបស់ `map()`៖

```js{5-8}
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/BLvYrB?editors=0010)

Sometimes this results in clearer code, but this style can also be abused. Like in JavaScript, it is up to you to decide whether it is worth extracting a variable for readability. Keep in mind that if the `map()` body is too nested, it might be a good time to [extract a component](/docs/components-and-props.html#extracting-components).

ពេលខ្លះលទ្ធផលនេះ នៅក្នុង code ដែល clear ជាងនេះ, ប៉ុន្តែ style នេះក៏អាចត្រូវបានប្រើក្នុងផ្លូវខុសឬមិនសមរម្យ។ ដូចជានៅក្នុង JavaScript, វាអាស្រ័យលើអ្នកក្នុងការសម្រេចថាតើវាមានតម្លៃឬយ៉ាងណាក្នុងការ extract variable មួយដែលអាចអោយគេអានបាន (readability)។ សូមចងចាំថាប្រសិនបើ `map()` body គឺ nested ពេក, វាអាចជាពេលវេលាដ៏ល្អមួយដើម្បី [extract component មួយ](/docs/components-and-props.html#extracting-components)។
