---
uuid: 20220720091913
created: 2022-07-20T09:19:13
alias: fetch api
---

# [[Fetch API]]

The [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) provides a [[JavaScript]] interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. It also provides a global [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch)method that provides an easy, logical way to fetch resources asynchronously across the network.

## Basic fetch request
```javascript
fetch('http://example.com/movies.json')
  .then(response => response.json())
  .then(data => console.log(data));
```

Here we are fetching a JSON file across the network and printing it to the console. The simplest use of `fetch()` takes one argument — the path to the resource you want to fetch — and does not directly return the JSON response body but instead returns a promise that resolves with a [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object.

## Request options
The `fetch()` method can optionally accept a second parameter, an `init` object that allows you to control a number of different settings:

```javascript
// Example POST method implementation:
async function postData(url = '', data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: 'POST', // *GET, POST, PUT, DELETE, etc.
    
    mode: 'cors', // no-cors, *cors, same-origin
    
    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    
    credentials: 'same-origin', // include, *same-origin, omit
    
    headers: {
      'Content-Type': 'application/json'
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    
    redirect: 'follow', // manual, *follow, error
    
    referrerPolicy: 'no-referrer', // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    
    body: JSON.stringify(data) // body data type must match "Content-Type" header
    
  });
  return response.json(); // parses JSON response into native JavaScript objects
}

postData('https://example.com/answer', { answer: 42 })
  .then(data => {
    console.log(data); // JSON data parsed by `data.json()` call
  })
```

## Uploading [[JSON]] data
Use [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch) to POST JSON-encoded data.

```javascript
const data = { username: 'example' };

fetch('https://example.com/profile', {
  method: 'POST', // or 'PUT'
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(data),
})
.then(response => response.json())
.then(data => {
  console.log('Success:', data);
})
.catch((error) => {
  console.error('Error:', error);
})
```

## Uploading a file
Files can be uploaded using an HTML `<input type="file" />` input element, [`FormData()`](https://developer.mozilla.org/en-US/docs/Web/API/FormData/FormData "FormData()")and [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch).

```javascript
const formData = new FormData();
const fileField = document.querySelector('input[type="file"]');

formData.append('username', 'abc123');
formData.append('avatar', fileField.files[0]);

fetch('https://example.com/profile/avatar', {
  method: 'PUT',
  body: formData
})
.then(response =%3E response.json())
.then(result => {
  console.log('Success:', result);
})
.catch(error => {
  console.error('Error:', error);
});
```

## Uploading multiple files
Files can be uploaded using an HTML `<input type="file" multiple />` input element, [`FormData()`](https://developer.mozilla.org/en-US/docs/Web/API/FormData/FormData "FormData()") and [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch).

```javascript
const formData = new FormData();
const photos = document.querySelector('input[type="file"][multiple]');

formData.append('title', 'My Vegas Vacation');
for (let i = 0; i %3C photos.files.length; i++) {
  formData.append(`photos_${i}`, photos.files[i]);
}

fetch('https://example.com/posts', {
  method: 'POST',
  body: formData,
})
.then(response =%3E response.json())
.then(result => {
  console.log('Success:', result);
})
.catch(error => {
  console.error('Error:', error);
});
```

## Checking that the fetch was successful
A [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch) promise will reject with a [`TypeError`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError) when a network error is encountered or CORS is misconfigured on the server-side, although this usually means permission issues or similar — a 404 does not constitute a network error, for example. An accurate check for a successful `fetch()` would include checking that the promise resolved, then checking that the [`Response.ok`](https://developer.mozilla.org/en-US/docs/Web/API/Response/ok) property has a value of true. The code would look something like this:
```javascript
fetch('flowers.jpg')
  .then(response =%3E {
    if (!response.ok) {
      throw new Error('Network response was not OK');
    }
    return response.blob();
  })
  .then(myBlob => {
    myImage.src = URL.createObjectURL(myBlob);
  })
  .catch(error => {
    console.error('There has been a problem with your fetch operation:', error);
  });
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)