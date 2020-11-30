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

ជាមួយនិង controlled component, តម្លៃរបស់ input គឺតែងតែ driven ដោយ React state។ ខណៈពេលនេះមានន័យថាអ្នកត្រូវវាយកូដបន្ថែមទៀត, ឥឡូវអ្នកអាចបញ្ជូនតម្លៃទៅកាន់ UI elements ផ្សេងៗដែរ, ឬ reset វាពី event handlers ផ្សេងៗ។

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

នៅពេលអ្នកត្រូវការ handle controlled `input` elements ច្រើន, អ្នកអាចបន្ថែម `name` attribute ទៅកាន់ element នីមួយៗហើយនិងអនុញ្ញាតឱ្យ handler function ជ្រើសរើសអ្វីដែលត្រូវធ្វើដោយផ្អែកលើតម្លៃនៃ `event.target.name` ។

ឧទាហរណ៍៖

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

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/wgedvV?editors=0010)

ចំណាំរបៀបដែលយើងប្រើ ES6 [computed property name](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names) syntax ដើម្បីធ្វើបច្ចុប្បន្នភាព state key ដែលត្រូវគ្នានិង input name ដែលត្រូវបានផ្តល់អោយ៖

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

ដូចគ្នា, ដែល `setState()` [ធ្នើការបញ្ចូលគ្នានូវ partial state ទៅក្នុង current state](/docs/state-and-lifecycle.html#state-updates-are-merged) ដោយស្វ័យប្រវត្តិ, យើងគ្រាន់តែត្រូវការ call វាជាមួយនិងផ្នែកណាដែលត្រូវបានផ្លាស់ប្តូរ។

## Controlled Input Null Value {#controlled-input-null-value}

ការបញ្ជាក់ value props នៅលើ [controlled component](/docs/forms.html#controlled-components) ការពារអ្នកប្រើប្រាស់ពីការផ្លាស់ប្តូរ input លុះត្រាតែអ្នកចង់ធ្វើដូច្នេះ។ ប្រសិនបើអ្នកមិនបានបញ្ជាក់ `value` ប៉ុន្តែ input នៅតែអាចកែបាន, អ្នកប្រហែលជាបានកំណត់ `value` ជា `undefined` ឬក៏ `null` ដោយចៃដន្យ។

កូដខាងក្រោមបង្ហាញដូចនេះ។ (input ត្រូវបាន lock ពេលដំបូង ប៉ុន្តែបានក្លាយជាអាចកែបានបន្ទាប់ពីមានការពន្យាពេលខ្លីមួយ។)

```javascript
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);

```

## Alternatives to Controlled Components {#alternatives-to-controlled-components}

ពេលខ្លះវាអាចធុញទ្រាន់ក្នុងការប្រើ controlled components, ពីព្រោះអ្នកត្រូវសរសេរ event handler សម្រាប់គ្រប់វិធីដែល data របស់អ្នកអាចផ្លាស់ប្តូរហើយនិង pipe input state ទាំងអស់តាមរយៈ React component។ នេះអាចក្លាយជាការរំខានជាពិសេសនៅពេលអ្នកកំពុងបម្លែង preexisting codebase ទៅជា React, 
ឬការរួមបញ្ចូលគ្នានូវ React application ជាមួយនិង non-React library។ ក្នុងស្ថានភាពនេះ អ្នកប្រហែលជាចង់ពិនិត្យមើល [uncontrolled components](/docs/uncontrolled-components.html), បច្ចេកទេសដែលជាជម្រើសមួយ​សម្រាប់ការ implement input forms។

## Fully-Fledged Solutions {#fully-fledged-solutions}

ប្រសិនបើអ្នកកំពុងស្វែងរកដំណោះស្រាយពេញលេញរួមបញ្ចូលទាំង validation, ការរក្សារការតាមដាននៃ visited fields, ហើយនិងការ handle ការ submit form, [Formik](https://jaredpalmer.com/formik) គឺជាផ្នែកមួយនៃជម្រើសដ៏ពេញនិយម។ ទោះជាយ៉ាងណាក៏ដោយ វាត្រូវបានបង្កើតតាមគោលការណ៍ដូចគ្នានៃ controlled components និងការគ្រប់គ្រង state — ដូច្នេះកុំភ្លេចរៀនវា។
