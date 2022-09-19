---
id: add-react-to-a-website
title: Add React to a Website
permalink: docs/add-react-to-a-website.html
redirect_from:
  - "docs/add-react-to-an-existing-app.html"
prev: getting-started.html
next: create-a-new-react-app.html
---

ប្រើ React តិចឬក៏ច្រើនតាមតែអ្នកត្រូវការ។

React មត្រូវបានរចនាឡើងពីការចាប់ផ្តើមប្រើបន្តិចម្តងៗ ហើយ **អ្នកអាចប្រើ React តិចឬក៏ច្រើនតាមតែអ្នកត្រូវការ**។ ប្រហែលជាអ្នកគ្រាន់តែចង់បន្ថែម "ផ្នកែតូចមួយនៃ User Interface" ទៅលើ page ដែលមានស្រាប់។ React components គឺជាវិធីដ៏ល្អមួយដើម្បីធ្វើដូចនោះ។

គេហទំព័រភាគច្រើនមិនមែន, ហើយនិងមិនចាំបាច់ត្រូវតែជា single-page apps។ ជាមួយ **បន្ទាត់មួយចំនួននៃកូដនិងគ្មានឧបករណ៍ស្ថាបនា (no build tooling)** សាកល្បង React នៅក្នុងផ្នែកតូចមួយនៃគេហទំព័ររបស់អ្នក។ អ្នកអាចពង្រីកវត្តមានរបស់វា (React) ជាបណ្តើរ ឬក៏រក្សាវានៅក្នុង dynamic widgets មួយចំនួន។

---

- [Add React in One Minute](#add-react-in-one-minute)
- [Optional: Try React with JSX](#optional-try-react-with-jsx) (no bundler necessary!)

## Add React in One Minute {#add-react-in-one-minute}

នៅក្នុងផ្នែកនេះ យើងនឹងបង្ហាញអ្នកពីរបៀបបន្ថែម React component ទៅក្នុង HTML page ដែលមានស្រាប់។ អ្នកអាចអនុវត្តជាមួយនិងគេហទំព័រផ្ទាល់ខ្លួនរបស់អ្នក ឬក៏បង្កើត HTML file ដែលទទេមួយដើម្បីអនុវត្ត។

វានឹងមិនមានឧបករណ៍ស្មុគស្មាញឬក៏ការតម្រូវអោយតំឡើង -- **ដើម្បីបំពេញផ្នែកនេះ អ្នកត្រូវការតែការតភ្ជាប់អ៊ីធឺណិតប៉ុណ្ណោះ ហើយនិងពេលវេលារបស់អ្នករយៈពេល១នាទី។**

<<<<<<< HEAD
Optional: [ទាញយកឧទាហរណ៍ពេញលេញ (2KB zipped)](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605/archive/f6c882b6ae18bde42dcf6fdb751aae93495a2275.zip)
=======
Optional: [Download the full example (2KB zipped)](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605/archive/87f0b6f34238595b44308acfb86df6ea43669c08.zip)
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

### Step 1: Add a DOM Container to the HTML {#step-1-add-a-dom-container-to-the-html}

ដំបូង បើក HTML page ដែលអ្នកចង់កែសម្រួល។ បន្ថែម `<div>` tag ទទេមួយដើម្បីសម្គាល់ទីកន្លែងដែលអ្នកចង់បង្ហាញអ្វីមួយជាមួយ React។ ឧទាហរណ៍​៖

```html{3}
<!-- ... existing HTML ... -->

<div id="like_button_container"></div>

<!-- ... existing HTML ... -->
```

យើងបានផ្ដល់ឱ្យ `<div>` នូវ unique `id` HTML attribute មួយ។ នេះនឹងអនុញ្ញាតឱ្យយើងរកវាឃើញដោយប្រើ JavaScript កូដនៅពេលក្រោយ ហើយនិងបង្ហាញ React component នៅខាងក្នុងវា (`<div>`)។

>ព័ត៌មានជំនួយ
>
>អ្នកអាចដាក់ "container" `<div>` មួយដូចនេះ **គ្រប់ទីកន្លែង** នៅខាងក្នុង `<body>` tag។ អ្នកប្រហែលមាន DOM containers ឯករាជ្យមួយចំនួននៅលើ page មួយដែលអ្នកត្រូវការ។ ជាទូទៅវាគឺទទេ -- React នឹងជំនួស content ដែលមានស្រាប់ណាមួយនៅខាងក្នុង DOM containers។

### Step 2: Add the Script Tags {#step-2-add-the-script-tags}

បន្ទាប់មកទៀត បន្ថែម `<script>` tags ចំនួនបីទៅកាន់ HTML page មុនការបិទ `</body>` tag៖

```html{5,6,9}
  <!-- ... other HTML ... -->

  <!-- Load React. -->
  <!-- Note: when deploying, replace "development.js" with "production.min.js". -->
  <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>

  <!-- Load our React component. -->
  <script src="like_button.js"></script>

</body>
```

ពីរ tags តំបូង load React។ tag ទីបី load component កូដរបស់អ្នក។

### Step 3: Create a React Component {#step-3-create-a-react-component}

បង្កើត file មួយហៅថា `like_button.js` ជាប់និង HTML page របស់អ្នក។

បើក **[this starter code](https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js)** ហើយ paste វាចូលក្នុង file ដែលអ្នកបានបង្កើត។

>ពត៌មានជំនួយ
>
>កូដនេះកំណត់ React component ហៅថា `LikeButton`។ កុំបារម្ភប្រសិនបើអ្នកមិនទាន់យល់វានៅឡើយ -- យើងនឹង cover ពីការបង្កើត blocks នៃ React នៅពេលក្រោយនៅក្នុង [hands-on tutorial](/tutorial/tutorial.html) និង [main concepts guide](/docs/hello-world.html)។ សម្រាប់ពេល​ឥលូវ​នេះ តោះយើងគ្រាន់តែបង្ហាញវានៅលើអេក្រង់!

<<<<<<< HEAD
បន្ទាប់ **[the starter code](https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js)**, បន្ថែមពីរបន្ទាត់នៅក្រោមបាតនៃ `like_button.js`៖
=======
After **[the starter code](https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js)**, add three lines to the bottom of `like_button.js`:
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

```js{3,4,5}
// ... the starter code you pasted ...

const domContainer = document.querySelector('#like_button_container');
const root = ReactDOM.createRoot(domContainer);
root.render(e(LikeButton));
```

<<<<<<< HEAD
ពីរបន្ទាត់នៃកូដនេះគឺថាការស្វែងរក `<div>` ដែលយើងបានបន្ថែមទៅកាន់ HTML នៅក្នុងជំហ៊ានដំបូងរបស់យើង ហើយបន្ទាប់មកបង្ហាញ "Like" ប៊ូតុង React component របស់យើងនៅខាងក្នុងវា។
=======
These three lines of code find the `<div>` we added to our HTML in the first step, create a React app with it, and then display our "Like" button React component inside of it.
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

### That's It! {#thats-it}

អត់មានជំហ៊ានទីបួនទេ។ **អ្នកទើបតែបានបន្ថែម React component ដំបូងទៅកាន់គេហទំព័រ​របស់​អ្នក។**

ពិនិត្យមើលផ្នែកបន្ទាប់ដើម្បីទទួលបានគន្លឹះបន្ថែមទៀតស្តីពីការ integrate React។

**[មើល source កូដរបស់ឧទាហរណ៍ពេញលេញ](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605)**

<<<<<<< HEAD
**[ទាញយកឧទាហរណ៍ពេញលេញ (2KB zipped)](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605/archive/f6c882b6ae18bde42dcf6fdb751aae93495a2275.zip)**
=======
**[Download the full example (2KB zipped)](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605/archive/87f0b6f34238595b44308acfb86df6ea43669c08.zip)**
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

### Tip: Reuse a Component {#tip-reuse-a-component}

ជាទូទៅ អ្នក​ប្រហែលជាចង់បង្ហាញ React components នៅកន្លែងច្រើននៅលើ HTML page។ នេះគឺជាឧទាហរណ៍ដែលបង្ហាញ "Like" ប៊ូតុងបីដង ហើយនិង​បេាះទិន្នន័យមួយចំនួនទៅអោយវា។

[មើល source កូដរបស់ឧទាហរណ៍ពេញលេញ](https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda)

<<<<<<< HEAD
[ទាញយកឧទាហរណ៍ពេញលេញ (2KB zipped)](https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda/archive/9d0dd0ee941fea05fd1357502e5aa348abb84c12.zip)
=======
[Download the full example (2KB zipped)](https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda/archive/279839cb9891bd41802ebebc5365e9dec08eeb9f.zip)
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

>ចំណាំ
>
>យុទ្ធសាស្ត្រនេះគឺមានប្រយោជន៍បំផុត នៅខណៈពេល page នៃផ្នែល React-powered ត្រូវបានដាក់ដាច់ឆ្ងាយពីគ្នា ។ នៅក្នុង React កូដ វាគឺងាយស្រួលជាងក្នុងការប្រើ [component composition](/docs/components-and-props.html#composing-components) ជំនួសវិញ។

### Tip: Minify JavaScript for Production {#tip-minify-javascript-for-production}

មុនពេល deploy គេហទំព័រ​របស់​អ្នកទៅកាន់ production ត្រូវចាំថា unminified JavaScript អាចធ្វើអោយ page ដើរយឺតយ៉ាងខ្លាំងសម្រាប់អ្នកប្រើរបស់អ្នក។

ប្រសិនបើអ្នក minify scripts របស់ application រួចហើយ, **គេហទំព័រ​របស់​អ្នកនឹងរួចរាល់សម្រាប់ production** ប្រសិនបើអ្នកធានាថាបាន deploy HTML ដោយ loads versions របស់ React នៅចុងបញ្ចប់នៅក្នុង `production.min.js`៖

```js
<script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
```

ប្រសិនបើអ្នកមិនមានជំហ៊ាន minification សម្រាប់ scripts របស់អ្នក [នេះជាវិធីមួយដើម្បីបង្កើតវាឡើង](https://gist.github.com/gaearon/42a2ffa41b8319948f9be4076286e1f3)។

## Optional: Try React with JSX {#optional-try-react-with-jsx}

<<<<<<< HEAD
នៅក្នុងឧទាហរណ៍ខាងលើ យើងគ្រាន់តែពឹងផ្អែកលើលក្ខណៈពិសេសដែលបាន support ដោយ browsers។​ នេះ​ជាហេតុដែលយើងបានប្រើ Javascript function call ដើម្បីប្រាប់ទៅ React នូវអ្វីដែលត្រូវបង្ហាញ៖
=======
In the examples above, we only relied on features that are natively supported by browsers. This is why we used a JavaScript function call to tell React what to display:
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

```js
const e = React.createElement;

// Display a "Like" <button>
return e(
  'button',
  { onClick: () => this.setState({ liked: true }) },
  'Like'
);
```

មួយវិញទៀត React ក៏ផ្តល់ជូននូវជម្រើសដើម្បីប្រើ [JSX](/docs/introducing-jsx.html) ជំនួសផងដែរ៖

```js
// Display a "Like" <button>
return (
  <button onClick={() => this.setState({ liked: true })}>
    Like
  </button>
);
```

ទំរង់នៃការសរសេរកូដទាំងពីរខាងលើគឺដូចគ្នា ហើយនិងបង្ហាញលទ្ធផលដូចគ្នា។ ខណៈពេលដែល **JSX គឺ [completely optional](/docs/react-without-jsx.html)** មនុស្សជាច្រើនយល់ថាវាមានប្រយោជន៍សម្រាប់ការសរសេរ UI កូដ​ -- ទាំងជាមួយ React និងជាមួយ libraries ផ្សេងៗ។

<<<<<<< HEAD
អ្នកអាចលេងជាមួយ JSX ដោយប្រើ [this online converter](https://babeljs.io/en/repl#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DwIwrgLhD2B2AEcDCAbAlgYwNYF4DeAFAJTw4B88EAFmgM4B0tAphAMoQCGETBe86WJgBMAXJQBOYJvAC-RGWQBQ8FfAAyaQYuAB6cFDhkgA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.4.3)។
=======
You can play with JSX using [this online converter](https://babeljs.io/en/repl#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DwIwrgLhD2B2AEcDCAbAlgYwNYF4DeAFAJTw4B88EAFmgM4B0tAphAMoQCGETBe86WJgBMAXJQBOYJvAC-RGWQBQ8FfAAyaQYuAB6cFDhkgA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.15.7).
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

### Quickly Try JSX {#quickly-try-jsx}

មធ្យោបាយលឿនបំផុតដើម្បីសាកល្បង JSX ក្នុង project របស់អ្នកគឺបន្ថែម `<script>` tag នេះទៅកាន់ page របស់អ្នក៖

```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

<<<<<<< HEAD
ឥឡូវ​នេះអ្នកអាចប្រើ JSX នៅក្នុង `<script>` tag ណាមួយដោយការបន្ថែមនូវ `type="text/babel"` attribute ទៅកាន់វា។ នេះគឺជា [ឧទាហរណ៍ HTML file ជាមួយ JSX](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html) ដែលអ្នកអាចទាញយកនិងលេងជាមួយវា។
=======
Now you can use JSX in any `<script>` tag by adding `type="text/babel"` attribute to it. Here is [an example HTML file with JSX](https://raw.githubusercontent.com/reactjs/reactjs.org/main/static/html/single-file-example.html) that you can download and play with.
>>>>>>> 841d3d1b75491ce153a53d1887ab020458090bbd

វិធីសាស្រ្តនេះគឺល្អសម្រាប់ការរៀននិងការបង្កើត demos ដែលសាមញ្ញ។ ទោះជាយ៉ាងណាវាធ្វើឱ្យគេហទំព័ររបស់អ្នកយឺត ហើយ **មិនសមរម្យសម្រាប់ production**។ 
នៅពេលអ្នកត្រៀមខ្លួនរួចរាល់ដើម្បីបន្តទៅមុខទៀត, លុប `<script>` tag នេះនិង `type="text/babel"` attributes ដេលអ្នកបានបន្ថេម។ ជំនួសវិញ, នៅផ្នែកបន្ទាប់អ្នកនឹងរៀបចំ JSX preprocessor មួយដើម្បីបម្លែង (convert) `<script>` tags ទាំងអស់របស់អ្នកដោយស្វ័យប្រវត្តិ។

### Add JSX to a Project {#add-jsx-to-a-project}

ការបន្ថែម JSX ទៅកាន់ project មួយមិនទាមទារនូវឧបករណ៍ស្មុគស្មាញ (complicated tools) ដូច bundler ឬក៏ development server នេាះទេ។ សំខាន់, ការបន្ថែម JSX **គឺច្រើនដូចជាការបន្ថែម CSS preprocessor មួយ។** តម្រូវការតែមួយគត់គឺត្រូវមាន [Node.js](https://nodejs.org/) ដែលបានដំឡើងនៅលើកុំព្យូទ័ររបស់អ្នក។

ទៅថតគម្រោងរបស់អ្នកនៅក្នុង terminal ហើយ paste ពីរ commands នេះ៖

1. **ជំហ៊ាន​ ១៖** Run `npm init -y` (ប្រសិនបើវាបរាជ័យ, [នេះគឺជាការជួសជុល](https://gist.github.com/gaearon/246f6380610e262f8a648e3e51cad40d))
2. **ជំហ៊ាន​ ២៖** Run `npm install babel-cli@6 babel-preset-react-app@3`

>ពត៌មានជំនួយ
>
>យើង **កំពុងប្រើ npm នៅទីនេះសម្រាប់តែការដំឡើង JSX preprocessor ប៉ុណ្ណេាះ** អ្នកនឹងមិនត្រូវការវាសម្រាប់អ្វីផ្សេងទេ។ ទាំង react និង application កូដអាចរក្សារជា `<script>` tags ដដែលដោយគ្មានការផ្លាស់ប្តូរ។

Congratulations! You just added a **production-ready JSX setup** to your project.

អបអរសាទរ! អ្នកទើបតែបានបន្ថែមនូវ **production-ready JSX setup** ទៅកាន់ project របស់អ្នក។


### Run JSX Preprocessor {#run-jsx-preprocessor}

បង្កើតថតឯកសារ (folder) ដែលហៅថា `src` ហើយ run terminal command នេះ៖

```console
npx babel --watch src --out-dir . --presets react-app/prod
```

>ចំណាំ
>
>`npx` មិនមែនជា typo ទេ -- វាគឺជា [package runner tool ដែលភ្ជាប់មកជាមួយ npm 5.2+](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b)។
>
>ប្រសិនបើអ្នកឃើញសារ error និយាយថា "You have mistakenly installed the `babel` package", អ្នកប្រហែលជាខកខាន [ជំហានមុន](#add-jsx-to-a-project). ធ្វើវានៅក្នុងថតឯកសារដូចគ្នាដដែល ហើយព្យាយាមម្តងទៀត។

កុំរង់ចាំដល់វាបញ្ចប់ -- command នេះ ចាប់ផ្តើម​ automated watcher សម្រាប់ JSX។

ប្រសិនបើឥឡូវអ្នកបង្កើត file ដែលហៅថា `src/like_button.js` ជាមួយនិង **[JSX starter code](https://gist.github.com/gaearon/c8e112dc74ac44aac4f673f2c39d19d1/raw/09b951c86c1bf1116af741fa4664511f2f179f0a/like_button.js)** នេះ watcher នឹងបង្កើត preprocessed `like_button.js` ជាមួយនិង plain JavaScript កូដដែលសមរម្យឬមួយក៏អាចអោយ browser យល់ឬក៏ run បាន។ 
ពេលអ្នកកែប្រែ source file ជាមួយ JSX, transform នឹង re-run ដោយស្វ័យប្រវត្តិ។

បន្ថែមពីលើនេះ នេះក៏អនុញ្ញាតឱ្យអ្នកប្រើផងដែរនូវ JavaScript syntax features ដូចជា classes ដោយគ្មានការព្រួយបារម្ភអំពីការ breaking browsers ចាស់ៗ។ ឧបករណ៍ (tools) ដែលយើងទើបតែបានប្រើហៅថា Babel ហើយអ្នកអាចរៀនបន្ថែមទៀតពីវានៅក្នុង [ឯកសាររបស់វា](https://babeljs.io/docs/en/babel-cli/)។

ប្រសិនបើអ្នកសង្កេតឃើញថាអ្នកកំពុងតែមានជំនាញឬក៏ចំនេះដឹងជាមួយនិង build tools ហើយនិងចង់អោយវាធ្វើអ្វីច្រើនទៀតសម្រាប់អ្នក [ផ្នែកបន្ទាប់](/docs/create-a-new-react-app.html) ពិពណ៌នាអំពី toolchains ដែលមានប្រជាប្រិយភាពនិងងាយស្រួលប្រើបំផុតមួយចំនួន។ ប្រសិនបើអ្នកមិនចង់ប្រើ toolchains ទេ -- អ្នកអាចប្រើ script tags ទាំងនេាះ!
