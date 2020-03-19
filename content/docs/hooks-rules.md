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

**កុំ call Hooks នៅខាងក្នុង loops, conditions, ឬ nested functions។** ជំនួស, តែងតែប្រើ Hooks នៅ top level នៃ React function របស់អ្នក។ ដោយធ្វើតាមច្បាប់នេះ, អ្នកត្រូវធានាថា Hooks ត្រូវបាន call នៅក្នុងលំដាប់ដូចគ្នារាល់ពេលដែល component renders។ នោះហើយជាអ្វីដែលអនុញ្ញាតឱ្យ React ដើម្បីការពារយ៉ាងត្រឹមត្រូវនូវ state នៃ Hooks រវាង ការហៅ `useState` និង `useEffect` ច្រើន។ (ប្រសិនបើអ្នកចង់ដឹង, យើងនឹងពន្យល់រឿងនេះឱ្យកាន់តែស៊ីជម្រៅ [ខាងក្រោម](#explanation)។)

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

As we [learned earlier](/docs/hooks-state.html#tip-using-multiple-state-variables), we can use multiple State or Effect Hooks in a single component:

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

So how does React know which state corresponds to which `useState` call? The answer is that **React relies on the order in which Hooks are called**. Our example works because the order of the Hook calls is the same on every render:

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

As long as the order of the Hook calls is the same between renders, React can associate some local state with each of them. But what happens if we put a Hook call (for example, the `persistForm` effect) inside a condition?

```js
  // 🔴 We're breaking the first rule by using a Hook in a condition
  if (name !== '') {
    useEffect(function persistForm() {
      localStorage.setItem('formData', name);
    });
  }
```

The `name !== ''` condition is `true` on the first render, so we run this Hook. However, on the next render the user might clear the form, making the condition `false`. Now that we skip this Hook during rendering, the order of the Hook calls becomes different:

```js
useState('Mary')           // 1. Read the name state variable (argument is ignored)
// useEffect(persistForm)  // 🔴 This Hook was skipped!
useState('Poppins')        // 🔴 2 (but was 3). Fail to read the surname state variable
useEffect(updateTitle)     // 🔴 3 (but was 4). Fail to replace the effect
```

React wouldn't know what to return for the second `useState` Hook call. React expected that the second Hook call in this component corresponds to the `persistForm` effect, just like during the previous render, but it doesn't anymore. From that point, every next Hook call after the one we skipped would also shift by one, leading to bugs.

**This is why Hooks must be called on the top level of our components.** If we want to run an effect conditionally, we can put that condition *inside* our Hook:

```js
  useEffect(function persistForm() {
    // 👍 We're not breaking the first rule anymore
    if (name !== '') {
      localStorage.setItem('formData', name);
    }
  });
```

**Note that you don't need to worry about this problem if you use the [provided lint rule](https://www.npmjs.com/package/eslint-plugin-react-hooks).** But now you also know *why* Hooks work this way, and which issues the rule is preventing.

## Next Steps {#next-steps}

ទីបំផុត, យើងត្រៀមខ្លួនដើម្បីរៀនពី [ការសរសេរ Hooks ផ្ទាល់ខ្លួនរបស់អ្នក](/docs/hooks-custom.html)! Custom Hooks អនុញ្ញាតឱ្យអ្នក combine Hooks ដែលផ្តល់ដោយ React ទៅក្នុង abstractions ផ្ទាល់ខ្លួនរបស់អ្នក, ហើយនិងប្រើឡើងវិញ (reuse) stateful logic ទូទៅ រវាង components ផ្សេងៗ។
