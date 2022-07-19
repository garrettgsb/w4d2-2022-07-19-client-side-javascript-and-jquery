Okay so you want to read JSON from an HTTP endpoint and use it in your client-side app. No problem. In Express (which you aren't writing for Tweeter, it's just provided to you), the endpoint will look something like this:

```
app.get('/tweets', (request, response) => {
  response.json(tweets);
  // Equivalent to: response.send(JSON.stringify(tweets));
})
```

That means that instead of sending you an HTML page, the server is going to send you a JSON string.

> FYI: `JSON.stringify(something)` to turn a Javascript value into a string; `JSON.parse(something)` to turn a JSON string back into a Javascript value.

To use the response from this endpoint in your client-side code, you'll need to use some kind of `fetch`-like function to make an AJAX request. "AJAX" stands for "asynchronous Javascript and XML," which just means "A request that's made by Javascript that doesn't require reloading the page."

jQuery has some fetch-like functions... See:

* https://api.jquery.com/jQuery.ajax/
* https://api.jquery.com/jQuery.get/
* https://api.jquery.com/jQuery.post/
* https://api.jquery.com/category/ajax/

We demoed with the regular built-in browser fetch though. Here's what that looked like:

```
fetch('/tweets')
  .then(res => res.json())
  .then(tweets => doSomethingWith(tweets));
```

Your `doSomethingWith` function would be where all the magic happens: Build a Tweet Object out of HTML and stuff and render it.

Or, the minimal example that we used to just plop the data into the bottom of the page:

```
fetch('/tweets')
  .then(res => res.json())
  .then(tweets => tweets.forEach(tweet => document.querySelector('body').append(tweet));
```

> Note: The step that's like `.then(res => res.json())` is specific to the built-in browser fetch. With jQuery fetch (or Axios or whatever), it will be a little different: You won't need that part, and in fact, it will probably error if you try to use it.
