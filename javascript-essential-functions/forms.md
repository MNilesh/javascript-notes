# Javascript Handling Form


## Accessing querystrings

We want to access the query string __name=Neil__
```
url = https://www.mywebsite.com/index?name=Neil
```

```
  const searchParams = new  URLSearchParams(window.location.search);
  let name = searchParams.get('name');  //Neil
```

To set a value to the queryString String

```
searchParams.set('age', 25);
```

If we pass an object to __URLSearchParams__ , it converts them to queryString.

```
const searchParams = new  URLSearchParams({
  name:'Neil',
  isA:'Entrepreneur',
  age:'27'
  
});
```
