---
id: faq-ajax
title: AJAX and APIs
permalink: docs/faq-ajax.html
layout: docs
category: FAQ
---

### តើខ្ញ៉ំអាចហៅAJAX មកប្រើតាមរបៀបណា? {#how-can-i-make-an-ajax-call}

ជាមូួយReact អ្នកអាចប្រើAJAX library មួយណាក៏បានតាមដែលអ្នកចង់ប្រើ។ ខាងក្រោមនេះ គីជាlibrary មួយចំនូនដែលត្រូវបានគេប្រើប្រាស់ច្រើនក្នុងពេលបច្ចុប្បន្ន:
  1. [Axios](https://github.com/axios/axios)
  2. [jQuery AJAX](https://api.jquery.com/jQuery.ajax/)
  3. [window.fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) ដែលជាមុខងារ មានស្រាប់ក្នុងកម្មវិធីសម្រាប់បើកវែបសាយ(browser)

### Where in the component lifecycle should I make an AJAX call? {#where-in-the-component-lifecycle-should-i-make-an-ajax-call}

You should populate data with AJAX calls in the [`componentDidMount`](/docs/react-component.html#mounting) lifecycle method. This is so you can use `setState` to update your component when the data is retrieved.

### Example: Using AJAX results to set local state {#example-using-ajax-results-to-set-local-state}

The component below demonstrates how to make an AJAX call in `componentDidMount` to populate local component state.

The example API returns a JSON object like this:

```
{
  "items": [
    { "id": 1, "name": "Apples",  "price": "$2" },
    { "id": 2, "name": "Peaches", "price": "$5" }
  ]
}
```

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      error: null,
      isLoaded: false,
      items: []
    };
  }

  componentDidMount() {
    fetch("https://api.example.com/items")
      .then(res => res.json())
      .then(
        (result) => {
          this.setState({
            isLoaded: true,
            items: result.items
          });
        },
        // Note: it's important to handle errors here
        // instead of a catch() block so that we don't swallow
        // exceptions from actual bugs in components.
        (error) => {
          this.setState({
            isLoaded: true,
            error
          });
        }
      )
  }

  render() {
    const { error, isLoaded, items } = this.state;
    if (error) {
      return <div>Error: {error.message}</div>;
    } else if (!isLoaded) {
      return <div>Loading...</div>;
    } else {
      return (
        <ul>
          {items.map(item => (
            <li key={item.name}>
              {item.name} {item.price}
            </li>
          ))}
        </ul>
      );
    }
  }
}
```
