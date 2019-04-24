---
id: forms
title: Forms
permalink: docs/forms.html
prev: lists-and-keys.html
next: lifting-state-up.html
redirect_from:
  - "tips/controlled-input-null-value.html"
  - "docs/forms-zh-CN.html"
---

HTML form elements ធ្វើការខុសគ្នាបន្តិចពី DOM elements ផ្សេងៗនៅក្នុង React ពីព្រេាះ form elements ជាធម្មតាវារក្សារទុកនូវ internal state មួយចំនួន។ ឧទាហរណ៍ form នេះគឺជា plain HTML ទទួលយកឈ្មោះតែមួយ៖

```html
<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

Form នេះមានលក្ខណះជា default HTML នៃការ browse ទៅកាន់ page ថ្មីនៅពេលដែលអ្នក​ប្រើ (user) submits form។ ប្រសិនបើអ្នកចង់បានលក្ខណះបែបនេះនៅក្នុង React វាអាចដំណើរការបាន។ ប៉ុន្តែនៅក្នុងករណីជាច្រើន វាមានភាពងាយស្រួលក្នុងការមាន JavaScript function មួយដែលដែលគ្រប់គ្រងក្នុងការ submits form ហើយនិងមានសិទ្ធិចូលដំណើរការទិន្នន័យដែលអ្នកប្រើប្រាស់ (user) បានបញ្ចូលទៅក្នុង form។ វិធីស្តង់ដារដើម្បីសម្រេចបានដូចនេះគឺជាមួយនិងបច្ចេកទេស (technique) ដែលគេហៅថា "controlled components"។

## Controlled Components {#controlled-components}

នៅក្នុង HTML form elements ដូចជា `<input>`, `<textarea>`, និង `<select>` ជាធម្មតា maintain state ដោយខ្លួនរបស់ពួកវាហើយធ្វើបច្ចុប្បន្នភាព (update) វាដោយផ្អែកលើការបញ្ចូលរបស់អ្នកប្រើ។ ក្នុង React, state ដែលអាចប្ដូរតម្លៃបានជាធម្មតាត្រូវបានរក្សារនៅក្នុង state property នៃ components និងបានធ្វើបច្ចុប្បន្នភាពតែជាមួយ [`setState()`](/docs/react-component.html#setstate)។

យើងអាចផ្សំទាំងពីរបញ្ចូលគ្នាដោយបង្កើត React state ជា "single source of truth"។ បន្ទាប់មកទៀត React component ដែល renders form ក៏គ្រប់គ្រងផងដែរនូវអ្វីដែលកើតឡើងនៅក្នុង form ទៅលើការបញ្ចូលរបស់អ្នកប្រើប្រាស់ជាបន្តបន្ទាប់។ input form element ដែល value របស់វាត្រូវបានគ្រប់គ្រងដោយ React នៅក្នុងវិធីនេះត្រូវបានគេហៅថា​​ "controlled component"។

ឧទាហរណ៍ ប្រសិនបើអ្នកចង់បង្កើតឧទាហរណ៍មុនដោយអោយវា log នូវ name នៅពេលដែលវាត្រូវបាន submit យើងអាចសរសេរ form ជា controlled component៖

```javascript{4,10-12,24}
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/VmmPgp?editors=0010)

ដែល `value` attribute គឺ set នៅលើ form element របស់យើង, តម្លៃដែលបានបង្ហាញនឹងតែងតែជា `this.state.value`, ការបង្កើត React state ជា source of truth។ ដែល `handleChange` runs នៅលើគ្រប់ក្តារចុចដើម្បីធ្វើបច្ចុប្បន្នភាព (update) React state, 
តម្លៃដែលបានបង្ហាញនឹងធ្វើបច្ចុប្បន្នភាពដូចអ្វីដែលអ្នកប្រើប្រាស់វាយ។

ជាមួយនិង controlled component, រាល់ state ដែលអាចផ្លាស់ប្តូរនឹងមាន handler function ដែលជាប់ទាក់ទង។ នេះធ្វើឱ្យវាងាយស្រួលដើម្បីកែប្រែឬក៏ validate ការបញ្ចូលរបស់អ្នកប្រើប្រាស់។ ឧទាហរណ៍ ប្រសិនបើយើងចង់បង្ខំអោយ names ត្រូវបានសរសេរជាមួយអក្សរធំទាំងអស់ (uppercase letters) យើងអាចសរសេរ `handleChange` ដូចនេះ៖

```javascript{2}
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}
```

## The textarea Tag {#the-textarea-tag}

នៅក្នុង HTML `<textarea>` element កំណត់ text របស់វាដោយ children របស់វា៖

```html
<textarea>
  Hello there, this is some text in a text area
</textarea>
```

នៅក្នុង React `<textarea>` ប្រើ `value` attribute ជំនួសវិញ។ មធ្យោបាយនេះ, ការប្រើ form ជាមួយ `<textarea>` អាចត្រូវបានសរសេរស្រដៀងទៅនឹង form ដែលប្រើ single-line input៖

```javascript{4-6,12-14,26}
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

សម្គាល់​ឃើញ​ថា `this.state.value` គឺត្រូវបាន initialize នៅក្នុង constructor ដូច្នេះ text area ចាប់ផ្តើមជាមួយនិង text មួយចំនួននៅខាងក្នុងវា។

## The select Tag {#the-select-tag}

នៅក្នុង HTML `<select>` បង្កើតតារាង drop-down។ ឧទាហរណ៍ HTML នេះបង្កើតតារាង drop-down មួយនៃរស់ជាតិ៖

```html
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

ចំណាំ​ថា Coconut option ត្រូវបានជ្រើសរើសដំបូង ដោយសារ `selected` attribute។ React, ជំនួសឱ្យការប្រើ `selected` attribute នេះ, ​ប្រើ `value` attribute នៅលើ root `select` tag។ នេះគឺកាន់តែងាយស្រួលនៅក្នុង controlled component ពីព្រេាះអ្នកគ្រានតែត្រូវការ update វានៅកន្លែងតែមួយ។ ឧទាហរណ៍៖


```javascript{4,10-12,24}
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/JbbEzX?editors=0010)

ជារួម, នេះធ្វើឱ្យវាដូច្នេះ `<input type="text">`, `<textarea>`, និង `<select>` ដំណើរការស្រដៀងគ្នាទាំងអស់ - ពួកវាទាំងអស់ទទួលយក `value` attribute ដែលអ្នកអាចប្រើដើម្បី implement controlled component។

> ចំណាំ
>
> អ្នកអាចបេាះ array​ ទៅអោយ `value` attribute, អនុញ្ញាតឱ្យអ្នកជ្រើសរើសជម្រើសច្រើននៅក្នុង `select` tag៖
>
>```js
><select multiple={true} value={['B', 'C']}>
>```

## The file input Tag {#the-file-input-tag}

នៅក្នុង HTML, `<input type="file">` អនុញ្ញាតឱ្យអ្នកប្រើប្រាស់ជ្រើសរើសឯកសារ (files )មួយឬច្រើនពីឧបករណ៍ផ្ទុករបស់ពួកគេដើម្បី upload ទៅកាន់ server ឬក៏រៀបចំដោយ JavaScript តាម​រយៈ [File API](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)។

```html
<input type="file" />
```

ដោយសារតែតម្លៃរបស់វាគឺបានតែអាន, វាគឺជា **uncontrolled** component នៅក្នុង React។ វាត្រូវបានគេយកមកពិភាក្សាជាមួយនិង uncontrolled components ផ្សេងទៀត [នៅពេលក្រោយនៅក្នុងឯកសារ](/docs/uncontrolled-components.html#the-file-input-tag)។

## Handling Multiple Inputs {#handling-multiple-inputs}

When you need to handle multiple controlled `input` elements, you can add a `name` attribute to each element and let the handler function choose what to do based on the value of `event.target.name`.

For example:

```javascript{15,18,28,37}
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/wgedvV?editors=0010)

Note how we used the ES6 [computed property name](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names) syntax to update the state key corresponding to the given input name:

```js{2}
this.setState({
  [name]: value
});
```

It is equivalent to this ES5 code:

```js{2}
var partialState = {};
partialState[name] = value;
this.setState(partialState);
```

Also, since `setState()` automatically [merges a partial state into the current state](/docs/state-and-lifecycle.html#state-updates-are-merged), we only needed to call it with the changed parts.

## Controlled Input Null Value {#controlled-input-null-value}

Specifying the value prop on a [controlled component](/docs/forms.html#controlled-components) prevents the user from changing the input unless you desire so. If you've specified a `value` but the input is still editable, you may have accidentally set `value` to `undefined` or `null`.

The following code demonstrates this. (The input is locked at first but becomes editable after a short delay.)

```javascript
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);

```

## Alternatives to Controlled Components {#alternatives-to-controlled-components}

It can sometimes be tedious to use controlled components, because you need to write an event handler for every way your data can change and pipe all of the input state through a React component. This can become particularly annoying when you are converting a preexisting codebase to React, or integrating a React application with a non-React library. In these situations, you might want to check out [uncontrolled components](/docs/uncontrolled-components.html), an alternative technique for implementing input forms.

## Fully-Fledged Solutions {#fully-fledged-solutions}

If you're looking for a complete solution including validation, keeping track of the visited fields, and handling form submission, [Formik](https://jaredpalmer.com/formik) is one of the popular choices. However, it is built on the same principles of controlled components and managing state — so don't neglect to learn them.
