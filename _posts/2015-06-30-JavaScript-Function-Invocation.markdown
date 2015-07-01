---
layout : post
title : "Java Script Invocation Pattern"
author : Jimmy Chen 
date : 2015-06-30 23:04:00
categories : jekyll update
---

There are four patterns in JavaScript : the method invocation pattern , the function invocation pattern , the constructor invocation pattern , and the apply invocation pattern.The patterns differ in how the bonus parameter this is initialized.

The Method Invocation Pattern 

When a function is stored as property of an Object ,we call method. When a method is invoked,this is bound to that object . If an invocation expression contains a refinement(that is , a . dot expression or [subscript] script),it is invoked as a method:
{% highlight javascript %}
var myObject = {
	value : 0,
	increament : function(inc){
	this.value += typeof inc === "number" ? inc : 1;
	}
};
myObject.increment();
myObject.increment(2);
{% endhighlight %}
A method can use this to access the object so that it can retrieve values from the object or modify the object. The binding of this to the object happens at invocation time.This very late binding makes functions that use this highly reusable. Methods that get their object context from this are called public methods.

The Function Invocation Pattern

When a function is not the property of an object , then it is invoked as a function:
{% highlight javascript %}
var sum = add(3,4);
{% endhighlight %}
When a function is invoked with this pattern , this is bound to the global object. This was a mistake in the design of language . Had the language been designed correctly , when the inner function is invoked ,this would still be bound to the this varialbe of the outer function . A consequenece of this error is that a method cannot employ an inner function to help it do its work because the inner function does not share the method's access to the object as its this is bound to the wrong value . Fortunately, there is an easy workaround . If the method defines a variable and assign it the value of this , the inner function will have access to this through that variable . By convention.the name of that variable is that : 
{% highlight javascript%}
myObject.double = function(){
	var that = this;
	var helper = function(){
		that.value = add(that.value , that.value);
	};
	helper();
}
myObject.double();
{% endhighlight%}

The Constructor Invocation Pattern

JaveScript is a prototypal inheritance language. That means that object can inherit properties directly from other objects . The language is class-free .
This is a radical departure from the current fashion . Most languages today are classical. Prototypal inheritance is powerfully expressive, but is not widely understood.JavaScript itself is not confident in its prototypal nature, so it offers an object-making syntax that is reminiscent of the classical languages. Few classical programmers found prototypal inheritance to be acceptable, and classically inspired syntax obscures the language's true prototypal nature. It is the worst of both world.
If a function is invoked with the new prefix , then a new  Ojbect will be created with hidden link to the value of the function's prototype member, and this will be bound the that new object.
The new prefix alse change the behavior of the return statement . We will see more about the next.
{% highlight javascript%}
var  Quo = function(string){
	this.status = string;
};
Quo.prototype.get_status = function(){
	return this.status;
};
var myQuo = new Quo("confused");
console.log(myQuo.get_status());
{% endhighlight%}
Functions that are inherit to be used with the new prefix are called constructor. By convention, they are kept in variables with capitalized name. If a constructor is called without the prefix , very bad thing can happen without a compile-time or runtime warning, so the capitalization convention is really important.
Use of this style of constructor is not recommended. We will see better alternatives in next chapter.

The Apply Invocation Pattern

Because JavaScript is a functional object-oriented language. function can have method.
The apply method let us construct an array of arguments to use to invoke a function . It also lets us choose the value of this. The apply method takes two paramenters. The first is the value that should be bound to this . The second is an array of parameters.

