---
id: accessibility
title: Accessibility
permalink: docs/accessibility.html
---

## ហេតុអ្វីបានជា Accessibility? {#why-accessibility}

Web accessibility (ក៏អាចហៅបានជា[**a11y**](https://en.wiktionary.org/wiki/a11y)) គឺជាការរចនានិងបង្កើតគេហទំព័រដែលអាចប្រើប្រាស់បានដោយមនុស្សគ្រប់គ្នា។ Accessibility supportគឺចាំបាច់សំរាប់ឱ្យបច្ចេកវិទ្យាជំនួយបកប្រែទៅជាគេហទំព័រ។

React fully supports building accessible websites, often by using standard HTML techniques.
Reactគាំទ្រយ៉ាងពេញលេញក្នុងការបង្កើតគេហទំព័រដែលអាចចូលដំណើរការបានដោយប្រើបច្ចេកទេសស្តង់ដាររបស់ HTML។

## ស្តង់ដារ និង ការណែនាំ {#standards-and-guidelines}

### WCAG {#wcag}

[ការណែនាំមាតិកាលទ្ធភាពប្រើប្រាស់គេហទំព័រ | Web Content Accessibility Guidelines](https://www.w3.org/WAI/intro/wcag) ផ្តល់នូវគោលការណ៍ណែនាំសម្រាប់បង្កើតគេហទំព័រដែលអាចចូលដំណើរការបាន។

បញ្ជីផ្ទៀងផ្ទាត់ WCAG ខាងក្រោមនេះនឹងផ្តល់នូវសេចក្តីសង្ខេបទូទៅ:

- [WCAG checklist from Wuhcag](https://www.wuhcag.com/wcag-checklist/)
- [WCAG checklist from WebAIM](https://webaim.org/standards/wcag/checklist)
- [Checklist from The A11Y Project](https://a11yproject.com/checklist.html)

### WAI-ARIA {#wai-aria}

[Web Accessibility Initiative - Accessible Rich Internet Applications](https://www.w3.org/WAI/intro/aria) គឺជាឯកសារដែលមាននូវបច្ចេកទេសសំរាប់បង្កើត(ធាតុក្រាហ្វិក JavaScript ឬ JavaScript widgets) យ៉ាងពេញលេញមួយ។

ចំណាំថា attribute `aria-*` ទាំងអស់របស់ HTML អាចប្រើប្រាស់យ៉ាងពេញលេញនៅក្នុង JSX ។ ខណៈពេលដែល properties និង attibutes ភាគច្រើនរបស់ DOM ក្នុង React ប្រើប្រាស់ជាស្ទីល camelCased ដែល attributes ទាំងនោះគួរតែសរសេរបែប hyphen-cased (ត្រូវបានគេស្គាល់ដូចជា kebab-case, lisp-case ជាដើម) ដែលដូចទៅនឹងការសរសេរក្នុង HTML ធម្មតា:

```javascript{3,4}
<input
  type="text"
  aria-label={labelText}
  aria-required="true"
  onChange={onchangeHandler}
  value={inputValue}
  name="name"
/>
```

## Semantic HTML {#semantic-html}
Semantic HTML គឺជាមូលដ្ឋានគ្រឹះនៃភាពងាយស្រួលនៅក្នុងកម្មវិធីបណ្តាញ។ ការប្រើធាតុ HTML ផ្សេងៗដើម្បីពង្រឹងអត្ថន័យនៃពត៌មាន
នៅក្នុងគេហទំព័ររបស់យើងនឹងផ្តល់អោយយើងប្រើប្រាស់ដោយឥតគិតថ្លៃ។

- [អត្ថបទយោងរបស់ធាតុ MDN HTML | MDN HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

ពេលខ្លះដើម្បីអោយកូត React របស់យើងដើរ យើងបានបន្ថែមធាតុ `<div>` ទៅកាន់ JSX ដែលអាចបំបែក HTML semantics ជាពិសេសនៅពេលដែលធ្វើការជាមួយ(បញ្ជី | lists) (`<ol>`, `<ul>` និង `<dl>`) និង HTML `<table>`។
ក្នុងករណីនេះយើងគួរតែប្រើ [React Fragments](/docs/fragments.html) ដើម្បីដាក់ធាតុច្រើនរួមបញ្ចូលជាក្រុម។

ឧទាហរណ៍៖

```javascript{1,5,8}
import React, { Fragment } from 'react';
function ListItem({ item }) {
  return (
    <Fragment>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </Fragment>
  );
}

function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        <ListItem item={item} key={item.id} />
      ))}
    </dl>
  );
}
```

អ្នកអាចធ្វើការ map ក្រុមនៃធាតុទៅជាអារេនៃ fragment ដូចដែលអ្នកចង់បានប្រភេទធាតុផ្សេងៗទៀតផងដែរ៖

```javascript{6,9}
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // Fragments should also have a `key` prop when mapping collections
        <Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </Fragment>
      ))}
    </dl>
  );
}
```

នៅពេលដែលអ្នកមិនត្រូវការ props លើ Fragment tag អ្នកអាចប្រើបែប [short syntax](/docs/fragments.html#short-syntax) បើសិនជាឧបករណ៍របស់អ្នកគាំទ្រ៖

```javascript{3,6}
function ListItem({ item }) {
  return (
    <>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </>
  );
}
```

សូមចូលទៅកាន់ [the Fragments documentation](/docs/fragments.html) សំរាប់ព័ត៌មានបន្ថែម។

## Accessible Forms {#accessible-forms}

### ការដាក់ស្លាកឈ្មោះ {#labeling}
គ្រប់ HTML form control ទាំងអស់ដូចជា `<input>` និង `<textarea>` ត្រូវការការដាក់ឈ្មោះដែលងាយល់។
យើងត្រូវតែផ្តល់ឬមានការពិពណ៌នានៃស្លាក ដែលអាចអោយអ្នកប្រើប្រាស់មើលឃើញ។

ធនធានខាងក្រោមនេះនឹងបង្ហាញយើងពីរបៀបដាក់ឈ្មោះ៖

- [The W3C shows us how to label elements](https://www.w3.org/WAI/tutorials/forms/labels/)
- [WebAIM shows us how to label elements](https://webaim.org/techniques/forms/controls)
- [The Paciello Group explains accessible names](https://www.paciellogroup.com/blog/2017/04/what-is-an-accessible-name/)


យើងក៏អាចប្រើប្រាស់នៅក្នុង React ដូចទៅនឹងការអនុវត្តតាមស្តង់ដាររបស់ HTML ខាងលើផងដែរ។ ចំណាំថា នៅក្នុង JSX `for` attribute គឺសរសេរទៅជា `htmlFor`៖

```javascript{1}
<label htmlFor="namedInput">Name:</label>
<input id="namedInput" type="text" name="name"/>
```

### ផ្តល់ដំណឹងដល់អ្នកប្រើប្រាស់ពេលដែលមាន errors {#notifying-the-user-of-errors}

គ្រប់ស្ថានភាព Error ទាំងអស់ត្រូវតែយល់ដោយអ្នកប្រើប្រាស់ទាំងអស់។ link ខាងក្រោមនឹងប្រាប់យើងពីរបៀបបង្ហាញសារ error ទៅកាន់អេក្រង់អ្នកអាន៖

- [The W3C demonstrates user notifications](https://www.w3.org/WAI/tutorials/forms/notifications/)
- [WebAIM looks at form validation](https://webaim.org/techniques/formvalidation/)

## Focus Control {#focus-control}

ត្រូវប្រាកដថាកម្មវិធីគេហទំព័ររបស់អ្នកអាចដំណើរការបានតែជាមួយក្តារចុចប៉ុណ្ណោះ៖

- [WebAIM talks about keyboard accessibility](https://webaim.org/techniques/keyboard/)

### Keyboard focus and focus outline {#keyboard-focus-and-focus-outline}

Keyboard focus សំដៅទៅលើ element នៅក្នុង DOM ដែលបានត្រូវ selected ឬឈរលើសំរាប់ចាំទទួលការបញ្ចូលពី keybaord។ យើងអាចឃើញសន្ថានលក្ខណៈរបស់វាគ្រប់ទីកន្លែង ដែលដូចនឹងរូបភាពបានបង្ហាញខាងក្រោម៖

<img src="../images/docs/keyboard-focus.png" alt="Blue keyboard focus outline around a selected link." />

ប្រសិនបើអ្នកជំនួស focus outline ជាមួយនឹងការដាក់ focus outline ផ្សេងទៀត មានតែប្រើ CSS ដើម្បីដក outline នេះចេញ។ ឧទាហរណ៍ដូចជាការដាក់ `outline: 0`។

### Mechanisms to skip to desired content {#mechanisms-to-skip-to-desired-content}

ផ្តល់វិធីសាស្រ្តដែលអនុញ្ញាតឱ្យអ្នកប្រើប្រាស់អាចរំលង ផ្នែក navigation ពីមុនក្នុងកម្មវិធីរបស់អ្នក ដែលអាចជួយនិងពន្លឿនល្បឿន navigation របស់ក្តាចុច។

Skiplinks or Skip Navigation Links គឺជា navigation links មើលមិនឃើញដែលអាចឃើញវិញនៅពេលដែលក្តារចុចរបស់អ្នកប្រើប្រាស់មានទំនាក់ទំនងជាមួួយ page។ ក្នុងការអនុវត្តឬសរសេរជាមួយនឹង page anchors ផ្ទាល់ខ្លួនគឺមានភាពងាយស្រួលក៏ដូចជាការដាក់ស្ទីល៖

ប្រើប្រាស់ landmark elements និង roles ដូចជ​ា `<main>` និង `<aside>` ដើម្បីកំណត់ព្រំដែនតាមទំព័រសំរាប់ជួយដល់ការ navigate របស់អ្នកប្រើប្រាស់ទៅកាន់តាមផ្នែក។

ស្វែងយល់ពីការប្រើប្រាស់នៃ elements ទាំងនោះដើម្បីបង្កើនលទ្ធភាព៖

- [Accessible Landmarks](https://www.scottohara.me/blog/2018/03/03/landmarks.html)

### Programmatically managing focus {#programmatically-managing-focus}

កម្មវិធី React របស់យើងបន្តកែប្រែ DOM របស់ HTML កំឡុងពេលដំណើរការ ពេលខ្លះនាំឱ្យក្តាចុចបាត់បង់ focus ឬ កំណត់ទៅធាតុផ្សេងដោយមិនមានការរំពឹងទុក។ ដើម្បីជួសជុលវា,
យើងត្រូវការដាក់កម្មវិធីផ្តោតលើក្តារចុចឱ្យបានត្រឹមត្រូវ។ ឧទាហរណ៍ដោយកំណត់ការផ្តោតលើក្តារចុចទៅលើប៊ូតុងបន្ទាប់ពី modal windows នោះត្រូវបានបិទ។

នេះជាវេបសាយនៃឯកសាររបស់ MDN និងមានបង្ហាញយើងពីរបៀបបង្កើត MDN
[keyboard-navigable JavaScript widgets](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Keyboard-navigable_JavaScript_widgets).

ដើម្បីដាក់ focus ក្នុង React យើងអាចប្រើ [Refs to DOM elements](/docs/refs-and-the-dom.html).

ដើម្បីប្រើវាយើងដំបូងបង្កើត ref ទៅកាន់ element នៅក្នុង JSX នៃ component class៖

```javascript{4-5,8-9,13}
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // Create a ref to store the textInput DOM element
    this.textInput = React.createRef();
  }
  render() {
  // Use the `ref` callback to store a reference to the text input DOM
  // element in an instance field (for example, this.textInput).
    return (
      <input
        type="text"
        ref={this.textInput}
      />
    );
  }
}
```

បន្ទាប់មកយើងអាច focus នៅកន្លែងផ្សេងៗក្នុង component របស់យើងនៅពេលដែលត្រូវការ៖

 ```javascript
 focus() {
   // Explicitly focus the text input using the raw DOM API
   // Note: we're accessing "current" to get the DOM node
   this.textInput.current.focus();
 }
 ```

ពេលខ្លះ component មេត្រូវតែដាក់ focus ទៅ element នៅក្នុង component កូន។ យើងអាចដាក់បានដោយ [exposing DOM refs to parent components](/docs/refs-and-the-dom.html#exposing-dom-refs-to-parent-components) តាមរយះ prop ពិសេសនៅលើ component កូនដែលផ្តល់តាម ref នៃមេ ទៅកាន់ DOM node របស់កូន។

```javascript{4,12,16}
function CustomTextInput(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}

class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.inputElement = React.createRef();
  }
  render() {
    return (
      <CustomTextInput inputRef={this.inputElement} />
    );
  }
}

// Now you can set focus when required.
this.inputElement.current.focus();
```

នៅពេលប្រើ HOC ដើម្បីពង្រីក component
យើងណែនាំ [forward the ref](/docs/forwarding-refs.html) សំរាប់ខ្ចប់ component ដោយប្រើ `forwardRef` function នៃ React។
ប្រសិនបើជំនួយការរបស់ HOC មិនបានដាក់បញ្ចូល ref forwardingទេ លំនាំខាងលើនៅតែអាចប្រើជា fallback បាន។

[react-aria-modal](https://github.com/davidtheclark/react-aria-modal) គឺជាឧទាហរណ៏នៃការគ្រប់គ្រង focus ដ៏ល្អ។ នេះជាឧទាហរណ៍ដ៏កម្រនៃ accessible modal window ពេញលេញ។ មិនត្រឹមតែកំណត់អាទិភាព focus លើប៊ូតុង cancel (ការពារអ្នកប្រើ keyboard ពីការធ្វើសកម្មភាពជោគជ័យដោយគ្មានបំណង) និងលាក់ keyboard focus នៅក្នុង modal ហើយវាកំណត់ឡើងវិញនៃ focus ទៅកាន់ element ដែលធ្វើឱ្យ modal ដំណើរការ។

>ចំណាំ:
>
>ខណៈនេះជា accessibility feature ដ៏សំខាន់ ដូច្នេះវាក៏ជាជាបច្ចេកទេសដែលគួរត្រូវតែបានប្រើដោយត្រឹមត្រូវ។
> ប្រើវាដើម្បីជួសជុលលំហូរនៃ keyboard focus នៅពេលវាត្រូវបានរំខាន, កុំព្យាយាមនិងរំពឹងមើលពីរបៀបដែលអ្នកប្រើចង់ប្រើកម្មវិធី។

## Mouse and pointer events {#mouse-and-pointer-events}

ធានាថាមុខងារទាំងអស់ដែលធ្វើការតាមរយះ mouse ឬ pointer event ក៏អាចប្រើប្រាស់បានដោយ keybaord តែឯងបាន។ ការពឹងទៅលើឧបករណ៍ pointer តែមួយមុខនឹងនាំមកនូវបញ្ហាផ្សេងៗទៅដល់អ្នកប្រើប្រាស់ keybaord ទៅកាន់កម្មវិធីរបស់អ្នក។

ដើម្បីបង្ហាញពីចំនុចនេះសូមមើលឧទាហរណ៍ដ៏អស្ចារ្យមួយនៃភាពងាយស្រួលដែលបណ្តាលមកពីការចុចព្រឹត្តិការណ៍។ នេះគឺជាលំនាំចុចខាងក្រៅដែលអ្នកប្រើអាចបិទដំណើរការ popover ដែលបានបើកដោយចុចខាងក្រៅ element។

<img src="../images/docs/outerclick-with-mouse.gif" alt="A toggle button opening a popover list implemented with the click outside pattern and operated with a mouse showing that the close action works." />

នេះត្រូវបានអនុវត្តជាធម្មតាដោយការភ្ជាប់មួយព្រឹត្តិការណ៍ `click` ទៅកាន់នឹងវត្ថុរបស់ `window` ដែលអាចបិទ popover នោះ៖

```javascript{12-14,26-30}
class OuterClickExample extends React.Component {
constructor(props) {
    super(props);

    this.state = { isOpen: false };
    this.toggleContainer = React.createRef();

    this.onClickHandler = this.onClickHandler.bind(this);
    this.onClickOutsideHandler = this.onClickOutsideHandler.bind(this);
  }

  componentDidMount() {
    window.addEventListener('click', this.onClickOutsideHandler);
  }

  componentWillUnmount() {
    window.removeEventListener('click', this.onClickOutsideHandler);
  }

  onClickHandler() {
    this.setState(currentState => ({
      isOpen: !currentState.isOpen
    }));
  }

  onClickOutsideHandler(event) {
    if (this.state.isOpen && !this.toggleContainer.current.contains(event.target)) {
      this.setState({ isOpen: false });
    }
  }

  render() {
    return (
      <div ref={this.toggleContainer}>
        <button onClick={this.onClickHandler}>Select an option</button>
        {this.state.isOpen ? (
          <ul>
            <li>Option 1</li>
            <li>Option 2</li>
            <li>Option 3</li>
          </ul>
        ) : null}
      </div>
    );
  }
}
```

វាប្រហែលជាដំណើរប្រក្រតីធម្មតាជាមួួយនឹងអ្នកប្រើប្រាស់ឧបករណ៍ចង្អុលដូចជា mouse។ ប៉ុន្តែបើធ្វើប្រតិបត្តការណ៍ជាមួយតែ keybaord អាចនឹងជួបបញ្ហានៅពេលដែលចុចដើម្បីផ្តូរទៅកាន់ element បន្ទាប់បណ្តាលឱ្យ `window` មិនបានទទួលប្រតិការណ៍ចុច។ វាអាចនាំឱ្យមុខងារដែលមិនច្បាស់លាស់ដែលរារាំងអ្នកប្រើពីការប្រើកម្មវិធីរបស់អ្នក។

<img src="../images/docs/outerclick-with-keyboard.gif" alt="A toggle button opening a popover list implemented with the click outside pattern and operated with the keyboard showing the popover not being closed on blur and it obscuring other screen elements." />

functionality ដូចគ្នាអាចសម្រេចបានដោយប្រើព្រឹត្តិការណ៍សមរម្យជំនួសវិញដើម្បីដោះស្រាយ ដូចជា `onBlur` និង `onFocus`៖

```javascript{19-29,31-34,37-38,40-41}
class BlurExample extends React.Component {
  constructor(props) {
    super(props);

    this.state = { isOpen: false };
    this.timeOutId = null;

    this.onClickHandler = this.onClickHandler.bind(this);
    this.onBlurHandler = this.onBlurHandler.bind(this);
    this.onFocusHandler = this.onFocusHandler.bind(this);
  }

  onClickHandler() {
    this.setState(currentState => ({
      isOpen: !currentState.isOpen
    }));
  }

  // We close the popover on the next tick by using setTimeout.
  // This is necessary because we need to first check if
  // another child of the element has received focus as
  // the blur event fires prior to the new focus event.
  onBlurHandler() {
    this.timeOutId = setTimeout(() => {
      this.setState({
        isOpen: false
      });
    });
  }

  // If a child receives focus, do not close the popover.
  onFocusHandler() {
    clearTimeout(this.timeOutId);
  }

  render() {
    // React assists us by bubbling the blur and
    // focus events to the parent.
    return (
      <div onBlur={this.onBlurHandler}
           onFocus={this.onFocusHandler}>
        <button onClick={this.onClickHandler}
                aria-haspopup="true"
                aria-expanded={this.state.isOpen}>
          Select an option
        </button>
        {this.state.isOpen ? (
          <ul>
            <li>Option 1</li>
            <li>Option 2</li>
            <li>Option 3</li>
          </ul>
        ) : null}
      </div>
    );
  }
}
```

កូដនេះបង្ហាញពីមុខងារទាំងអ្នកប្រើឧបករណ៍ចង្អុលនិងអ្នកប្រើក្តារចុច។ ហើយចាំថាដាក់បន្ថែម `aria-*` props សម្រាប់ជួយអ្នកប្រើប្រាស់។ សម្រាប់ភាពសាមញ្ញរបស់
ព្រឹត្តិការណ៍ក្តារចុចដើម្បីបើកដំណើរការរវាងនឹង 'key arrow' នៃជម្រើស popover មិនត្រូវបានអនុវត្ត។

<img src="../images/docs/blur-popover-close.gif" alt="A popover list correctly closing for both mouse and keyboard users." />

នេះជាឧទាហរណ៍មួយនៃករណីជាច្រើនដែលអាស្រ័យលើតែព្រឹត្តិការណ៍ចង្អុល ឬ mouse នាំឱ្យមានបញ្ហាដល់អ្នកប្រើប្រាស់ក្តារចុច។ តែងតែសាកល្បងជាមួយនឹងក្តារចុចភ្លាមៗ ដើម្បីរកបញ្ហាដែលអាចកែតំរូវដោយប្រើព្រឹត្តិការការពាររបស់ក្តាចុច។

## More Complex Widgets {#more-complex-widgets}

A more complex user experience should not mean a less accessible one. Whereas accessibility is most easily achieved by coding as close to HTML as possible,
even the most complex widget can be coded accessibly.
បទពិសោធអ្នកប្រើដែលស្មុគស្មាញមិនគួរមានន័យថាអាចចូលប្រើបានតិចជាងមួយទេ។

ទីនេះយើងត្រូវការចំណេះដឹងនៃ [ARIA Roles](https://www.w3.org/TR/wai-aria/#roles) ដូចជា [ARIA States and Properties](https://www.w3.org/TR/wai-aria/#states_and_properties)។ ទាំងនេះគឺជាប្រអប់ឧបករណ៍ដែលបំពេញដោយ attributes របស់ HTML ដែលត្រូវបានគាំទ្រយ៉ាងពេញលេញនៅក្នុង JSX និងអាចឱ្យយើងបង្កើត components របស់ React ដែលអាចចូលដំណើរការបានយ៉ាងពេញលេញ។

Each type of widget has a specific design pattern and is expected to function in a certain way by users and user agents alike:
ប្រភេទធាតុក្រាហ្វិកនីមួយៗមានលំនាំរចនាជាក់លាក់ហើយត្រូវបានគេរំពឹងថានឹងដំណើរការតាមវិធីជាក់ស្តែងដោយអ្នកប្រើនិងភ្នាក់ងារអ្នកប្រើដូចគ្នា៖

- [WAI-ARIA Authoring Practices - Design Patterns and Widgets](https://www.w3.org/TR/wai-aria-practices/#aria_ex)
- [Heydon Pickering - ARIA Examples](https://heydonworks.com/practical_aria_examples/)
- [Inclusive Components](https://inclusive-components.design/)

## Other Points for Consideration {#other-points-for-consideration}

### Setting the language {#setting-the-language}

Indicate the human language of page texts as screen reader software uses this to select the correct voice settings:
ចង្អុលបង្ហាញភាសាមនុស្សនៃអត្ថបទទំព័រដែលជាកម្មវិធីអានអេក្រង់ប្រើនេះដើម្បីជ្រើសការកំណត់សំឡេងត្រឹមត្រូវ៖

- [WebAIM - Document Language](https://webaim.org/techniques/screenreader/#language)

### Setting the document title {#setting-the-document-title}

Set the document `<title>` to correctly describe the current page content as this ensures that the user remains aware of the current page context:
កំណត់ឯកសារ `<title>` ដើម្បីពិពណ៌នាខ្លឹមសារទំព័របច្ចុប្បន្នយ៉ាងត្រឹមត្រូវដែលវាធានាថាអ្នកប្រើប្រាស់នៅតែដឹងពីបរិបទទំព័របច្ចុប្បន្ន៖

- [WCAG - Understanding the Document Title Requirement](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)

We can set this in React using the [React Document Title Component](https://github.com/gaearon/react-document-title).
យើងអាចកំណត់វានៅក្នុងការឆ្លើយតបដោយប្រើប៊ូតុង [React Document Title Component](https://github.com/gaearon/react-document-title)។

### Color contrast {#color-contrast}

Ensure that all readable text on your website has sufficient color contrast to remain maximally readable by users with low vision:
ត្រូវប្រាកដថាអត្ថបទទាំងអស់ដែលអាចអានបាននៅលើគេហទំព័ររបស់អ្នកមានភាពផ្ទុយគ្នាពណ៌គ្រប់គ្រាន់ដើម្បីនៅតែអាចអានបានដោយអ្នកប្រើដែលមានពន្លឺតិចតួច៖

- [WCAG - Understanding the Color Contrast Requirement](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
- [Everything About Color Contrast And Why You Should Rethink It](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/)
- [A11yProject - What is Color Contrast](https://a11yproject.com/posts/what-is-color-contrast/)

It can be tedious to manually calculate the proper color combinations for all cases in your website so instead, you can [calculate an entire accessible color palette with Colorable](https://jxnblk.com/colorable/).
វាអាចធុញទ្រាន់ក្នុងការគណនាបន្សំពណ៌ត្រឹមត្រូវសម្រាប់គ្រប់ករណីទាំងអស់នៅក្នុងគេហទំព័ររបស់អ្នកដូច្នេះ អ្នកអាចធ្វើបាន [calculate an entire accessible color palette with Colorable](https://jxnblk.com/colorable/)។

Both the aXe and WAVE tools mentioned below also include color contrast tests and will report on contrast errors.
ទាំងឧបករណ៍ aXe និង WAVE ដែលបានរៀបរាប់ខាងក្រោមក៏មានការធ្វើតេស្តកម្រិតពណ៌ហើយនឹងរាយការណ៍អំពីកំហុសឆ្គងផងដែរ។

If you want to extend your contrast testing abilities you can use these tools:
ប្រសិនបើអ្នកចង់ពង្រីកសមត្ថភាពសាកល្បងកម្រិតពណ៌របស់អ្នកអ្នកអាចប្រើឧបករណ៍ទាំងនេះ៖

- [WebAIM - Color Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [The Paciello Group - Color Contrast Analyzer](https://www.paciellogroup.com/resources/contrastanalyser/)

## Development and Testing Tools {#development-and-testing-tools}

There are a number of tools we can use to assist in the creation of accessible web applications.

### The keyboard {#the-keyboard}

By far the easiest and also one of the most important checks is to test if your entire website can be reached and used with the keyboard alone. Do this by:

1. Plugging out your mouse.
1. Using `Tab` and `Shift+Tab` to browse.
1. Using `Enter` to activate elements.
1. Where required, using your keyboard arrow keys to interact with some elements, such as menus and dropdowns.

### Development assistance {#development-assistance}

We can check some accessibility features directly in our JSX code. Often intellisense checks are already provided in JSX aware IDE's for the ARIA roles, states and properties. We also
have access to the following tool:

#### eslint-plugin-jsx-a11y {#eslint-plugin-jsx-a11y}

The [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) plugin for ESLint provides AST linting feedback regarding accessibility issues in your JSX. Many
IDE's allow you to integrate these findings directly into code analysis and source code windows.

[Create React App](https://github.com/facebookincubator/create-react-app) has this plugin with a subset of rules activated. If you want to enable even more accessibility rules,
you can create an `.eslintrc` file in the root of your project with this content:

  ```json
  {
    "extends": ["react-app", "plugin:jsx-a11y/recommended"],
    "plugins": ["jsx-a11y"]
  }
  ```

### Testing accessibility in the browser {#testing-accessibility-in-the-browser}

A number of tools exist that can run accessibility audits on web pages in your browser. Please use them in combination with other accessibility checks mentioned here as they can only
test the technical accessibility of your HTML.

#### aXe, aXe-core and react-axe {#axe-axe-core-and-react-axe}

Deque Systems offers [aXe-core](https://github.com/dequelabs/axe-core) for automated and end-to-end accessibility tests of your applications. This module includes integrations for Selenium.

[The Accessibility Engine](https://www.deque.com/products/axe/) or aXe, is an accessibility inspector browser extension built on `aXe-core`.

You can also use the [react-axe](https://github.com/dylanb/react-axe) module to report these accessibility findings directly to the console while developing and debugging.

#### WebAIM WAVE {#webaim-wave}

The [Web Accessibility Evaluation Tool](https://wave.webaim.org/extension/) is another accessibility browser extension.

#### Accessibility inspectors and the Accessibility Tree {#accessibility-inspectors-and-the-accessibility-tree}

[The Accessibility Tree](https://www.paciellogroup.com/blog/2015/01/the-browser-accessibility-tree/) is a subset of the DOM tree that contains accessible objects for every DOM element that should be exposed
to assistive technology, such as screen readers.

In some browsers we can easily view the accessibility information for each element in the accessibility tree:

- [Using the Accessibility Inspector in Firefox](https://developer.mozilla.org/en-US/docs/Tools/Accessibility_inspector)
- [Activate the Accessibility Inspector in Chrome](https://gist.github.com/marcysutton/0a42f815878c159517a55e6652e3b23a)
- [Using the Accessibility Inspector in OS X Safari](https://developer.apple.com/library/content/documentation/Accessibility/Conceptual/AccessibilityMacOSX/OSXAXTestingApps.html)

### Screen readers {#screen-readers}

Testing with a screen reader should form part of your accessibility tests.

Please note that browser / screen reader combinations matter. It is recommended that you test your application in the browser best suited to your screen reader of choice.

### Commonly Used Screen Readers {#commonly-used-screen-readers}

#### NVDA in Firefox {#nvda-in-firefox}

[NonVisual Desktop Access](https://www.nvaccess.org/) or NVDA is an open source Windows screen reader that is widely used.

Refer to the following guides on how to best use NVDA:

- [WebAIM - Using NVDA to Evaluate Web Accessibility](https://webaim.org/articles/nvda/)
- [Deque - NVDA Keyboard Shortcuts](https://dequeuniversity.com/screenreaders/nvda-keyboard-shortcuts)

#### VoiceOver in Safari {#voiceover-in-safari}

VoiceOver is an integrated screen reader on Apple devices.

Refer to the following guides on how activate and use VoiceOver:

- [WebAIM - Using VoiceOver to Evaluate Web Accessibility](https://webaim.org/articles/voiceover/)
- [Deque - VoiceOver for OS X Keyboard Shortcuts](https://dequeuniversity.com/screenreaders/voiceover-keyboard-shortcuts)
- [Deque - VoiceOver for iOS Shortcuts](https://dequeuniversity.com/screenreaders/voiceover-ios-shortcuts)

#### JAWS in Internet Explorer {#jaws-in-internet-explorer}

[Job Access With Speech](https://www.freedomscientific.com/Products/software/JAWS/) or JAWS, is a prolifically used screen reader on Windows.

Refer to the following guides on how to best use JAWS:

- [WebAIM - Using JAWS to Evaluate Web Accessibility](https://webaim.org/articles/jaws/)
- [Deque - JAWS Keyboard Shortcuts](https://dequeuniversity.com/screenreaders/jaws-keyboard-shortcuts)

### Other Screen Readers {#other-screen-readers}

#### ChromeVox in Google Chrome {#chromevox-in-google-chrome}

[ChromeVox](https://www.chromevox.com/) is an integrated screen reader on Chromebooks and is available [as an extension](https://chrome.google.com/webstore/detail/chromevox/kgejglhpjiefppelpmljglcjbhoiplfn?hl=en) for Google Chrome.

Refer to the following guides on how best to use ChromeVox:

- [Google Chromebook Help - Use the Built-in Screen Reader](https://support.google.com/chromebook/answer/7031755?hl=en)
- [ChromeVox Classic Keyboard Shortcuts Reference](https://www.chromevox.com/keyboard_shortcuts.html)
