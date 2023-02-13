---
id: hooks-rules
title: Rules of Hooks
permalink: docs/hooks-rules.html
next: hooks-custom.html
prev: hooks-effect.html
---

*Hooks* គឺជាមុខងារថ្មីមួយនៅក្នុងជំនាន់ React ១៦.៨ វាមានលក្ខណៈពិសេសដែលអាចឲ្យអ្នកប្រើប្រាស់ State និងមុខងារ React ដទៃទៀតដោយមិនចាំបាច់ class។

Hooks គឺជា JavaScript functions, ប៉ុន្តែអ្នកត្រូវអនុវត្តតាមច្បាប់ពីរនៅពេលប្រើវា។ យើងផ្តល់ជូននូវ [linter plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks) ដើម្បីអនុវត្តច្បាប់ទាំងនេះដោយស្វ័យប្រវត្តិ៖

### Only Call Hooks at the Top Level {#only-call-hooks-at-the-top-level}

<<<<<<< HEAD
**កុំ call Hooks នៅខាងក្នុង loops, conditions, ឬ nested functions។** ជំនួស, តែងតែប្រើ Hooks នៅ top level នៃ React function របស់អ្នក។ ដោយធ្វើតាមច្បាប់នេះ, អ្នកត្រូវធានាថា Hooks ត្រូវបាន call នៅក្នុងលំដាប់ដូចគ្នារាល់ពេលដែល component renders។ នោះហើយជាអ្វីដែលអនុញ្ញាតឱ្យ React ដើម្បីការពារយ៉ាងត្រឹមត្រូវនូវ state នៃ Hooks រវាង ការហៅ `useState` និង `useEffect` ច្រើន។ (ប្រសិនបើអ្នកចង់ដឹង, យើងនឹងពន្យល់រឿងនេះឱ្យកាន់តែស៊ីជម្រៅ [ខាងក្រោម](#explanation)។)
=======
**Don't call Hooks inside loops, conditions, or nested functions.** Instead, always use Hooks at the top level of your React function, before any early returns. By following this rule, you ensure that Hooks are called in the same order each time a component renders. That's what allows React to correctly preserve the state of Hooks between multiple `useState` and `useEffect` calls. (If you're curious, we'll explain this in depth [below](#explanation).)
>>>>>>> 47adefd30c46f486428d8231a68e639d62f02c9e

### Only Call Hooks from React Functions {#only-call-hooks-from-react-functions}

**កុំ call Hooks ពី regular JavaScript functions។** ជំនួស, អ្នកអាច៖

* ✅ Call Hooks ពី React function components.
* ✅ Call Hooks ពី custom Hooks (យើងនឹងរៀនអំពីពួកវា [នៅទំព័របន្ទាប់](/docs/hooks-custom.html)).

ដោយធ្វើតាមច្បាប់នេះ, អ្នកត្រូវធានាថា stateful logic ទាំងអស់ នៅក្នុង component គឺអាចមើលឃើញយ៉ាងច្បាស់ ពី source code របស់វា។

## ESLint Plugin {#eslint-plugin}

យើងបាន release ESLint plugin មួយ ត្រូវបានគេហៅថា [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) ដែលអនុវត្តច្បាប់ទាំងពីរនេះ។ អ្នកអាចបន្ថែម plugin នេះទៅក្នុង project របស់អ្នក ប្រសិនបើអ្នកចង់សាកល្បងវា៖

Plugin នេះគឺត្រូវបានរួមបញ្ចូលដោយ default នៅក្នុង [Create React App](/docs/create-a-new-react-app.html#create-react-app)។

```bash
npm install eslint-plugin-react-hooks --save-dev
```

```js
// Your ESLint configuration
{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    "react-hooks/rules-of-hooks": "error", // Checks rules of Hooks
    "react-hooks/exhaustive-deps": "warn" // Checks effect dependencies
  }
}
```

**You can skip to the next page explaining how to write [your own Hooks](/docs/hooks-custom.html) now.** On this page, we'll continue by explaining the reasoning behind these rules.

**អ្នកអាចរំលងទៅទំព័របន្ទាប់ដែលពន្យល់ពីរបៀបសរសេរ [Hooks ផ្ទាល់ខ្លួនរបស់អ្នក](/docs/hooks-custom.html)**

## Explanation {#explanation}

ដូចដែលយើង [បានរៀនមុននេះបន្តិច](/docs/hooks-state.html#tip-using-multiple-state-variables), យើងអាចប្រើ State ឬ Effect Hooks ច្រើ​ន នៅក្នុង single component មួយ៖

```js
function Form() {
  // 1. Use the name state variable
  const [name, setName] = useState('Mary');

  // 2. Use an effect for persisting the form
  useEffect(function persistForm() {
    localStorage.setItem('formData', name);
  });

  // 3. Use the surname state variable
  const [surname, setSurname] = useState('Poppins');

  // 4. Use an effect for updating the title
  useEffect(function updateTitle() {
    document.title = name + ' ' + surname;
  });

  // ...
}
```

ដូច្នេះតើធ្វើដូចម្តេចទើប React ដឹងថា state មួយណា ត្រូវគ្នា នឹងការ call `userState`​ មួយណា? ចម្លើយគឺថា **React ពឹកផ្អែកលើលំដាប់ដែល Hooks ត្រូវបាន call**។ ឧទាហរណ៍របស់យើងដំណើរការពីព្រោះ លំដាប់នៃការ calls Hook គឺដូចគ្នានៅគ្រប់ការ render៖

```js
// ------------
// First render
// ------------
useState('Mary')           // 1. Initialize the name state variable with 'Mary'
useEffect(persistForm)     // 2. Add an effect for persisting the form
useState('Poppins')        // 3. Initialize the surname state variable with 'Poppins'
useEffect(updateTitle)     // 4. Add an effect for updating the title

// -------------
// Second render
// -------------
useState('Mary')           // 1. Read the name state variable (argument is ignored)
useEffect(persistForm)     // 2. Replace the effect for persisting the form
useState('Poppins')        // 3. Read the surname state variable (argument is ignored)
useEffect(updateTitle)     // 4. Replace the effect for updating the title

// ...
```

ដរាបណាលំដាប់នៃការ calls Hooks គឺដូចគ្នារវាង renders, React អាចភ្ជាប់ local state មួយចំនួនទៅវិញទៅមក។ ប៉ុន្តែមានអ្វីកើតឡើង ប្រសិនបើយើងដាក់ការ call Hook មួយ (ឧទាហរណ៍, `persistForm` effect) នៅខាងក្នុង condition មួយ?

```js
  // 🔴 We're breaking the first rule by using a Hook in a condition
  if (name !== '') {
    useEffect(function persistForm() {
      localStorage.setItem('formData', name);
    });
  }
```

`name !== ''` condition គឺ `true` ទៅលើការ render តំបូង, ដូច្នេះយើង run Hook នេះ។ ទោះយ៉ាងណាក៏ដោយ, ទៅលើការ render បន្ទាប់ user ប្រហែលជា clear the form, ធ្វើអោយ condition `false`។ ឥឡូវយើងរំលង (skip) Hook នេះកំឡុងពេល rendering, លំដាប់នៃការ calls Hook ក្លាយជាខុសគ្នា៖

```js
useState('Mary')           // 1. Read the name state variable (argument is ignored)
// useEffect(persistForm)  // 🔴 This Hook was skipped!
useState('Poppins')        // 🔴 2 (but was 3). Fail to read the surname state variable
useEffect(updateTitle)     // 🔴 3 (but was 4). Fail to replace the effect
```

React នឹងមិនដឹងអ្វីដែលត្រូវ return សម្រាប់ការ call `useState` ទីពីរ។ React រំពឹងថាការ call Hook ទីពីរនៅក្នុង component នេះ ត្រូវគ្នានឹង `persistForm` effect, ដូចនឹងកំឡុងពេល previous render, ប៉ុន្តែវាមិនមានទៀតទេ។ ពីចំនុចនេាះ, រាល់ការ call next Hook បន្ទាប់មកមួយដែលយើងបានរំលង (skip) ក៏នឹងផ្លាស់ប្តូរដោយមួយ,​ នាំទៅរក bugs។

**នេះគឺជាមូលហេតុ Hook ត្រូវតែ ត្រូវបាន call នៅ top level នៃ components របស់យើង។** ប្រសិនបើយើងចង់ run effect ដោយមានលក្ខខណ្ឌ, យើងអាចដាក់ condtion នេាះ *នៅខាងក្នុង* Hook របស់យើង៖

```js
  useEffect(function persistForm() {
    // 👍 We're not breaking the first rule anymore
    if (name !== '') {
      localStorage.setItem('formData', name);
    }
  });
```

**កត់សម្គាល់ថា អ្នកមិនចាំបាច់ព្រួយបារម្ភអំពីបញ្ហានេះទេប្រសិនបើអ្នកប្រើ [lint rule ដែលត្រូវបានផ្តល់អោយ](https://www.npmjs.com/package/eslint-plugin-react-hooks)។** តែឥឡូវអ្នកក៏ដឹងដែរ *ហេតុអ្វី* Hooks ដំណើរការតាមវិធីនេះ, ហើយបញ្ហា (issues) ណាមួយដែលវិធាន (rule) គឺកំពុងរារាំង (prevent)។

## Next Steps {#next-steps}

ទីបំផុត, យើងត្រៀមខ្លួនដើម្បីរៀនពី [ការសរសេរ Hooks ផ្ទាល់ខ្លួនរបស់អ្នក](/docs/hooks-custom.html)! Custom Hooks អនុញ្ញាតឱ្យអ្នក combine Hooks ដែលផ្តល់ដោយ React ទៅក្នុង abstractions ផ្ទាល់ខ្លួនរបស់អ្នក, ហើយនិងប្រើឡើងវិញ (reuse) stateful logic ទូទៅ រវាង components ផ្សេងៗ។
