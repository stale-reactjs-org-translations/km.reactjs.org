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

Also use landmark elements and roles, such as `<main>` and `<aside>`, to demarcate page regions as assistive technology allow the user to quickly navigate to these sections.

Read more about the use of these elements to enhance accessibility here:

- [Accessible Landmarks](https://www.scottohara.me/blog/2018/03/03/landmarks.html)

### Programmatically managing focus {#programmatically-managing-focus}

Our React applications continuously modify the HTML DOM during runtime, sometimes leading to keyboard focus being lost or set to an unexpected element. In order to repair this,
we need to programmatically nudge the keyboard focus in the right direction. For example, by resetting keyboard focus to a button that opened a modal window after that modal window is closed.

MDN Web Docs takes a look at this and describes how we can build [keyboard-navigable JavaScript widgets](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Keyboard-navigable_JavaScript_widgets).

To set focus in React, we can use [Refs to DOM elements](/docs/refs-and-the-dom.html).

Using this, we first create a ref to an element in the JSX of a component class:

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

Then we can focus it elsewhere in our component when needed:

 ```javascript
 focus() {
   // Explicitly focus the text input using the raw DOM API
   // Note: we're accessing "current" to get the DOM node
   this.textInput.current.focus();
 }
 ```

Sometimes a parent component needs to set focus to an element in a child component. We can do this by [exposing DOM refs to parent components](/docs/refs-and-the-dom.html#exposing-dom-refs-to-parent-components)
through a special prop on the child component that forwards the parent's ref to the child's DOM node.

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

When using a HOC to extend components, it is recommended to [forward the ref](/docs/forwarding-refs.html) to the wrapped component using the `forwardRef` function of React. If a third party HOC
does not implement ref forwarding, the above pattern can still be used as a fallback.

A great focus management example is the [react-aria-modal](https://github.com/davidtheclark/react-aria-modal). This is a relatively rare example of a fully accessible modal window. Not only does it set initial focus on
the cancel button (preventing the keyboard user from accidentally activating the success action) and trap keyboard focus inside the modal, it also resets focus back to the element that
initially triggered the modal.

>Note:
>
>While this is a very important accessibility feature, it is also a technique that should be used judiciously. Use it to repair the keyboard focus flow when it is disturbed, not to try and anticipate how
>users want to use applications.

## Mouse and pointer events {#mouse-and-pointer-events}

Ensure that all functionality exposed through a mouse or pointer event can also be accessed using the keyboard alone. Depending only on the pointer device will lead to many cases where
keyboard users cannot use your application.

To illustrate this, let's look at a prolific example of broken accessibility caused by click events. This is the outside click pattern, where a user can disable an opened popover by clicking outside the element.

<img src="../images/docs/outerclick-with-mouse.gif" alt="A toggle button opening a popover list implemented with the click outside pattern and operated with a mouse showing that the close action works." />

This is typically implemented by attaching a `click` event to the `window` object that closes the popover:

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

This may work fine for users with pointer devices, such as a mouse, but operating this with the keyboard alone leads to broken functionality when tabbing to the next element
as the `window` object never receives a `click` event. This can lead to obscured functionality which blocks users from using your application.

<img src="../images/docs/outerclick-with-keyboard.gif" alt="A toggle button opening a popover list implemented with the click outside pattern and operated with the keyboard showing the popover not being closed on blur and it obscuring other screen elements." />

The same functionality can be achieved by using an appropriate event handlers instead, such as `onBlur` and `onFocus`:

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

This code exposes the functionality to both pointer device and keyboard users. Also note the added `aria-*` props to support screen-reader users. For simplicity's sake
the keyboard events to enable `arrow key` interaction of the popover options have not been implemented.

<img src="../images/docs/blur-popover-close.gif" alt="A popover list correctly closing for both mouse and keyboard users." />

This is one example of many cases where depending on only pointer and mouse events will break functionality for keyboard users. Always testing with the keyboard will immediately
highlight the problem areas which can then be fixed by using keyboard aware event handlers.

## More Complex Widgets {#more-complex-widgets}

A more complex user experience should not mean a less accessible one. Whereas accessibility is most easily achieved by coding as close to HTML as possible,
even the most complex widget can be coded accessibly.

Here we require knowledge of [ARIA Roles](https://www.w3.org/TR/wai-aria/#roles) as well as [ARIA States and Properties](https://www.w3.org/TR/wai-aria/#states_and_properties).
These are toolboxes filled with HTML attributes that are fully supported in JSX and enable us to construct fully accessible, highly functional React components.

Each type of widget has a specific design pattern and is expected to function in a certain way by users and user agents alike:

- [WAI-ARIA Authoring Practices - Design Patterns and Widgets](https://www.w3.org/TR/wai-aria-practices/#aria_ex)
- [Heydon Pickering - ARIA Examples](https://heydonworks.com/practical_aria_examples/)
- [Inclusive Components](https://inclusive-components.design/)

## Other Points for Consideration {#other-points-for-consideration}

### Setting the language {#setting-the-language}

Indicate the human language of page texts as screen reader software uses this to select the correct voice settings:

- [WebAIM - Document Language](https://webaim.org/techniques/screenreader/#language)

### Setting the document title {#setting-the-document-title}

Set the document `<title>` to correctly describe the current page content as this ensures that the user remains aware of the current page context:

- [WCAG - Understanding the Document Title Requirement](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)

We can set this in React using the [React Document Title Component](https://github.com/gaearon/react-document-title).

### Color contrast {#color-contrast}

Ensure that all readable text on your website has sufficient color contrast to remain maximally readable by users with low vision:

- [WCAG - Understanding the Color Contrast Requirement](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
- [Everything About Color Contrast And Why You Should Rethink It](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/)
- [A11yProject - What is Color Contrast](https://a11yproject.com/posts/what-is-color-contrast/)

It can be tedious to manually calculate the proper color combinations for all cases in your website so instead, you can [calculate an entire accessible color palette with Colorable](https://jxnblk.com/colorable/).

Both the aXe and WAVE tools mentioned below also include color contrast tests and will report on contrast errors.

If you want to extend your contrast testing abilities you can use these tools:

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
