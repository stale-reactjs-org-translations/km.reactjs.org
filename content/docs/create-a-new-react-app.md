---
id: create-a-new-react-app
title: Create a New React App
permalink: docs/create-a-new-react-app.html
redirect_from:
  - "docs/add-react-to-a-new-app.html"
prev: add-react-to-a-website.html
next: cdn-links.html
---

ប្រើចង្កោមឧបករណ៍ដែលបានរួមបញ្ចូលគ្នា (integrated toolchain) សម្រាប់អ្នកប្រើប្រាស់ (user) ដ៏ល្អបំផុត ហើយនិងសម្រាប់បទពិសោធរបស់ developer។

ទំព័រនេះពិពណ៌នាឧបករណ៍មានប្រសិទ្ធភាព (toolchains) មួយចំនួនដែលពេញនិយមដែលជួយក្នុងការងារដូចជា៖

* Scaling to many files and components.
* Using third-party libraries from npm.
* Detecting common mistakes early.
* Live-editing CSS and JS in development.
* Optimizing the output for production.

ឧបករណ៍មានប្រសិទ្ធភាព (toolchains) ដែលត្រូវានណែនាំនៅលើទំព័រនេះ **មិនទាមទារការ configuration ដើម្បីចាប់ផ្តើមទេ**។

## អ្នកប្រហែលមិនត្រូវការឧបករណ៍មានប្រសិទ្ធភាព (Toolchain) ទេ {#you-might-not-need-a-toolchain}

ប្រសិនបើអ្នកមិនជួបប្រទះបញ្ហាដែលបានពិពណ៌នាខាងលើ ឬក៏មិនមានអារម្មណ៍ថាស្រួល (comfortable) ក្នុងការប្រើឧបករណ៍មានប្រសិទ្ធភាព (tools) របស់ JavaScript នៅឡើយទេ សូមពិចារណា [ការបន្ថែម React ជា plain `<script>` tag នៅលើ ទំព័រ HTML](/docs/add-react-to-a-website.html), 
ស្រេចចិត្ត (optionally) [ជាមួយ JSX](/docs/add-react-to-a-website.html#optional-try-react-with-jsx)។

នេះគឺជា **វិធីងាយស្រួលបំផុតដើម្បីបញ្ចូល React ទៅក្នុងវេបសាយដែលមានស្រាប់។** អ្នកអាចបន្ថែមឧបករណ៍មានប្រសិទ្ធភាពដែលមានទំហំធំប្រសិនបើអ្នករកឃើញថាវាមានប្រយោជន៍!

## ឧបករណ៍មានប្រសិទ្ធភាព   (Toolchains) ដែលបានណែនាំ  {#recommended-toolchains}

ក្រុម React ជាបឋមសូមផ្តល់ដំបូន្មាននូវដំណេាះស្រាយដូចនេះ៖

- ប្រសិនបើអ្នក **កំពុងតែរៀន  React** ឬ **កំពុងបង្កើត  [single-page](/docs/glossary.html#single-page-application) app ថ្មីមួយ** អ្នកអាចប្រើ [Create React App](#create-react-app)។
- ប្រសិនបើអ្នកកំពុងតែបង្កើត **គេហទំព័រ  server-rendered ជាមួយ Node.js** អ្នកអាចសាកល្បង [Next.js](#nextjs)។
- ប្រសិនបើអ្នកកំពុងតែបង្កើត **static content-oriented website** អ្នកអាចសាកល្បង [Gatsby](#gatsby)។
- ប្រសិនបើអ្នកកំពុងតែបង្កើត **component library** ឬ **integrating with an existing codebase** អ្នកអាចសាកល្បង [More Flexible Toolchains](#more-flexible-toolchains)។

### Create React App {#create-react-app}

[Create React App](https://github.com/facebookincubator/create-react-app) គឺជា environment ដែលផ្តល់ភាពសុខស្រួល (comfortable) មួយសម្រាប់ **ការរៀន React** ហើយគឺជាវិធីដ៏ល្អបំផុតដើម្បីចាប់ផ្តើមបង្កើត **[single-page](/docs/glossary.html#single-page-application) application ថ្មីមួយ** នៅក្នុង​ React។

<<<<<<< HEAD
វាបង្កើត (sets up)នូវ development environment របស់អ្នកដូច្នេះអ្នកអាចប្រើលក្ខណៈពិសេសចុងក្រោយបំផុតរបស់ JavaScript (latest JavaScript features), ផ្តល់ developer នូវបទពិសោធដ៏អស្ចារ្យបំផុត, ហើយនិងបង្កើនប្រសិទ្ធភាព app របស់អ្នកសម្រាប់ production។ អ្នកនឹងត្រូវមាន Node >= ៨.១០ និង npm >= ៥.៦ នៅលើម៉ាស៊ីនរបស់អ្នក។ ដើម្បីបង្កើត product, run៖
=======
It sets up your development environment so that you can use the latest JavaScript features, provides a nice developer experience, and optimizes your app for production. You’ll need to have [Node >= 14.0.0 and npm >= 5.6](https://nodejs.org/en/) on your machine. To create a project, run:
>>>>>>> 3bba430b5959c2263c73f0d05d46e2c99c972b1c

```bash
npx create-react-app my-app
cd my-app
npm start
```

>ចំណាំ
>
>`npx` នៅលើបន្ទាត់ទីមួយគឺមិនមែនជា typo ទេ -- វាគឺជា [package runner tool ដែលភ្ជាប់មកជាមួយ npm 5.2+](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b)។

Create React App មិនដោះស្រាយ​ (doesn't handle) នូវ backend logic ឬ databases នេាះទេ; វាគ្រាន់តែបង្កើតនូវ frontend build pipeline មួយ ដូចច្នេះអ្នកអាចវាជាមួយ backend ផ្សេងៗដែលអ្នកចូលចិត្ត។ បច្ចេកទេសខាងក្រោយ, វាប្រើ [Babel](https://babeljs.io/) និង [webpack](https://webpack.js.org/) ប៉ុន្តែអ្នកមិនចាំបាច់ដឹងអ្វីអំពីពួកវាទេ។

នៅពេលអ្នកត្រៀមខ្លួនរួចរាល់ហើយដើម្បី deploy ទៅកាន់ production, running `npm run build` និងបង្កើត optimized build មួយសម្រាប់ app របស់អ្នកនៅក្នុងថតឯកសារ `build`។ អ្នកអាចស្វែងយល់បន្ថែមអំពី Create React App [ពី README របស់វា](https://github.com/facebookincubator/create-react-app#create-react-app-) និង [ការណែនាំសម្រាប់អ្នកប្រើប្រាស់](https://facebook.github.io/create-react-app/)។

### Next.js {#nextjs}

[Next.js](https://nextjs.org/) គឺជា framework ដែលស្រាលហើយនិងពេញនិយមមួយសម្រាប់ **static និង server‑rendered applications** បង្កើតជាមួយ React។ វារួមបញ្ចូលទាំង **styling និង routing solutions** out of the box, ហើយសន្មត់ថាអ្នកកំពុងប្រើ [Node.js](https://nodejs.org/) ជា server environment។

រៀន Next.js ពី [ឯកសារណែនាំផ្លូវការរបស់វា](https://nextjs.org/learn/)។

### Gatsby {#gatsby}

[Gatsby](https://www.gatsbyjs.org/) គឺជាវិធីដ៏ល្អបំផុតក្នុងការបង្កើត **static websites** ជាមួយ React។ វាអនុញ្ញាតឱ្យអ្នកប្រើ React components, ប៉ុន្ត HTMl និង CSS ត្រូវបានបង្ហាញមុនដើម្បីធានាថាពេលវេលា load មានល្បឿនលឿនបំផុត។

រៀន Gatsby ពី [ឯកសារណែនាំផ្លូវការរបស់វា](https://www.gatsbyjs.org/docs/) និង [gallery of starter kits](https://www.gatsbyjs.org/docs/gatsby-starters/)។

### ឧបករណ៍មានប្រសិទ្ធភាព (Toolchains) ដែលអាចបត់បែនបានកាន់តែច្រើន (Flexible) {#more-flexible-toolchains}

ឧបករណ៍មានប្រសិទ្ធភាព (toolchains) ខាងក្រោមនេះ ផ្តល់នូវភាពបត់បែន (flexiblity) និងជម្រើសកាន់តែច្រើន។ យើងសូមណែនាំពួកវាទៅកាន់អ្នកប្រើប្រាស់ (user) ដែលមានបទពិសោធន៍ច្រើន៖

- **[Neutrino](https://neutrinojs.org/)** រួមបញ្ចូលគ្នានូវអំណាច (power) នៃ [webpack](https://webpack.js.org/) ជាមួយភាពសាមញ្ញនៃ presets ហើយនិងរួមបញ្ចូលទាំង preset សម្រាប់ [React apps](https://neutrinojs.org/packages/react/) និង [React components](https://neutrinojs.org/packages/react-components/)។

<<<<<<< HEAD
- **[nwb](https://github.com/insin/nwb)** គឺអស្ចារ្យណាស់សម្រាប់ [ការ publishing React components សម្រាប់ npm](https://github.com/insin/nwb/blob/master/docs/guides/ReactComponents.md#developing-react-components-and-libraries-with-nwb)។ វា [អាចត្រូវបានប្រើ](https://github.com/insin/nwb/blob/master/docs/guides/ReactApps.md#developing-react-apps-with-nwb) សម្រាប់បង្កើត React apps ផងដែរ។
=======
- **[Nx](https://nx.dev/react)** is a toolkit for full-stack monorepo development, with built-in support for React, Next.js, [Express](https://expressjs.com/), and more.

- **[Parcel](https://parceljs.org/)** is a fast, zero configuration web application bundler that [works with React](https://parceljs.org/recipes/react/).
>>>>>>> 3bba430b5959c2263c73f0d05d46e2c99c972b1c

- **[Parcel](https://parceljs.org/)** គឺលឿនណាស់, គឺជា zero configuration web application bundler ដែល [ធ្វើការជាមួយ React](https://parceljs.org/recipes.html#react)។

- **[Razzle](https://github.com/jaredpalmer/razzle)** គឺជា server-rendering framework មួយដែលមិនទាមទារនូវការ​ configuration ច្រើនប៉ុន្តែផ្តល់នូវភាពបត់បែន (flexibility) ច្រើនជាង Next.js។

## ការបង្កើតឧបករណ៍មានប្រសិទ្ធភាព (Toolchain) មួយពីទទេ {#creating-a-toolchain-from-scratch}

ឧបករណ៍មានប្រសិទ្ធភាពមួយរបស់ JavaScript ជាធម្មតាមាន៖

* **package manager** មួយ, ដូចជា [Yarn](https://yarnpkg.com/) ឬ [npm](https://www.npmjs.com/)។ វាអនុញ្ញាតឱ្យអ្នកទាញយកគុណប្រយោជន៍ពី ecosystem ដ៏ធំនៃ third-party packages ហើយនិងងាយស្រួលដំឡើងឬធ្វើឱ្យវាទាន់សម័យ។

* **bundler** មួយ, ដូចជា [webpack](https://webpack.js.org/) or [Parcel](https://parceljs.org/)។ វាអនុញ្ញាតឱ្យអ្នកសរសេរ modular កូដហើយនិង bundle វាជាមួយគ្នាទៅជា packages តូចមួយដើម្បីបង្កើនប្រសិទ្ធភាពក្នុងការ load time។

* **compiler** មួយ, ដូចជា [Babel](https://babeljs.io/). វាអនុញ្ញាតឱ្យអ្នកសរសេរ JavaScript កូដដែលទំនើបដែលនៅតែដំណើរការនៅក្នុង browsers ចាស់ៗ។

ប្រសិនបើអ្នកចង់រៀបចំដំឡើងឧបករណ៍មានប្រសិទ្ធភាព (JavaScript toolchain) របស់អ្នកពីទទេ [សូមពិនិត្យមើលការណែនាំនេះ](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658) ដែលនឹងបង្កើតឡើងវិញនូវ functionality មួយចំនួនរបស់ Create React App។

កុំភ្លេចធានាថាឧបករណ៍មានប្រសិទ្ធភាព (custom toolchain) ផ្ទាល់ខ្លួនរបស់អ្នក [ត្រូវបានដំឡើងយ៉ាងត្រឹមត្រូវសម្រាប់ production](/docs/optimizing-performance.html#use-the-production-build)។
