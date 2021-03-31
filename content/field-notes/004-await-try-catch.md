---
title: "Async Try/Catch Control Flow"
slug: 4
author: "Adam Hawkins"
date: 2021-03-30T21:24:42-10:00
---

Some situations require returning a value from a try catch block that
includes an `async` function. This typically happens in my code when
calling an external service, then having to catch an error to return a
specific value (say an expected `404 Not Found` to return `null`) or
throw a different type of error (i.e. defining my own APIs).

I prefer to use `const` wherever possible. The problem is that a
structure like:

```javascript
try {
  const data = await doSomething();
} catch (error) {
  // error handling
}

// use data
```

Does not work due to scoping. One alternative is using `await` with a
a `catch` on the promise. This structure allows assigning a value and
catching errors in a single expression.

```javascript
const data = await doSomething().catch((error) => {
  if (error.name === "SomethingToHandle") {
    // process error.
  } else {
    throw error;
  }
});
```

This seems nicer than something like:

```javascript
let data;

try {
  data = await doSomething();
} catch (error) {
  if (error.name === "SomethingToHandle") {
    // process error.
  } else {
    throw error;
  }
}

// use data
```

I think this structure only works if `catch` function intends to
`throw` the error again. If a specific error is allowed, then a
another Promise is required like so:

```javascript
const data = await new Promise((resolve, reject) => {
  return doSomething.then(resolve).catch((error) => {
    if (error.name === "SomethingRecoverableError") {
      resolve(null);
    } else {
      reject(error);
    }
  });
}).catch((error) => {
  if (error.name === "SomethingToProcess") {
    // process error.
  } else {
    throw error;
  }
});
```

I admit the last example is difficult to read. Personally I'd need a
double take if I encountered it in the wild. Such is life when errors
must be caught either for recovery or to be rethrown in some way.

Personally, I'd like it if JS had something like Ruby's arbitrary
begin blocks with return values and error handling for these cases.
Return errors ala Golang is another (albeit entirely different)
approach.
