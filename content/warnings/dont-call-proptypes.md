---
title: Don't Call PropTypes Warning
layout: single
permalink: warnings/dont-call-proptypes.html
---

> ចំណាំ:
>
> `React.PropTypes` ត្រូវបាន ផ្លាស់ប្ដូរទៅកាន់ package ផ្សេងទៀត ចាប់តាំង ពី React ជំនាន់ 15.5។ សូមប្រើប្រាស់ [`prop-types` library](https://www.npmjs.com/package/prop-types) ជំនួសវិញ។
>
>យើងបានប្រើប្រាស់ [a codemod script](/blog/2017/04/07/react-v15.5.0.html#migrating-from-react.proptypes) ដើម្បីធ្វើ automate the conversion.

រៀងរាល់ major realase របស់ React នៅថ្ងៃអនាគត កូដដែលមាន មុខងារ PropType validation និងត្រូវបាន ដកចេញ នៅលើ production។ នៅពេលនោះ រៀងរាល់ កូដ ដែលធ្វើការហៅ function ទាំងនោះដោយផ្ទាល់ (ដែលមិនបាន ដកចេញ ពី production) នឹង បង្កើតអោយមាន error។

### ការប្រកាស់ PropTypes នៅអាចធ្វើបាន {#declaring-proptypes-is-still-fine}

របៀបប្រើប្រាស់ PropTypes បែប នៅតែបន្តប្រើប្រាស់បាន:

```javascript
Button.propTypes = {
  highlighted: PropTypes.bool
};
```

គ្មានអ្វី ផ្លាស់ប្តូរ នោះទេ។

### កុំហៅ PropTypes ដោយផ្ទាល់ {#dont-call-proptypes-directly}

ការប្រើប្រាស់ PropTypes នៅលើវិធីសាស្រ្ត ណាមួយ ដែលមិនមែនជា ជាការសរសេរពន្យល់ ទៅលើ React components នឹង មិនអាចបន្តប្រើប្រាស់ បានទៀតទេ:

```javascript
var apiShape = PropTypes.shape({
  body: PropTypes.object,
  statusCode: PropTypes.number.isRequired
}).isRequired;

// Not supported!
var error = apiShape(json, 'response');
```

ប្រសិនបើ ត្រូវពឹងផ្អែកលើ PropTypes បែបនេះ យើងណែនាំអោយ ប្រើប្រាស់ ឬ បង្កើត fork ថ្មីចេញពី PropTypes (ដូចទៅនឹង package [ទាំង](https://github.com/aackerman/PropTypes) [ពីរ](https://github.com/developit/proptypes) នេះ)។

ប្រសិនបើអ្នក មិនដោះស្រាយ warning នេះទេ នោះអាចនឹង ធ្វើអោយ កូដ crash នៅលើ production ជាមួយ React ជំនាន់ទី១៦។

### ប្រសិនបើអ្នកមិនហៅ PropTypes ដោយធម្មតា ប៉ុន្តែនៅតែទទួលបាន warning  {#if-you-dont-call-proptypes-directly-but-still-get-the-warning}

ពិនិត្យ stack trace ដែលបានបង្កើតដោយ warning។ អ្នកអារចរកឃើញ component ដែលទទួលខុសត្រូវ ចំពោះការហៅ PropTypes ដោយផ្ទាល់។ មូលហេតុភាគច្រើន ដែលបង្ករអោយមាន បញ្ហានេះកើតឡើង គីបណ្ដាលមកពី third party PropTypes ដែលសរសេរគ្របពីលើ PropTypes របស់ React។ ឧទាហរណ៍:

```js
Button.propTypes = {
  highlighted: ThirdPartyPropTypes.deprecated(
    PropTypes.bool,
    'Use `active` prop instead'
  )
}
```

ក្នុងករណីនេះ `ThirPartyPropTypes.deprecated` ជាការហៅរបស់ wrapper `PropTypes.bool`។ តាមលំនាំ បែបនេះ គីមិនមាន បញ្ហានោះទេ ប៉ុន្តែ វានឹងបង្កើតអោយមាន false positive ពីព្រោះ React បានគិតថា អ្នកបានធ្វើការហៅ PropTypes ដោយផ្ទាល់។ ផ្នែកបន្ទាប់ នឹង ធ្វើការបកស្រាយ ពីការដោះស្រាយ បញ្ហានេះសម្រាប់ library ដែល implement អ្វីដែលដូចជា `ThirdPartyPropTypes`។ ប្រសិនបើវា  មិនមែនជា library ដែលជារបស់អ្នកនោះទេ អ្នកអាចបង្កើត issue ប្រឆាំងនឹងវាបាន។

### ការកែកំហុស false positive នៅលើ third party PropTypes {#fixing-the-false-positive-in-third-party-proptypes}

ប្រសិនបើអ្នក អ្នកសរសេរ third-party PropTypes ហើយបាន អនុញ្ញាត្តអោយ អ្នកប្រើប្រាស់ សរសេរគ្របពីលើ React PropTypes ដែលមានស្រាប់ នោះអាចអោយ អ្នកប្រើប្រាស់ មើលឃើញថា ពាក្យ warning កើតចេញមកពី library របស់អ្នក។ វាកើតឡើងដោយសារ React មិនអាចមើលឃើញ "secret" ជា argument ចុងក្រោដែល [បានបោះ](https://github.com/facebook/react/pull/7132) សម្រាប់ស្វែងរក ការហៅ PropTypes ដោយផ្ទាល។

ដើម្បីធ្វើការ កែហុសនេះ។ យើងនឹងតម្រូវអោយប្រើ `deprecated` មកពី [react-bootstrap/react-prop-types](https://github.com/react-bootstrap/react-prop-types/blob/0d1cd3a49a93e513325e3258b28a82ce7d38e690/src/deprecated.js) ជាឧទាហរណ៍។ សម្រាប់ការ អនុវត្តនេះ យើងបានបន្ត arguments ដូចជា `props`, `propName`, and `componentName`:

```javascript
export default function deprecated(propType, explanation) {
  return function validate(props, propName, componentName) {
    if (props[propName] != null) {
      const message = `"${propName}" property of "${componentName}" has been deprecated.\n${explanation}`;
      if (!warned[message]) {
        warning(false, message);
        warned[message] = true;
      }
    }

    return propType(props, propName, componentName);
  };
}
```

ដើម្បីធ្វើការ កែកំហុស false positive ត្រូវចាំអោយច្បាស់ អ្នកត្រូវបោះបន្ត គ្រប់ arguments **ទាំងអស់** បន្តទៅកាន់ function ដែលក្ដោប PropType។  វិធីសាស្ត្រនេះ មានភាពងាយស្រួល សម្រាប់ ES6 `...rest` notation:
```javascript
export default function deprecated(propType, explanation) {
  return function validate(props, propName, componentName, ...rest) { // Note ...rest here
    if (props[propName] != null) {
      const message = `"${propName}" property of "${componentName}" has been deprecated.\n${explanation}`;
      if (!warned[message]) {
        warning(false, message);
        warned[message] = true;
      }
    }

    return propType(props, propName, componentName, ...rest); // and here
  };
}
```

បែបនេះ នឹងអាច បញ្ឈប់ warning។