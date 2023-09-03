---
layout: post
title:  Exception Handling in Promises
read: 6
post-image: /assets/images/posts/10_promise_exception/post.jpg
description: How to handle exceptions in JavaScript promises
categories: software development
---

---

![](/assets/images/posts/10_promise_exception/post.jpg)


## Introduction to promises {#promise}

A **promise** is a special JavaScript object returned by an asynchronous function. At the time it is returned to the caller, generally the operation is not finished. However, the `Promise` object provides methods to handle the eventual completion or failure of the operation.

Imagine a function `doSomething()` that takes in an input parameter `input` and two callback functions, `successCallback` and `errorCallback` -- `doSomething(input, successCallback, errorCallback)`. The callback functions are called when the operation is successful and when there is an error respectively.

Using a promise, `doSomething()` can be rewritten to return a `Promise` object as such:

{% highlight javascript %}

function doSomething(input) {
    return new Promise(resolve, reject) {
        // your logic here...
    }
}

doSomething(input)
    .then(successCallback, errorCallback);
{% endhighlight %}

The `then` method is a method of the `Promise` object that takes in two optional parameters -- two handlers to deal with the success and failure of the promise. The first handler is the resolve handler that handles a resolved promise (when the promise is successful). The second handler is the reject handler that handles a rejected promise (when the promise is not successful).

An advantage of a promise is that it allows you to chain operations together so that they run sequentially, instead of nesting another operation within the `successCallback`. This is because the `then` method returns a new `Promise`, for which the `then` method can be called again on this new promise to perform another operation.

In other words, instead of:

{% highlight javascript %}
doSomething(input, function (result) {
    doSecondThing(result, function (secondResult) {
        doThirdThing(result, errorCallback);
    }, errorCallback);
}, errorCallback);
{% endhighlight %}

you can do:

{% highlight javascript %}
doSomething(input)
    .then(doSecondThing, errorCallback)
    .then(doThirdThing, errorCallback)
    .catch(errorCallback);
{% endhighlight %}

which is arguably neater and easier to read. Note the [`catch` method](#catch) which we will get to in a second.

## Exception handling {#exceptionhandlng}

Exceptions can happen in promises, just like anywhere else in a program. How do we handle exceptions in promises?

There are 2 built-in ways to do so.

### 1. Reject handler {#rejecthandler}

As mentioned above, a reject handler is a function passed into the `then` method to handle rejected promises.

In each link of the chain, exceptions are handled by the reject handler in the subsequent link. Take the promise chain below. An exception in link 1 will be handled by the reject handler in link 2 (`rejectHandler1`). An exception in link 2 will then be handled by the reject handler in link 3 (`rejectHandler2`), and so on.

{% highlight javascript %}
doSomething(input)                           // link 1
    .then(doSecondThing, rejectHandler1)     // link 2
    .then(doThirdThing, rejectHandler2)      // link 3
    .catch(rejectHandler3);                  // link 4
{% endhighlight %}

Once the exception is handled, the rest of the chain continues.

Note that not each link requires a reject handler since it is optional to pass in a reject handler to the `then` method. In the event where the reject handler is not defined, the `then` method will use its default reject handler, which rethrows the exception: `(err) => {throw err;}`. The exception will then be handled by the reject handler in the subsequent link. In the example below, exceptions in links 1 and 2 are handled by `rejectHandler2`, because there is no reject handler defined in link 2.

{% highlight javascript %}
doSomething(input)                           // link 1
    .then(doSecondThing)                     // link 2
    .then(doThirdThing, rejectHandler2)      // link 3
    .catch(rejectHandler3);                  // link 4
{% endhighlight %}

This means that:

> An exception in a chain will be handled by the first reject handler it sees down the chain.

### 2. `catch` method {#catch}

In a chain with multiple links, the reject handler could be the same for all links. In this case, you can use the `catch` method:

{% highlight javascript %}
doSomething(input)
    .then(doSecondThing)
    .then(doThirdThing)
    .catch(rejectHandler);
{% endhighlight %}

The `catch` method is a method of the `Promise` object. It is effectively the `then` method with only the reject handler passed in, i.e. `then(null, rejectHandler)`. With the `catch` method, exception in every link above it is handled by the `catch` block.

Note that you may use the `catch` method in the middle of a chain but this is not a good practice as any exceptions from the links below the `catch` method are not taken care of.

{% highlight javascript %}
doSomething(input)
    .then(doSecondThing)
    .catch(rejectHandler);
    .then(doThirdThing)
{% endhighlight %}

## Comparison

There are differences between the two methods. The most significant one is:
- in method 1, the exception is handled immediately in the chain. Once handled, the chain continues. 
- in method 2, the exception is caught at the end of the chain and handled immediately but the links between the failed link and the `catch` block are skipped.

In most cases, you would like to skip the chain when an exception occurs because subsequent links in the chain rely on the results from the links above. In such cases, the `catch` method will be beneficial. 

However, sometimes, you may want the rest of the chain to continue to run regardless of an exception in a particular link. Or, you may need to handle the exception from a particular link differently from the rest of the chain. In these cases, defining a reject handler in the subsequent link will be useful. Note that both methods are not mutually exclusive. Therefore, a catch block can then be put at the end of the chain to handle any exceptions that might still happen after that link.

{% highlight javascript %}
doSomething(input)
    .then(doSecondThing, rejectHandler1)    // handle err from doSomething
    .then(doThirdThing)
    .then(doFourthThing)
    .catch(rejectHandler2);                 // handle err from links 2-4
{% endhighlight %}

# Conclusion

It is good practice to handle exceptions properly. In promises, there are two ways to handle exceptions: using reject handlers, and using the `catch` method.

> An exception in a chain can be handled by the first reject handler it sees down the chain or by a catch block at the end.
   
---

**Author**: <a href="https://github.com/andreusjh99" target="_blank">Chia Jing Heng (andreusjh99)</a>