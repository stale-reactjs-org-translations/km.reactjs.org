---
id: cdn-links
title: CDN Links
permalink: docs/cdn-links.html
prev: create-a-new-react-app.html
next: hello-world.html
---

ទាំង React និង ReactDOm គឺមាននៅលើ CDN។

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

កំណែ (versions) ខាងលើគឺមានន័យតែសម្រាប់ development និងមិនសមស្របសម្រាប់ production។ កំណែ production (production versions) ដែលបាន minified និង optimized នៃ React គឺមាននៅ៖

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
```

ដើម្បី load កំណែជាក់លាក់ (specific version) មួយនៃ​​​`react` និង `react-dom`​ជាមួយលេខកំណែ (version number)។

### Why the `crossorigin` Attribute? {#why-the-crossorigin-attribute}

If you serve React from a CDN, we recommend to keep the [`crossorigin`](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) attribute set:

```html
<script crossorigin src="..."></script>
```

We also recommend to verify that the CDN you are using sets the `Access-Control-Allow-Origin: *` HTTP header:

![Access-Control-Allow-Origin: *](../images/docs/cdn-cors-header.png)

This enables a better [error handling experience](/blog/2017/07/26/error-handling-in-react-16.html) in React 16 and later.
