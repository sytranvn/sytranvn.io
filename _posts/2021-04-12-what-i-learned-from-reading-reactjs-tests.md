---
layout: post
title: What I learned from reading reactjs tests
category: reactjs
tags: reactjs
---

First of all, I think React DOM is one of the most interesting part in React code base. I'm not sure if it is correct but whatever, stop thinking and start diving.

This is the [React-DOM test file](https://github.com/facebook/react/blob/9d48779b362ef773da50fef95af6998b560c75c0/packages/react-dom/src/__tests__/ReactDOM-test.js) at the time I'm writing this post. If you find latest version is different from what mentioned in this post please feel free to make a PR.

- `ReactDOM`  
    - `should bubble onSubmit`  
    So we can listen an `onsubmit` event on a `div`. That's crazy right? Most of the time we only listen this event on a `form` but in fact any tag can listen to this event if it has a form children.
    - `should overwrite props.children with children argument`  
    So for example if we have `<Component children={'real'}>fake</Component>`. We will get `fake` as result.
    - `throws in render() if the update callback is not a function`  
    `ReactDOM.render` supports an optional `callback` parameters to be called after component is mounted into container. I look for [actual implementation](https://github.com/facebook/react/blob/dd8552ae0d82afed66fec649ee5c044c69c65e92/packages/react-dom/src/client/ReactDOMLegacy.js#L198-L204) and find it callback `fiberRoot` instance as `this`. So you can `console.log(this.nodeName)`  
- `ReactMount`  
    - `should unmount and remount if the key changes`  
    I have known this beavior of React key before, but it's interesting to see it actually documented in the test.
    - 