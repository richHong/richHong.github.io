---
layout: post
title:  "Inheritance"
date:   2016-03-07
categories: javascript
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In object-oriented programming, inheritance is when an object is based on another object to maintain the same behavior. In Javascript, the type of inheritance is called prototypal inheritance, where as other languages may use classes. It is very common to have multiple objects that have the same properties and methods, so having a prototype with the methods and properties we want can help us save time and not repeat code. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If we wanted to make several objects that represent different dogs, one way would be to make a function. It would assign properties and methods common to all dogs, but it would also be able to have specific parameters for that particular dog. See the code snippet below.

{% highlight javascript linenos %}
function Dog (name, breed, age){
	this.name = name;
	this.breed = breed;
	this.legs = 4;
	this.age = age;
	this.bark = function(){console.log('Ruff ruff! barked ' + this.name)};
};

var snoopy = new Dog ('Snoopy', 'beagle', 5);

console.log(snoopy);
// Dog { name: 'Snoopy', breed: 'beagle', legs: 4, age: 5, bark: [Function] }
snoopy.bark();
// Ruff ruff! barked Snoopy

var pluto = new Dog ('Pluto', 'bloodhound', 7);

console.log(pluto);
// Dog { name: 'Pluto', breed: 'bloodhound', legs: 4, age: 7, bark: [Function] }
pluto.bark();
// Ruff ruff! barked Pluto
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So by creating the Dog function we are able to create dogs using the `new` operator. This type of function is called a constructor function. In the example above we created Snoopy and Pluto. These dogs have 4 legs and a bark method, but have different a different name, age, and breed.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Next, let's make it so that all dogs are animals as well. So, let's make an animal object and give it properties that all animals should have. Using `Object.prototype`, we can assign all dog objects to have the properties of the animal object. We will set a hasFur property equal to true and add an eat method for all animals. This is just like how arrays have built in methods. There is an `Array.prototype` that new arrays inherit its methods from. See the code snippet below.

{% highlight javascript linenos %}

var animal = {hasFur: true, 
              eat:function(){console.log(this.name + ' ate a bowl of food')}
};

Dog.prototype = animal;

var spike = new Dog ('Spike', 'bulldog', 3);

console.log(spike)
// { name: 'Spike', breed: 'bulldog', legs: 4, age: 3, bark: [Function] }
console.log(spike.hasFur);
// true
spike.eat();
// Spike ate a bowl of food
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Now that all dogs are animals, let's make a new dog named Spike. Since Spike is a dog and all dogs are animals, Spike has now inherited the hasFur property and the eat method. Notice that even though Spike has inherited the properties, it is not explicitly shown in the console.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;We can also create a new dog from an existing dog. The new dog will inherit all the properties of the existing dog using `Object.create()`. See the code snippet below.

{% highlight javascript linenos %}

function puppyMaker (parent, name){
	var puppy = Object.create(parent);
	puppy.name = name;
	puppy.age = 1;
	return puppy;
}

var odie = puppyMaker(spike, 'Odie');

console.log(odie);
// { name: 'Odie', age: 1 }
odie.eat();
// Odie ate a bowl of food
odie.bark();
// Ruff ruff! barked Odie
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In this example, we are using a function called puppyMaker to make more dogs using a parent dog. Let's make another dog named Odie. Now since Spike is Odie's parent, Odie will inherit the properties of Spike. Odie can eat like all animals can and can bark like all dogs can.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So with this brief introduction, you should be able save some time and code by using inheritance.