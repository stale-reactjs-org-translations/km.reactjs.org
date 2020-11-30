---
id: cdn-links
title: CDN Links
permalink: docs/cdn-links.html
prev: create-a-new-react-app.html
next: release-channels.html
---

ទាំង React និង ReactDOm គឺមាននៅលើ CDN។

```html
<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
```

កំណែ (versions) ខាងលើគឺមានន័យតែសម្រាប់ development និងមិនសមស្របសម្រាប់ production។ កំណែ production (production versions) ដែលបាន minified និង optimized នៃ React គឺមាននៅ៖

```html
<script crossorigin src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
```

<<<<<<< HEAD
ដើម្បី load កំណែជាក់លាក់ (specific version) មួយនៃ​​​`react` និង `react-dom`​ជាមួយលេខកំណែ (version number)។
=======
To load a specific version of `react` and `react-dom`, replace `17` with the version number.
>>>>>>> 5e437a10ed4e89cd5eaf990ce4f43e0857592b53

### Why the `crossorigin` Attribute? {#why-the-crossorigin-attribute}

ប្រសិនបើអ្នកប្រើ React ពី CDN យើងសូមណែនាំឱ្យរក្សាការ set [`crossorigin`](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) attribute។

```html
<script crossorigin src="..."></script>
```

យើងក៏សូមណែនាំឱ្យផ្ទៀងផ្ទាត់ថា CDN ដែលអ្នកកំពុងប្រើប្រាស់ sets នូវ `Access-Control-Allow-Origin: *` HTTP header៖

![Access-Control-Allow-Origin: *](../images/docs/cdn-cors-header.png)

នេះធ្វើឱ្យប្រសើរឡើងនូវ [error handling experience](/blog/2017/07/26/error-handling-in-react-16.html) នៅក្នុង React 16 និងក្រោយៗ។
