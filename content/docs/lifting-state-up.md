---
id: lifting-state-up
title: Lifting State Up
permalink: docs/lifting-state-up.html
prev: forms.html
next: composition-vs-inheritance.html
redirect_from:
  - "docs/flux-overview.html"
  - "docs/flux-todo-list.html"
---

យើង​សូម​ផ្ដល់​អនុសាសន៍​ពីការលើក state ដែលត្រូវបាន shared ទៅកាន់ ancestor រួមគ្នាដែលជិតស្និទ្ធបំផុត។ តោះយើងមើលរបៀបដែលវាដំណើរការ។

នៅក្នុងផ្នែកនេះ យើងនឹងបង្កើតម៉ាសុីនគណនាសីតុណ្ហាភាពដែលគណនាថាទឹកនឹងឆ្អិននៅសីតុណ្ហាភាពដែលបានផ្តល់ឱ្យ។

យើងនឹងចាប់ផ្តើមជាមួយ component មួយដែលត្រូវបានគេហៅថា `BoilingVerdict`។ 
វាទទួលយកសីតុណ្ហាភាព `celsius` ជា props ហើយ prints ថាតើវាគ្រប់គ្រាន់ដើម្បីដាំទឹក៖

```js{3,5}
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>The water would boil.</p>;
  }
  return <p>The water would not boil.</p>;
}
```

បន្ទាប់មកទៀត យើងនឹងបង្កើត component មួយដែលត្រូវបានគេហៅថា `Calculator`។ វា renders `<input>` មួយដែលអនុញ្ញាតឱ្យអ្នកបញ្ចូលសីតុណ្ហភាព ហើយរក្សាតម្លៃរបស់វានៅក្នុង `this.state.temperature`។

លើសពីនេះទៀត វា renders `BoilingVerdict` សម្រាប់តម្លៃបញ្ចូលបច្ចុប្បន្ន។

```js{5,9,13,17-21}
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input
          value={temperature}
          onChange={this.handleChange} />
        <BoilingVerdict
          celsius={parseFloat(temperature)} />
      </fieldset>
    );
  }
}
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/ZXeOBm?editors=0010)

## Adding a Second Input {#adding-a-second-input}

តម្រូវការថ្មីរបស់យើងគឺថា បន្ថែមពីលើ Celsius input យើងផ្តល់ជូននូវ Fahrenheit input ហើយពួកវាត្រូវបានរក្សាទុកក្នុងលក្ខណះ sync។

យើងអាចចាប់ផ្តើមដោយការទាញយក `TemperatureInput` component ពី `Calculator`។ យើងនឹងបន្ថែម `scale` prop ថ្មីមួយអោយវាដែលអាចជា `"c"` ឬ `"f"`៖

```js{1-4,19,22}
const scaleNames = {
  c: 'Celsius',
  f: 'Fahrenheit'
};

class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

ឥឡូវនេះយើងអាចផ្លាស់ប្តូរ `Calculator` ដើម្បី render temperature inputs ពីរដាច់ដោយឡែកពីគ្នា៖

```js{5,6}
class Calculator extends React.Component {
  render() {
    return (
      <div>
        <TemperatureInput scale="c" />
        <TemperatureInput scale="f" />
      </div>
    );
  }
}
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/jGBryx?editors=0010)

ឥឡូវ​នេះយើងមាន inputs ចំនួនពីរ ប៉ុន្តែនៅពេលដែលអ្នកបញ្ចូលសីតុណ្ហភាពមួយក្នុងចំណោមពួកវា inputs ផ្សេងៗទៀតមិន update នេាះទេ។ នេះផ្ទុយនឹងតម្រូវការរបស់យើង៖ យើងចង់រក្សាវាក្នុងលក្ខណះ sync។

យើងក៏មិនអាចបង្ហាញផងដែរនូវ `BoilingVerdict` ពី `Calculator`។ `Calculator` មិនដឹងពីសីតុណ្ហភាពបច្ចុប្បន្ ពីព្រោះវាត្រូវបានលាក់នៅខាងក្នុង `TemperatureInput`។

## Writing Conversion Functions {#writing-conversion-functions}

ដំបូង យើងនឹងសរសេរ functions ពីរដើម្បីបម្លែងពី Celsius ទៅជា Fahrenheit ហើយនិងពី Fahrenheit ទៅជា Celsius៖

```js
function toCelsius(fahrenheit) {
  return (fahrenheit - 32) * 5 / 9;
}

function toFahrenheit(celsius) {
  return (celsius * 9 / 5) + 32;
}
```

functions ពីរនេះបម្លែងលេខ។ យើងនឹងសរសេរ function ផ្សេងទៀតដែលទទួលយក string `temperature` ហើយនិង converter function មួយជា arguments ហើយ returns នូវ string មួយ។ យើងនឹងប្រើវាដើម្បីគណនាតម្លៃនៃ input មួយដោយផ្អែកលើ input ផ្សេង។

វា returns string ទទេមួយនៅលើ `temperature` (សីតុណ្ហាភាព) មិនត្រឹមត្រួវមួយ ហើយវារក្សាទុក output (ទិន្នផល) ដែល rounded ទៅខ្ទង់ទសភាគទីបី៖

```js
function tryConvert(temperature, convert) {
  const input = parseFloat(temperature);
  if (Number.isNaN(input)) {
    return '';
  }
  const output = convert(input);
  const rounded = Math.round(output * 1000) / 1000;
  return rounded.toString();
}
```

ឧទាហរណ៍ `tryConvert('abc', toCelsius)` returns នូវ string ទទេមួយ ហើយ `tryConvert('10.22', toFahrenheit)` returns នូវ​ `'50.396'`។

## Lifting State Up {#lifting-state-up}

បច្ចុប្បន្ន `TemperatureInput` components ទាំងពីររក្សាតម្លៃរបស់ពួកគេនៅក្នុង local state ដោយឯករាជ្យ៖

```js{5,9,13}
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    // ...  
```

ទោះយ៉ាងណា យើងចង់អោយ inputs ទាងំពីរនេះនៅក្នុងលក្ខណះ sync ជាមួយគ្នា។ នៅពេលដែលយើង update Celsius input, Fahrenheit input គួរតែ reflect (បង្ហាយអោយឃើញនូវ) សីតុណ្ហាភាពដែលបានបម្លែង, និងផ្ទុយមកវិញ។

នៅក្នុង React ការចែករំលែក state គឺត្រូវបានសម្រេចដោយការផ្លាស់ទីវាឡើងទៅកាន់ ancestor រួមគ្នាដែលជិតស្និទ្ធបំផុត នៃ components ដែលត្រូវការវា។ នេះត្រូវបានគេហៅថា "lifting state up"។ យើងនឹងដកចេញនូវ local state ពី `TemperatureInput` ហើយផ្លាស់ទីវាទៅក្នុង `Calculator` ជំនួសវិញ។

ប្រសិនបើ `Calculator` មាន shared state ផ្ទាល់ខ្លួន, វាក្លាយជា "source of truth" សម្រាប់សីតុណ្ហាភាពបច្ចុប្បន្ននៅ inputs ទាំងពីរ។ វាអាចធ្វើអោយពួកវាទាំងពីរមានតម្លៃដែលស្របជាមួយគ្នា (consistent) ទៅវិញទៅមក។ ដែល props នៃ `TemperatureInput` components ទាំងពីរគឺមកពី parent `Calculator` component តែមួយ, inputs ទាំងពីរនឹងតែងតែមានលក្ខណះ sync។

តោះយើងមើលរបៀបដែលវាដំណើរការបានពីមួយជំហ៊ានទៅមួយជំហ៊ាន។

ដំបូង យើងនឹងជំនួស (replace) `this.state.temperature` ជាមួយ `this.props.temperature` ក្នុង `TemperatureInput` component។ សម្រាប់​ឥលូវ​នេះ ចូរក្លែងថា `this.props.temperature` ធ្លាប់​មាន​រួចហើយ, បើទោះបីជាយើងនឹងត្រូវការបេាះវាពី `Calculator` នៅពេលអនាគត៖

```js{3}
  render() {
    // Before: const temperature = this.state.temperature;
    const temperature = this.props.temperature;
    // ...
```

យើងដឹងថា [props គឺ read-only](/docs/components-and-props.html#props-are-read-only)។ នៅពេលដែល `temperature` បាននៅក្នុង local state, `TemperatureInput` គ្រាន់តែអាច call `this.setState()` ដើម្បីផ្លាស់ប្តូរវា។ ទោះយ៉ាងណា, ពេលនេះ `temperature` គឺមកពី parent ដែលជា prop, `TemperatureInput` គ្មានការគ្រប់គ្រងលើវាទេ។

នៅក្នុង React, នេះត្រូវបានដោះស្រាយជាធម្មតាដោយការបង្កើត component "controlled"។ គ្រាន់តែដូច DOM `<input>`​ ដែលទទួលយក (accepts) ទាំង `value` ហើយនិង `onChange` prop, ដូច្នេាះ custom `TemperatureInput` អាចទទួលយក (accept) ទាំង `temperature` និង `onTemperatureChange` props ពី parent `Calculator` របស់វា។

ឥឡូវ​នេះ, នៅពេលដែល `TemperatureInput` ចង់ធ្វើបច្ចុប្បន្នភាព (update) temperature របស់វា, វា calls `this.props.onTemperatureChange`៖

```js{3}
  handleChange(e) {
    // Before: this.setState({temperature: e.target.value});
    this.props.onTemperatureChange(e.target.value);
    // ...
```

>ចំណាំ៖
>
>មិនមានអត្ថន័យពិសេសចំពោះឈ្មេាះរបស់ `temperature` ឬ `onTemperatureChange` prop នៅក្នុង custom components។  យើងអាចហៅពួកគេថាអ្វីផ្សេងទៀត, ដូចជាដាក់ឈ្មោះពួក​ `value` និង `onChange` ដែលវាជា convention រួមមួយ។

`onTemperatureChange` prop នឹងត្រូវបានផ្តល់ឱ្យជាមួយគ្នានិង `temperature` prop ដោយ parent `Calculator` component។ វានឹង handle ការផ្លាស់ប្តូរដោយការកែប្រែ local state របស់ខ្លួនវាផ្ទាល់, ដូច្នេះការ re-render នូវ inputs ទាំងពីរជាមួយតម្លៃថ្មី។ យើងនឹងពិនិត្យមើលការអនុវត្ត (implementation) ថ្មីនៃ `Calculator` ឆាប់ៗនេះ។

មុនពេលចូលទៅក្នុងការផ្លាស់ប្តូរក្នុង `Calculator`, តោះពិនិត្យឡើងវិញនូវការផ្លាស់ប្តូររបស់ `TemperatureInput` component។ យើងបានដកចេញនូវ local state ពីវា, ហើយនិងជំនួយដោយការអាន (read)  `this.state.temperature`, ឥឡូវយើងអាន (read) `this.props.temperature`។ ជំនួសដោយការ call `this.setState()` នៅពេលដែលយើងចង់ផ្លាស់ប្តូរ, ឥឡូវយើង call `this.props.onTemperatureChange()`, ដែលនឹងត្រូវបានផ្តល់ដោយ `Calculator`៖

```js{8,12}
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.props.onTemperatureChange(e.target.value);
  }

  render() {
    const temperature = this.props.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

ឥឡូវនេះសូមត្រលប់ទៅ `Calculator` component វិញ។

យើងនឹងរក្សាទុក input's `temperature` និង `scale` បច្ចុប្បន្នក្នុង local state របស់វា។ នេះគឺជា state យើង "lifted up" ពី inputs, ហើយវានឹងបម្រើជា "source of truth" សម្រាប់ពួកវាទាំងពីរ។ វាជាតំណាងតូចបំផុតនៃទិន្នន័យទាំងអស់ដែលយើងត្រូវដឹងក្នុងគោលបំណង render inputs ទាំងពីរ។

ឧទាហរណ៍, ប្រសិនបើយើងបញ្ចូល​ ៣៧ ទៅក្នុង Celsius input, state នៃ `Calculator` component នឹងទៅជា៖

```js
{
  temperature: '37',
  scale: 'c'
}
```

ប្រសិនបើយើងកែសម្រួល Fahrenheit field ទៅជា ២១២ នៅពេលក្រោយ, state នៃ `Calculator` នឹងទៅជា៖

```js
{
  temperature: '212',
  scale: 'f'
}
```

យើងអាចរក្សាទុកតម្លៃនៃ inputs ទាំងពីរ, ប៉ុន្តែវាប្រែទៅជាមិនចាំបាច់។ វាគ្រប់គ្រាន់ក្នុងការរក្សាទុកតម្លៃនៃ input ដែលបានផ្លាស់ប្តូរថ្មីបំផុត, និងទំហំដែលវាតំណាងអោយ។ យើងអាចសន្និដ្ឋានបាននូវតម្លៃនៃ input ផ្សេងដោយផ្អែកលើ `temperature` ​និង `scale` តែឯង។

Inputs មានលក្ខណះជា sync ពីព្រេាះ តម្លៃរបស់ពួកវាត្រូវបានគណនាពី state ដូចគ្នា៖

```js{6,10,14,18-21,27-28,31-32,34}
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    this.state = {temperature: '', scale: 'c'};
  }

  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />
        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />
        <BoilingVerdict
          celsius={parseFloat(celsius)} />
      </div>
    );
  }
}
```

[**សាកល្បងវានៅលើ CodePen**](https://codepen.io/gaearon/pen/WZpxpz?editors=0010)

ឥឡូវ​នេះ, មិនថា input មួយណាដែលអ្នកកែប្រែ, `this.state.temperature` ហើយនិង `this.state.scale` នៅក្នុង `Calculator` និងទទួលបានការធ្វើបច្ចុប្បន្នភាព។ មួយនៃ inputs ទទួលបានតម្លៃដូច, ដូច្នេះ input របស់អ្នកប្រើប្រាស់ត្រូវបានរក្សាទុក, ហើយ តម្លៃរបស់ input ផ្សេងត្រូវបានគណនាឡើងវិញដោយផ្អែកលើវាជានិច្ច។

ចូរសង្ខេបនូវអ្វីដែលកើតឡើងនៅពេលអ្នកកែប្រែការ input៖

* React calls function ដែលបានបញ្ជាក់គឺ `onChange` នៅលើ DOM `<input>`។ នៅក្នុងករណីរបស់យើង, នេះគឺ `handleChange` method នៅក្នុង `TemperatureInput` component។
* `handleChange` method នៅក្នុង `TemperatureInput` component calls `this.props.onTemperatureChange()` ជាមួយនឹងតម្លៃថ្មីដែលចង់បាន។ props របស់វា, រួមទាំង `onTemperatureChange`, ត្រូវបានផ្តល់ដោយ​ parent component របស់វាគឺ `Calculator`។
* នៅពេលដែលវាបាន render ពីមុន, `Calculator` បានបញ្ជាក់ថា `onTemperatureChange` នៃ `TemperatureInput` របស់ Celsius គឺជា `handleCelsiusChange` method របស់ `Calculator`, ហើយ  `onTemperatureChange` នៃ Fahrenheit `TemperatureInput` គឺជា `handleFahrenheitChange` method របស់ `Calculator`។ ដូច្នេះ methods ទាំងពីររបស់ `Calculator` ត្រូវបាន call ដោយផ្អែកលើការ input ដែលយើងបានកែសម្រួល។
* នៅក្នុង methods ទាំងនេះ, `Calculator` component ស្នើរ React ដើម្បី re-render ខ្លួនវាដោយការ call `this.setState()` ជាមួយតម្លៃថ្មីរបស់ input និង scale ​បច្ចុប្បន្ននៃ input ដែលយើងទើបតែកែសម្រួល។
* React calls `render` method របស់ `Calculator` component ដើម្បីស្វែងយល់ថា តើ UI គួរមើលឃើញដូចម្តេច។ ម្លៃនៃ inputs ទាំងពីរត្រូវបានគណនាឡើងវិញផ្អែកលើ temperature ​បច្ចុប្បន្ននិង active scale។ ការបម្លែងសីតុណ្ហភាពត្រូវបានអនុវត្តនៅទីនេះ។
* React calls `render` methods នៃ `TemperatureInput` components ផ្ទាល់ខ្លួនជាមួយ props ថ្មីរបស់ពួកវាដែលបានបញ្ជាក់ដោយ `Calculator`។ វាដឹងថា UI របស់ពួកគេគួរតែមានលក្ខណៈដូចម្តេច។
* React calls `render` method នៃ `BoilingVerdict` component, ដោយការបេាះ temperature នៅក្នុង Celsius ជា props របស់វា។
* React DOM ធ្វើបច្ចុប្បន្នភាព DOM ជាមួយ boiling verdict ហើយនិងដើម្បីផ្គូផ្គងតម្លៃ input ដែលចង់បាន។ input ដែលយើងបានកែតម្រូវទទួលបានតម្លៃបច្ចុប្បន្នរបស់វា, ហើយ input ផ្សេងៗត្រូវបានធ្វើឱ្យទាន់សម័យទៅសីតុណ្ហភាពបន្ទាប់ពីបម្លែង។

រាល់ការធ្វើបច្ចុប្បន្នភាពត្រូវឆ្លងកាត់ជំហានដូចគ្នាដូច្នេះ input នូវរក្សារលក្ខណះ sync។

## Lessons Learned {#lessons-learned}

វាគួរតែមាន "source of truth" តែមួយសម្រាប់ទិន្នន័យណាមួយដែលផ្លាស់ប្តូរនៅក្នុង React application។ ជាធម្មតា, state ត្រូវបានបន្ថែមជាលើកដំបូងទៅអោយ component ដែលត្រូវការវាសម្រាប់ការ​ render។ ប្រសិនបើ components ផ្សេងៗត្រូវការវាដែរ, អ្នកអាចលើកវាទៅកាន់ក្រុម ancestor ដែលជិតបំផុតរបស់វា។ ជំនួសឱ្យការព្យាយាម sync state រវាង components ខុសគ្នា, អ្នកគួរតែពឹងផ្អែកលើ [top-down data flow](/docs/state-and-lifecycle.html#the-data-flows-down)។

ការលើក state ជាប់ពាក់ព័ន្ធនឹងការសរសេរបន្ថែម code "boilerplate" ច្រើនជាង វិធីសាស្រ្ two-way binding, ប៉ុន្តែជាប្រយោជន៍មួយ, វាធ្វើការតិចតួចដើម្បីរកនិងកម្ចាត់ bugs។ ដែល state មួយចំនួន "lives" នៅក្នុង ​component​ ខ្លះហើយ component នេាះអាចផ្លាស់ប្តូរវាបាន, bugs ត្រូវបានកាត់បន្ថយយ៉ាងខ្លាំង។ លើសពីនេះទៀត, អ្នកអាច impement custom logic មួយចំនួនដើម្បីបដិសេធឬបំលែងការបញ្ចូលរបស់អ្នកប្រើ។

ប្រសិនបើមានអ្វីអាចទាញចេញពី props ឬក័ state, វាប្រហែលជាមិនគួរនៅក្នុង state, ឧទាហរណ៍, ជំនួសឱ្យការរក្សាទុកទាំង `celsiusValue` និង `fahrenheitValue`, យើងរក្សាទុកតែការកែប្រែចុងក្រោយនូវ `temperature` និង `scale` របស់វាប៉ុណ្ណោះ។ តម្លៃនៃការ input ផ្សេងៗអាច
តែងតែអាចគណនាពីពួកវាបាននៅក្នុង `render` method។ នេះអនុញ្ញាតឱ្យយើងសម្អាត (clear) ឬអនុវត្ត (apply) field ផ្សេង ដោយមិនបាត់បង់ precision ក្នុងការបញ្ចូលរបស់អ្នកប្រើប្រាស់។

<<<<<<< HEAD
នៅពេលដែលអ្នកឃើញអ្វីមួយខុសនៅក្នុង UI, អ្នកអាចប្រើ [React Developer Tools](https://github.com/facebook/react/tree/master/packages/react-devtools) ដើម្បី inspect props ហើយនិង move up the tree រហូតដល់អ្នករកឃើញ​ component ដែលទទួលខុសត្រូវសម្រាប់ធ្វើបច្ចុប្បន្នភាព​ state។ នេះអនុញ្ញាតឱ្យអ្នកតាមដានកំហុសទៅកាន់ប្រភពរបស់វា៖
=======
When you see something wrong in the UI, you can use [React Developer Tools](https://github.com/facebook/react/tree/main/packages/react-devtools) to inspect the props and move up the tree until you find the component responsible for updating the state. This lets you trace the bugs to their source:
>>>>>>> 5f0549c86e7a9c0774e66687d1bc0118a681eb9d

<img src="../images/docs/react-devtools-state.gif" alt="Monitoring State in React DevTools" max-width="100%" height="100%">
