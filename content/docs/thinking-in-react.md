---
id: thinking-in-react
title: Thinking in React
permalink: docs/thinking-in-react.html
redirect_from:
  - 'blog/2013/11/05/thinking-in-react.html'
  - 'docs/thinking-in-react-zh-CN.html'
prev: composition-vs-inheritance.html
---

នៅក្នុងគំនិតរបស់ពួកយើង React គឺជាវិធីសំខាន់បំផុតដើម្បីកសាង Web apps ជាមួយ JavaScript ដ៏ធំមួយ។ វាបានគ្រប់គ្រងការងារនិងដំណើរការដែលកំពុងកើនឡើង (scale) បានយ៉ាងល្អសម្រាប់យើងនៅ Facebook និង Instagram។

ផ្នែកមួយនៃផ្នែកដ៏អស្ចារ្យជាច្រើននៃ React គឺរបៀបដែលវាធ្វើឱ្យអ្នកគិតអំពី apps នៅពេលអ្នកបង្កើតពួកវា, នៅក្នុងឯកសារនេះ យើងនឹងនាំអ្នកឆ្លងកាត់ដំណើរការនៃការបង្កើតតារាងទិន្នន័យរបស់ផលិតផលដែលអាច search បានដោយការប្រើ React។

## Start With A Mock {#start-with-a-mock}

ស្រមៃថាយើងមាន JSON API មួយនិង mock មួយសម្រាប់ designer របស់យើងរួចហើយ។ Mock មើលទៅដូចនេះ៖

![Mockup](../images/blog/thinking-in-react-mock.png)

JSON API របស់យើង returns ទិន្នន័យមួយចំនួនដែលមើលទៅដូចនេះ៖

```
[
  {category: "Sporting Goods", price: "$49.99", stocked: true, name: "Football"},
  {category: "Sporting Goods", price: "$9.99", stocked: true, name: "Baseball"},
  {category: "Sporting Goods", price: "$29.99", stocked: false, name: "Basketball"},
  {category: "Electronics", price: "$99.99", stocked: true, name: "iPod Touch"},
  {category: "Electronics", price: "$399.99", stocked: false, name: "iPhone 5"},
  {category: "Electronics", price: "$199.99", stocked: true, name: "Nexus 7"}
];
```

## Step 1: Break The UI Into A Component Hierarchy {#step-1-break-the-ui-into-a-component-hierarchy}

រឿងដំបូងដែលអ្នកនឹងចង់ធ្វើគឺគូសប្រអប់នៅជុំវិញ component ទាំងអស់ (និង subcomponent) នៅក្នុង mock និងដាក់ឈ្មោះឱ្យពួកវា។ ប្រសិនបើអ្នកកំពុងតែធ្វើការជាមួយ designer ពួកគេប្រហែលជាបានធ្វើរួចហើយ ដូច្នេះសូមទៅនិយាយជាមួយពួកគេ! ឈ្មោះ Photoshop layer របស់ពួកគេអាចនឹងក្លាយជាឈ្មោះនៃ React components របស់អ្នក!

ប៉ុន្ដែតើអ្នកដឹងដោយរបៀបណាអ្វីដែលជា component របស់វាផ្ទាល់? គ្រាន់តែប្រើបច្ចេកទេសដូចគ្នាដើម្បីសម្រេចចិត្តថាអ្នកគួរតែបង្កើត function ឬក៏ object ថ្មីមួយ។ ដែលបច្ចេកទេសបែបនេាះគឺ [single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle), component មួយគួរតែធ្វើរឿងតែមួយគត់។ ប្រសិនបើវាបន្តរីកធំទៅៗ វាគួរតែត្រូវបានគេបំបែកទៅជា subcomponents តូចៗ។

ដែលអ្នកតែងតែបង្ហាញ JSON data model ទៅអោយអ្នកប្រើប្រាស់, អ្នកនឹងរកឃើញថាប្រសិនបើ model របស់អ្នកត្រូវបានបង្កើតឡើងដោយត្រឹមត្រូវ, UI របស់អ្នក (ហើយនិងរចនាសម្ព័ន្ធ component របស់អ្នក) នឹង map បានយ៉ាងល្អ។ នោះពីព្រេាះតែ UI និង data models មាននិន្នាការប្រកាន់ខ្ជាប់នូវ *ស្ថាបត្យកម្មព័ត៌មាន* ដូចគ្នា។ គ្រាន់តែបំបែកវាជា components ដែលតំណាងឱ្យបំណែកមួយជាក់លាក់នៃ data model របស់អ្នក។ ការបំបែក UI របស់អ្នកទៅជា components, ដែល component នីមួយៗ ត្រូវនឹងផ្នែកមួយនៃគំរូទិន្នន័យរបស់អ្នក។

![Diagram showing nesting of components](../images/blog/thinking-in-react-components.png)

<<<<<<< HEAD
អ្នកនឹងឃើញនៅទីនេះថាយើងមាន៥ components នៅក្នុង app ដ៏សាមញ្ញរបស់យើង។ ដែលទិន្នន័យតំណាងដោយ component នីមួយៗ។
=======
You'll see here that we have five components in our app. We've italicized the data each component represents. The numbers in the image correspond to the numbers below.
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

  1. **`FilterableProductTable` (orange):** មានឧទាហរណ៍ទាំងមូល
  2. **`SearchBar` (blue):** ទទួលការ *input របស់អ្នកប្រើប្រាស់* ទាំងអស់
  3. **`ProductTable` (green):** បង្ហាញនិងច្រេាះយក *បណ្តុំ data* ដោយផ្អែកលើ *ការ input របស់អ្នកប្រើប្រាស់*
  4. **`ProductCategoryRow` (turquoise):** បង្ហាញ heading សម្រាប់ *category* នីមួយៗ
  5. **`ProductRow` (red):** បង្ហាញជួរដេកសម្រាប់ *ផលិតផល* នីមួយៗ

ប្រសិនបើអ្នកក្រឡេកមើល `ProductTable` អ្នកនឹងឃើញថា header របស់តារាង (មានស្លាក "Name" និង "Price") គឺមិនមែនជា component របស់វាផ្ទាល់ទេ។ នេះជាបញ្ហាចំណង់ចំណូលចិត្ត, ហើយមាន argument មួយត្រូវបានបង្កើតឡើងតាមវិធីផ្សេង។ 
សម្រាប់ឧទាហរណ៍នេះ, យើងទុកវាជាផ្នែកមួយ `ProductTable` ពីព្រេាះវាជាផ្នែកមួយនៃការ render *បណ្តុំ data* ដែលជាការ responsibility របស់ `ProductTable`។ ទោះយ៉ាងណា, ប្រសិនបើ header នេះកាន់តែធំទៅៗទៅជាស្មុគស្មាញ (i.e. ប្រសិនបើយើងចង់បន្ថែម sorting feature), វាពិតជាគំណិតត្រឹមត្រូវក្នុងការបង្កើត `ProductTableHeader` component សម្រាប់ `ProductTable`។

ឥឡូវនេះយើងបានកំណត់ components នៅក្នុង mock របស់យើងរួចរាល់ហើយ, តេាះរៀបចំពួកវាទៅជារចនាសម្ព័ន្ធ (hierarchy)។ នេះគឺងាយស្រួល។ Components ដែលនៅក្នុង component ផ្សេងនៅក្នុង mock គួរតែជា child នៅក្នុង រចនាសម្ព័ន្ធ (hierarchy)៖

  * `FilterableProductTable`
    * `SearchBar`
    * `ProductTable`
      * `ProductCategoryRow`
      * `ProductRow`

## Step 2: Build A Static Version in React {#step-2-build-a-static-version-in-react}

<p data-height="600" data-theme-id="0" data-slug-hash="BwWzwm" data-default-tab="js" data-user="lacker" data-embed-version="2" class="codepen">សូមមើល Pen <a href="https://codepen.io/gaearon/pen/BwWzwm">Thinking In React: Step 2</a> នៅលើ <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

ឥឡូវ​នេះអ្នកមានរចនាសម្ព័ន្ធ component របស់អ្នក, វាដល់ពេលដែលត្រូវ implement app របស់អ្នក។ វិធីងាយស្រួលបំផុតគឺត្រូវបង្កើត version មួយដែលទទួលយក data model របស់អ្នកហើយ render UI បន្តែមិនមាន interactivity ទេ។ វាជាការល្អបំផុតក្នុងការបំបែកដំណើរការទាំងនេះ ពីព្រេាះការបង្កើត static version មួយតម្រូវឱ្យមានការ typing ច្រើននិងមិនមានការគិតទាល់តែសេាះ, ហើយការបន្ថែម interactivity តម្រូវឱ្យមានការគិតច្រើននិងមិនមបានការ typing ច្រើន។ យើងនឹងឃើញថាហេតុអ្វី។

ដើម្បីបង្កើត static version មួយនៃ app របស់អ្នកដែល render data model របស់អ្នក, អ្នកនឹងចង់បង្កើត components ដែលប្រើឡើងវិញ (reuse) នូវ component ផ្សេងហើយបេាះ (pass) data ដោយការប្រើ *props*។ *props* គឺជាមធ្យោបាយមួយក្នុងការបេាះ data ពី parent ទៅកាន់ child។ ប្រសិនបើអ្នកធ្លាប់ស្គាល់ concept នៃ *state*, **កុំប្រើ state ទាំងស្រុង** ដើម្បីបង្កើត static version នេះអី។ State ត្រូវបានប្រើសម្រាប់តែ interactivity, ហើយនិង data ដែលផ្លាស់ប្តូរតាមពេលវេលា។ នេះគឺជា static version នៃ app, ដូច្នេះអ្នកមិនត្រូវការវាទេ។

អ្នកអាចបង្កើតជាលក្ខណះ top-down ឬ bottom-up។ អ្នកអាចចាប់ផ្តើមបង្កើត component higher up នៅក្នុងរចនាសម្ព័ន្ធ (hierarchy) (ឧទាហរណ៍ ការចាប់ផ្តើមជាមួយ `FilterableProductTable`) ឬក៏ជាមួយ component ដែលនៅក្នុងវា (`ProductRow`)។ នៅក្នុងឧទាហរណ៏សាមញ្ញ 
វាជាធម្មតាងាយស្រួលក្នុងការប្រើ top-down សម្រាប់ products ធំៗ, ហើយវាកាន់តែងាយស្រួលក្នុងការប្រើ bottom-up ហើយនិងសរសេរ tests។

<<<<<<< HEAD
នៅចុងបញ្ចប់នៃជំហាននេះ, អ្នកនឹងមាន library មួយជា reusable components ដែល render data model របស់អ្នក។ Components នឹងមានតែ `render` methods ដែលនេះគឺជា static version មួយនៃ app របស់អ្នក។ Component ដែលនៅផ្នែកខាងលើគេនៃរចនាសម្ព័ន្ធ (hierarchy) (`FilterableProductTable`) នឺងទទួលយក data model របស់អ្នកជា prop មួយ។ ប្រសិនបើអ្នកធ្វើការផ្លាស់ប្តូរ data model មូលដ្ឋានរបស់អ្នកហើយ call `ReactDOM.render()` ម្តងទៀត, UI នឹងត្រូវបានធ្វើបច្ចុប្បន្នភាព។ អ្នកអាចឃើញពីរបៀដែល UI របស់អ្នកធ្វើបច្ចុប្បន្នភាព ហើយនិងកន្លែងដែលវាផ្លាស់ប្តូរ។ **one-way data flow** របស់ React (ត្រូវបានគេហៅផងដែរថា *one-way binding*) រក្សារអ្វីគ្រប់យ៉ាងជាលក្ខណះ modular ហើយនិងលឿន។

ប្រសិនបើអ្នកត្រូវការជំនួយក្នុងការអនុវត្តជំហាននេះសូមចូលទៅកាន់ [React docs](/docs/)។
=======
At the end of this step, you'll have a library of reusable components that render your data model. The components will only have `render()` methods since this is a static version of your app. The component at the top of the hierarchy (`FilterableProductTable`) will take your data model as a prop. If you make a change to your underlying data model and call `root.render()` again, the UI will be updated. You can see how your UI is updated and where to make changes. React's **one-way data flow** (also called *one-way binding*) keeps everything modular and fast.

Refer to the [React docs](/docs/getting-started.html) if you need help executing this step.
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

### A Brief Interlude: Props vs State {#a-brief-interlude-props-vs-state}

"model" data នៅក្នុង React មានពីរប្រភេទ៖ props និង state។ វាចាំបាច់ក្នុងការស្វែងយល់ពីភាពខុសគ្នារវាងវាទាំងពីរ។ ក្រឡេកមើល [ឯកសារផ្លូវការរបស់ React](/docs/state-and-lifecycle.html) ប្រសិនជាអ្នកមិនប្រាកដថាអ្វីដែលជាភាពខុសគ្នារវាងវាទាំងពីរ។ សូម​មើល​ផង​ដែរនូវ [FAQ: អ្វីដែលជាភាពខុសគ្នារវាង state និង props?](/docs/faq-state.html#what-is-the-difference-between-state-and-props)

## Step 3: Identify The Minimal (but complete) Representation Of UI State {#step-3-identify-the-minimal-but-complete-representation-of-ui-state}

ដើម្បីបង្កើត UI interactive, អ្នកត្រូវការដើម្បីអាចផ្លាស់ប្តូរ trigger ទៅលើគំរូទិន្នន័យមូលដ្ឋាន។ React អាចសម្រេចបែបនេះបានជាមួយ **state**។

ដើម្បីបង្កើត app របស់អ្នកយ៉ាងត្រឹមត្រូវ, តំបូងអ្នកតម្រូវអោយគិតពីសំណុំអប្បបរមានៃ state អាចផ្លាស់ប្តូរបានដែល app របស់អ្នកត្រូវការ។ គន្លឹះគឺនៅទីនេះ [DRY: *Don't Repeat Yourself*](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)។ រកមើលការតំណាងតិចតួចបំផុតនៃ state ដែល application របស់អ្នកត្រូវការហើយនិងគណនាអ្វីៗផ្សេងទៀតដែលអ្នកត្រូវការតាមតម្រូវការ។ ឧទាហរណ៍, ប្រសិនបើអ្នកកំពុងតែបង្កើតតារាង TODO មួយ, រក្សាទុក array មួយនៃធាតុ (items) របស់ TODO នៅជុំវិញ; កុំរក្សាទុក state variable ដាច់ដោយឡែកសម្រាប់ការរាប់។ ជំនួសដោយ, ពេលដែលអ្នកចង់ render TODO count, យកប្រវែងនៃធាតុរបស់ TODO array។

<<<<<<< HEAD
គិតពីបំណែកទាំងអស់នៃទិន្នន័យនៅក្នុងឧទាហរណ៍នៃ application របស់យើង។ យើងមាន៖
=======
Think of all the pieces of data in our example application. We have:
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

  * បញ្ជីផលិតផលដើម
  * search text ដែលអ្នកប្រើប្រាស់បានបញ្ចូល
  * តម្លៃនៃ checkbox
  * បញ្ជីផលិតផល (products) ដែលបាន filtered

តេាះក្រឡេកមើលវាមួយៗហើយស្វែងយល់មួយណាគឺជា state។ សួរបីសំណួរអំពីបំណែកនៃទិន្នន័យនីមួយៗ៖

  ១. វាត្រូវបានគេបេាះពី parent មួយតាមរយៈ​ props? ដូច្នេះ, វាប្រហែលជាមិនមែនជា state។
  ២. តើវានៅតែមិនផ្លាស់ប្តូរតាមពេលវេលា? ដូច្នេះ, វាប្រហែលជាមិនមែនជា state។
  ៣. តើអ្នកអាចគណនាវាដោយផ្អែកលើ state ផ្សេងឬ props ដែលនៅក្នុង component របស់អ្នក? ដូច្នេះ, វាប្រហែលជាមិនមែនជា state។

បញ្ជីដើមនៃផលិតផលត្រូវបាន passed ចូលដែលជា props, ដូច្នេះនេះគឺមិនមែនជា state។ search text និង checkbox ហាក់ដូចជា state ដែលពួកវាផ្លាស់ប្តូរ (change) គ្រប់ពេលវេលាហើយនិងមិនអាចត្រូវបានគណនាពីអ្វីផ្សេងៗទៀត។ ហើយជាចុងក្រោយ, បញ្ជីផលិតផល (products) ដែលបាន filtered គឺមិនមែនជា state ពីព្រេាះវាអាចត្រូវបានគណនាដោយបញ្ចូលគ្នារវាងបញ្ជីផលិតផលដើមជាមួយនិង search text និងតម្លៃនៃ checkbox។

ដូច្នេះចុងក្រោយ, state របស់យើងគឺ៖

  * search text អ្នកប្រើប្រាស់បានបញ្ចូល
  * តម្លៃនៃ checkbox

## Step 4: Identify Where Your State Should Live {#step-4-identify-where-your-state-should-live}

<p data-height="600" data-theme-id="0" data-slug-hash="qPrNQZ" data-default-tab="js" data-user="lacker" data-embed-version="2" class="codepen">សូមមើល Pen <a href="https://codepen.io/gaearon/pen/qPrNQZ">Thinking In React: Step 4</a> នៅលើ <a href="https://codepen.io">CodePen</a>.</p>

អូខេ, ដូច្នេះយើងបានកំណត់ថាតើអ្វីជា minnimal set of app state។ បន្ទាប់ទៀត, យើងត្រូវកំណត់ថាតើ component មួយណាដែលផ្លាស់ប្តូរ, ឬក៏ *owns*, នេះគឺ state។

សូមចងចាំថា៖ React គឺមានលំហូរទិន្នន័យតែមួយផ្លូវចុះទៅ component hierarchy ក្រោមៗ។ វាប្រហែលជាមិនច្បាស់ថាតើ component មួយណាគួរមាន state មួយណា។ **ជារឿយៗនេះគឺជាផ្នែកដែលពិបាកបំផុតសម្រាប់អ្នកចំណូលថ្មីក្នុងការស្វែងយល់** ដូច្នេះធ្វើតាមជំហានទាំងនេះដើម្បីដោះស្រាយ៖

សម្រាប់ state នីមួយៗ នៅក្នុង application របស់អ្នក៖

  * កំនត់គ្រប់ component ទាំងអស់ដែល renders អ្វីមួយដោយផ្អែកលើ state មួយនេាះ។
  * ស្វែងរក component រួមមួយ (single component មួយដែលនៅពីលើ components ទាំងអស់ដែលត្រូវការ state នៅក្នុង hierarchy)។
  * ទាំងម្ចាស់រួមនិង component​ higher up ផ្សេងទៀតនៅក្នុង hierarchy គួរតែជាម្ចាស់នៃ state។
  * ប្រសិនបើអ្នកមិនអាចស្វែងរក component មួយដែលសម្យហេតុសម្យផលដែលត្រូវជាម្ចាស់ state, បង្កើត component តែមួយគត់សម្រាប់ការកាន់កាប់ state ហើយនិងបន្ថែមវានៅកន្លែងណាមួយក្នុង hierarchy ពីលើ component ម្ចាស់ដើមរួម។

តេាះធ្វើតាមយុទ្ធសាស្ត្រនេះសម្រាប់ application របស់យើង៖

  * `ProductTable` ត្រូវ filter តារាងផលិតផល (product list) ដោយផ្អែកលើ state និង `SearchBar` ត្រូវបង្ហាញ search text និង checked state។
  * Component ដែលជាម្ចាស់រួមគឺ `FilterableProductTable`។
  * វាសម្យហេតុសម្យផលសម្រាប់ filter text ហើយនិងពិនិត្យតម្លៃដើម្បី live នៅក្នុង `FilterableProductTable`។

Cool, ដូច្នេះយើងបានសម្រេចចិត្តថា state របស់យើង lives នៅក្នុង `FilterableProductTable`។ តំបូង, បន្ថែម instance property មួយ `this.state = {filterText: '', inStockOnly: false}` ទៅអោយ `constructor` របស់ `FilterableProductTable` ដើម្បីឆ្លុះបញ្ចាំង state តំបូង (initial state) នៃ application របស់អ្នក។ បន្ទាប់មក, បេាះ `filterText` និង `inStockOnly` ទៅអោយ `ProductTable` និង `SearchBar` ជា prop មួយ។ ចុងក្រោយ, ប្រើ props ទាំងនេាះដើម្បី filter rows នៅក្នុង `ProductTable` ហើយនិងកំនត់តម្លៃនៃ form fields នៅក្នុង `SearchBar`។

អ្នកអាចចាប់ផ្តើមមើលឃើញថា application របស់អ្នកនិងមានអ្វី៖ កំនត់ `filterText` អោយ `"ball"` និង refresh app របស់អ្នក។ អ្នកនឹងឃើញថាតារាងទិន្នន័យត្រូវបានធ្វើបច្ចុប្បន្នភាពយ៉ាងត្រឹមត្រូវ។

## Step 5: Add Inverse Data Flow {#step-5-add-inverse-data-flow}

<p data-height="600" data-theme-id="0" data-slug-hash="LzWZvb" data-default-tab="js,result" data-user="rohan10" data-embed-version="2" data-pen-title="Thinking In React: Step 5" class="codepen">សូមមើល Pen <a href="https://codepen.io/gaearon/pen/LzWZvb">Thinking In React: Step 5</a> នៅលើ <a href="https://codepen.io">CodePen</a>.</p>

រហូតមកដល់ពេលនេះយើងបានបង្កើត app មួយដែល renders យ៉ាងត្រឹមត្រូវនូវ function មួយនៃ props និង​ state ដោយអនុវត្តតាម flowing down the hierarchy។ ឥឡូវនេះដល់ពេលដែលត្រូវ support នូវលំហូរ data តាមវីធីផ្សេង៖ form components ដែលនៅជ្រៅក្នុង hierarchy តំរូវអោយ update the state នៅក្នុង `FilterableProductTable`។

React បង្កើតលំហូរ data ច្បាស់លាស់ដើម្បីជួយអ្នកឱ្យយល់ពីរបៀបដែលកម្មវិធីរបស់អ្នកដំណើរការ, ប៉ុន្តែវាមិនតំរូវឱ្យមានការ typing ច្រើនជាង traditional two-way data binding នេាះទេ។

<<<<<<< HEAD
ប្រសិនបើអ្នកព្យាយាម type ឬក៏ពិនិត្យ the box នៅក្នុងកំណែបច្ចុប្បន្ននៃឧទាហរណ៍នេះ,​ អ្នកនឹងឃើញថា React មិនអើពើនឹងការបញ្ចូលរបស់អ្នក។ នេះគឺជាចេតនា, 
ដូចដែលយើងបាន set `value` prop នៃ the `input` ដែលតែងតែស្មើរទៅនិង the `state` ដែលបានបេាះពី `FilterableProductTable`។
=======
If you try to type or check the box in the previous version of the example (step 4), you'll see that React ignores your input. This is intentional, as we've set the `value` prop of the `input` to always be equal to the `state` passed in from `FilterableProductTable`.
>>>>>>> 707f22d25f5b343a2e5e063877f1fc97cb1f48a1

តោះគិតអំពីអ្វីដែលយើងចង់អោយកើតឡើង។ យើងចង់ធ្វើឱ្យប្រាកដថានៅពេលណាដែលអ្នកប្រើប្រាស់ផ្លាស់ប្តូរ form, យើងធ្វើបច្ចុប្បន្នភាព state ដើម្បីឆ្លុះបញ្ចាំងពីការបញ្ចូលរបស់អ្នកប្រើប្រាស់។ ដែល components គួរតែធ្វើបច្ចុប្បន្នភាពនូវ state ផ្ទាល់ខ្លួនរបស់ពួកវា, `FilterableProductTable` នឹងបេាះ callbacks ទៅកាន់ `SearchBar` ដែលនឹង fire រាល់ពេលដែល state គួរតែត្រូវបានគេធ្វើបច្ចុប្បន្នភាព។ យើងអាចប្រើ `onChange` event ទៅលើ inputs ដើម្បីជូនដំណឹងអំពីវា។ The callbacks ត្រូវបានបេាះដោយ `FilterableProductTable` នឹង call `setState()`, ហើយ app នឹងត្រូវបានគេធ្វើបច្ចុប្បន្នភាព។

## And That's It {#and-thats-it}

សង្ឃឹមថានេះផ្តល់ឱ្យអ្នកនូវគំនិតនៃការគិតអំពីការបង្កើត components ហើយនិង applications ជាមួយ React។ ខណៈពេលដែលវាអាចជាការវាយច្រើនជាងអ្នកធ្លាប់ប្រើ, សូមចាំថាកូដត្រូវបានអានច្រើនជាងអ្វីដែលបានសរសេរ, ហើយវាពិបាកក្នុងការអាន modular នេះ, code គឺច្បាស់លាស់ណាស់។ ដូចដែលអ្នកចាប់ផ្តើមបង្កើត libraries ធំៗនៃ components, អ្នកនឹងពេញចិត្តនូវ explicitness និង modularity នេះ, ហើយនិងជាមួយការកាត់បន្ថយកូដ, បន្ទាត់នៃកូដរបស់អ្នកនឹងចាប់ផ្តើមកាត់បន្ថយ។ :)
