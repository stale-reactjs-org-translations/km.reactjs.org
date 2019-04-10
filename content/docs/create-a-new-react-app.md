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

[Create React App](https://github.com/facebookincubator/create-react-app) is a comfortable environment for **learning React**, and is the best way to start building **a new [single-page](/docs/glossary.html#single-page-application) application** in React.

It sets up your development environment so that you can use the latest JavaScript features, provides a nice developer experience, and optimizes your app for production. You’ll need to have Node >= 6 and npm >= 5.2 on your machine. To create a project, run:

```bash
npx create-react-app my-app
cd my-app
npm start
```

>Note
>
>`npx` on the first line is not a typo -- it's a [package runner tool that comes with npm 5.2+](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b).

Create React App doesn't handle backend logic or databases; it just creates a frontend build pipeline, so you can use it with any backend you want. Under the hood, it uses [Babel](https://babeljs.io/) and [webpack](https://webpack.js.org/), but you don't need to know anything about them.

When you're ready to deploy to production, running `npm run build` will create an optimized build of your app in the `build` folder. You can learn more about Create React App [from its README](https://github.com/facebookincubator/create-react-app#create-react-app-) and the [User Guide](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#table-of-contents).

### Next.js {#nextjs}

[Next.js](https://nextjs.org/) គឺជា framework ដែលស្រាលហើយនិងពេញនិយមមួយសម្រាប់ **static និង server‑rendered applications** បង្កើតជាមួយ React។ វារួមបញ្ចូលទាំង **styling និង routing solutions** out of the box, ហើយសន្មត់ថាអ្នកកំពុងប្រើ [Node.js](https://nodejs.org/) ជា server environment។

រៀន Next.js ពី [ឯកសារណែនាំផ្លូវការរបស់វា](https://nextjs.org/learn/)។

### Gatsby {#gatsby}

[Gatsby](https://www.gatsbyjs.org/) គឺជាវិធីដ៏ល្អបំផុតក្នុងការបង្កើត **static websites** ជាមួយ React។ វាអនុញ្ញាតឱ្យអ្នកប្រើ React components, ប៉ុន្ត HTMl និង CSS ត្រូវបានបង្ហាញមុនដើម្បីធានាថាពេលវេលា load មានល្បឿនលឿនបំផុត។

រៀន Gatsby ពី [ឯកសារណែនាំផ្លូវការរបស់វា](https://www.gatsbyjs.org/docs/) និង [gallery of starter kits](https://www.gatsbyjs.org/docs/gatsby-starters/)។

### ឧបករណ៍មានប្រសិទ្ធភាព (Toolchains) ដែលអាចបត់បែនបានកាន់តែច្រើន (Flexible) {#more-flexible-toolchains}

ឧបករណ៍មានប្រសិទ្ធភាព (toolchains) ខាងក្រោមនេះ ផ្តល់នូវភាពបត់បែន (flexiblity) និងជម្រើសកាន់តែច្រើន។ We recommend them to more experienced users:

- **[Neutrino](https://neutrinojs.org/)** combines the power of [webpack](https://webpack.js.org/) with the simplicity of presets, and includes a preset for [React apps](https://neutrinojs.org/packages/react/) and [React components](https://neutrinojs.org/packages/react-components/).

- **[nwb](https://github.com/insin/nwb)** is particularly great for [publishing React components for npm](https://github.com/insin/nwb/blob/master/docs/guides/ReactComponents.md#developing-react-components-and-libraries-with-nwb). It [can be used](https://github.com/insin/nwb/blob/master/docs/guides/ReactApps.md#developing-react-apps-with-nwb) for creating React apps, too. 

- **[Parcel](https://parceljs.org/)** is a fast, zero configuration web application bundler that [works with React](https://parceljs.org/recipes.html#react).

- **[Razzle](https://github.com/jaredpalmer/razzle)** is a server-rendering framework that doesn't require any configuration, but offers more flexibility than Next.js.

## ការបង្កើតឧបករណ៍មានប្រសិទ្ធភាព    (Toolchain) មួយពីទទេ {#creating-a-toolchain-from-scratch}

ឧបករណ៍មានប្រសិទ្ធភាពមួយរបស់ JavaScript ជាធម្មតាមាន៖

* **package manager** មួយ, ដូចជា [Yarn](https://yarnpkg.com/) ឬ [npm](https://www.npmjs.com/)។ វាអនុញ្ញាតឱ្យអ្នកទាញយកគុណប្រយោជន៍ពី ecosystem ដ៏ធំនៃ third-party packages ហើយនិងងាយស្រួលដំឡើងឬធ្វើឱ្យវាទាន់សម័យ។

* **bundler** មួយ, ដូចជា [webpack](https://webpack.js.org/) or [Parcel](https://parceljs.org/)។ វាអនុញ្ញាតឱ្យអ្នកសរសេរ modular កូដហើយនិង bundle វាជាមួយគ្នាទៅជា packages តូចមួយដើម្បីបង្កើនប្រសិទ្ធភាពក្នុងការ load time។

* **compiler** មួយ, ដូចជា [Babel](https://babeljs.io/). វាអនុញ្ញាតឱ្យអ្នកសរសេរ JavaScript កូដដែលទំនើបដែលនៅតែដំណើរការនៅក្នុង browsers ចាស់ៗ។

ប្រសិនបើអ្នកចង់រៀបចំដំឡើងឧបករណ៍មានប្រសិទ្ធភាព (JavaScript toolchain) របស់អ្នកពីទទេ [សូមពិនិត្យមើលការណែនាំនេះ](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658) ដែលនឹងបង្កើតឡើងវិញនូវ functionality មួយចំនួនរបស់ Create React App។

កុំភ្លេចធានាថាឧបករណ៍មានប្រសិទ្ធភាព (custom toolchain) ផ្ទាល់ខ្លួនរបស់អ្នក [ត្រូវបានដំឡើងយ៉ាងត្រឹមត្រូវសម្រាប់ production](/docs/optimizing-performance.html#use-the-production-build)។
