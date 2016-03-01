---
layout: post
title:  "Recursion"
date:   2016-02-25
categories: javascript
---

What is Recursion?
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Recursion is an important programming technique where a function can call itself repeatedly until it arrives at the desired result. It can be considered a type of looping. Recursion is a concept that is not easily understood when first introduced to beginning programmers. The classic example is the factorial function. The factorial of n is the product of all positive integers less than or equal to n. See the code snippet below.

{% highlight javascript linenos %}
var factorial = function(n) {
  if (n === 0){
    return 1;
  }
  return n * factorial(n-1);
};
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;On line 5, we are calling factorial within itself, however we are calling it on (n-1). The function will essentially tumble down positive integers until it reaches zero. So for instance, if n where equal to 5, the function will return 5 * factorial(n-1) which will return 5 * 4 * factorial(n-1) and so on... until we end up with 5 * 4 * 3 * 2 * 1. When n gets down to zero, the function returns 1 resulting in the answer of 120.

The Recursive Case and the Base Case
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The two requirements for a recursive function are at least one recursive case and at least one base case. The recursive case in the factorial function is the looping part of the function on line 5 where we are calling itself on (n-1). The base case is where we want the recursion to stop. In the factorial function, the base case is when n is equal to 0 on line 2. At this point, we are now breaking out the loop and returning 1 instead of recursing. Without a base case, there is the danger of having an infinite loop.

_.flatten
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Let's take a look at a more complex example with the underscore function, _.flatten. This function will take a nested array and put all elements on one level. For instance the array, [[3, 4], [5, 6]], would have a flattened array of [3, 4, 5, 6]. See the code snippet below.

{% highlight javascript linenos %}
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

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If we did not have recursion, we would have to create a for loop for each level of nesting. If the element is very deeply nested, we run into problems very quickly. But since we are able to use recursion, it can simplify the process by looping through each nest of the array until an element is found. Starting on line 6, we see our base case which checks for the presence of an array, and pushes the element into the result array. On line 9, we see our recursive case, which will call the _.flatten function on any arrays found. 

So there you have it! You now have a better understanding of recursion.