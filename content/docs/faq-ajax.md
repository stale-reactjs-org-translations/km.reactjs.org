---
id: faq-ajax
title: AJAX and APIs
permalink: docs/faq-ajax.html
layout: docs
category: FAQ
---

### តើខ្ញុំអាចហៅ AJAX មកប្រើតាមរបៀបណា? {#how-can-i-make-an-ajax-call}

ជាមួយ React អ្នកអាចប្រើ AJAX library មួយណាក៏បានតាមដែលអ្នកចង់ប្រើ។ ខាងក្រោមនេះ គីជាlibrary មួយចំនូនដែលត្រូវបានគេប្រើប្រាស់ច្រើនក្នុងពេលបច្ចុប្បន្ន៖
  1. [Axios](https://github.com/axios/axios)
  2. [jQuery AJAX](https://api.jquery.com/jQuery.ajax/)
  3. [window.fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) (ដែលជាមុខងារ មានស្រាប់ក្នុងកម្មវិធីសម្រាប់បើកវែបសាយ(browser))

### តើខ្ញុំគួរហៅAJAX មកប្រើនៅក្នុងវដ្ដណាក្នុង Component lifecycle? {#where-in-the-component-lifecycle-should-i-make-an-ajax-call}

អ្នកគួរតែធ្វើការលើទិន្នន័យជាមួយ AJAX នៅក្នុង lifecycle method ឈ្មោះ [`componentDidMount`](/docs/react-component.html#mounting)។ វិធីនេះធ្វើឲ្យអ្នកអាចប្រើប្រាស់method `setState` ដើម្បីupdate componentរបស់អ្នក នៅពេលទិន្នន័យត្រូវបានទាញយកមកប្រើ។

### ឧទាហរណ៏: ការប្រើប្រាស់លទ្ធផលទិន្នន័យដែលបានពី AJAX ដើម្បី set តម្លៃអោយstateក្នុងlocal {#example-using-ajax-results-to-set-local-state}

Componentខាងក្រោមនឹងបង្ហាញពីរបៀបហៅ AJAX មកប្រើក្នុងmethod `componentDidMount` ដើម្បីធ្វើការលើ state component ក្នុង local។

ខាងក្រោមជាឧទាហរណ៏របស់APIដែលផ្ដល់ JSON object តែមួយមានសណ្ឋានដូចនេះ៖

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

Here is the equivalent with [Hooks](https://reactjs.org/docs/hooks-intro.html): 

```js
function MyComponent() {
  const [error, setError] = useState(null);
  const [isLoaded, setIsLoaded] = useState(false);
  const [items, setItems] = useState([]);

  // Note: the empty deps array [] means
  // this useEffect will run once
  // similar to componentDidMount()
  useEffect(() => {
    fetch("https://api.example.com/items")
      .then(res => res.json())
      .then(
        (result) => {
          setIsLoaded(true);
          setItems(result);
        },
        // Note: it's important to handle errors here
        // instead of a catch() block so that we don't swallow
        // exceptions from actual bugs in components.
        (error) => {
          setIsLoaded(true);
          setError(error);
        }
      )
  }, [])

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
```
