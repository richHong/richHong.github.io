---
layout: post
title:  "Recursion"
date:   2016-02-25
categories: javascript recursion
---

What is Recursion?
---
Recursion is an important programming technique where a function calls itself repeatedly until it arrives at the desired result. It can be considered a type of looping. It is a concept that is not easily understood when first introduced. The classic example is the factorial problem. The factorial of n is the product of all positive integers less than or equal to n. See the code snippet below.

{% highlight js linenos %}
var factorial = function(n) {
  if (n === 0){
  return 1;
  }
  return n * factorial(n-1);
};
{% endhighlight %}

We can see on line 5, that we are calling factorial within itself, but we are calling it on (n-1). The function will essentialy trickle down positive integers until it reaches 0. So for instance, if n where equal to 5, the function will return 5 * factorial(n-1), which will return 5 * 4 * factorial(n-1) and so on... until we end up with 5 * 4 * 3 * 2 * 1. When n gets down to 0, the function returns 1 resulting in the product of 120 * 1.

The Recursive Case and the Base Case
---
The two requirements for a recursive function are a base and a recursive case. The recursive case in the factorial problem is the looping part of the function on line 5 where we are calling itself on (n-1). The base case is where we want the recursion to stop. In the factorial problem, the base case is when n is equal to 0. At this point, we are now breaking out the loop and returning 1 instead of recursing the factorial function. Without a base case, there is the danger of having an infinite loop.

_.flatten
---
Let's take a look at a more complex example with the underscore function, _.flatten. Flatten will take a nested array and put all elements on one level. See the code snippet below.

{% highlight js linenos %}
var _.flatten = function(nestedArray, result) {
  if (result === undefined) {
    result = [];
  } 
  nestedArray.forEach(function(element) {
    if (!Array.isArray(element)) {
      result.push(element);
    } else {
      flatten(element, result);
    }
  });
  return result;
};
  {% endhighlight %}

If we did not have recursion, we would have to create a for loop for each level of nesting. If the element is very deeply nested, we run into problems very quickly. But since we are able to use recursion, it can simplify the process by looping through each nest of the array until an element is found. On line 6 and 7 we see our base case and on line 9 we see our recursive case. 

So there you have it! You now have a better understanding of recursion.