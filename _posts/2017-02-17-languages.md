---
layout: post
title: What Makes a Language Fast?  Five Factors That Affect a Programming Language's Speed
---

Often I have heard that Ruby is a slow language compared to other languages like Go and Elixir.  I have also heard of startups that originally build their apps on Rails but after hitting it big need to switch to a language like Java in order to scale up.  What are the factors that determine whether a language is considered fast?  How do companies choose which language is most appropriate for their application?  This blog will cover these five factors, a brief overview of how a language is run on your computer processor, and some considerations that go into deciding what is an optimal language for a particular end use.

__The Five Main Factors__:

__Asynchronous__

A language that can be asynchronous can be much faster than a synchronous one.  Let's say that I want to bake a cake and wash the dishes.  If I put the cake in the oven, wait for it to bake, then wash the dishes, that is synchronous.  There is a little time lost waiting for the cake to bake and doing nothing.  This is how Ruby works, it waits for something to be completely done before starting something else.  Now let's say that I put the cake in the oven, and while it bakes I do the dishes thereby cutting the overall time to do both tasks.  That is asynchronous.

Javascript is a language that is good at asynch.  One example of how Javascript uses asynch is when a number of api calls are made to a backend to get a bundle of information.  Instead of waiting for each call to get it's response before making the next one, it can make other calls while it is waiting for previous ones.  If all the calls are necessary to perform an action, then a "promise" can be made which means it will wait for all the calls to complete before performing the action.

__Multithreaded__

Let's say that I decided to ask my friend to wash the dishes while I baked a cake.  That is multithreading.  I doubled the working power by asking my friend to help.  Likewise multithreaded languages can spin up multiple "threads" to perform multiple tasks at once.

Java and Elixir are capable of multithreading while Ruby and Javascript are not.

__Static Typed__

A statically typed language is one in which you have to define what data type a variable is.  For example in Java, if you set a variable to be an array, you have to specify that it is an array.  Ruby on the other hand is dynamically typed.  You don't have to specify that a variable is any particular data structure, and you can even change what it is at any time.  Although a dynamically typed language can be great to build something quickly, it runs slower than a statically typed language.  This is because a statically typed language knows exactly how much memory to allocate to a variable because it knows exactly what kind of data type it is.  A dynamically typed language on the other hand must allocate a greater amount of memory to store a variable because it doesn't know what it will be.  Less memory usage results in greater speed.

__Functional__

A functional language is the opposite of an object-oriented language.  Elixir is a functional language, in which everything is based on functions not objects.  Ruby is an object-oriented language because everything in Ruby including simple things like numbers and strings are objects.  Objects take up a lot of memory and therefore an object-oriented language will be slower.

__Compiled__

All languages at the end of the day need to be translated into byte code for your computer's processor.  Some languages like Java and Elixir pre-compile themselves into an intermediate form of byte code that is one step closer to processor byte code.  This extra step makes it easier for the language to be translated into processor byte code, resulting in a faster language.  A language such as Ruby or Python are not compiled but are "interpreted".  Interpreted just means that it does not go though the pre-compiling step, and has to be directly interpreted into processor byte code which requires more work and is therefore slower.  Still faster yet is C which can compile directly into processor byte code skipping the intermediate step.  A language that is directly compiled into processor byte code is called a "natively compiled" language.

Here is a chart summarizing four popular languages and their characteristics:

![Chart](./public/chart.png)

Lastly, how do you choose which language is good for your app?  When choosing a language it is important to consider what the app is being used for.  For example, math computations are run on the computer's processor.  Therefore apps that do a lot of math computations will run faster with a natively compiled language because it won't be slowed down by pre-compiling or interpretation.  Apps that have a relatively few numbers of users but need to wait for multiple api calls to perform a function, would benefit from an asynchronous language.  Apps that have millions of users trying to request a webpage all at once will benefit from a multi-threaded language.  An app that is for a startup which doesn't have a lot of users yet and needs to be built quickly would do well with Ruby.

In summary the five characteristics that can increase the speed of a language are: Asynchronious, Multi-Threaded, Statically-typed, Functional, and Compiled.  When choosing a language it is good to consider what the app is being used for.

A special thanks to Alex Jensen and Adam Zaninovich for their help in explaining these concepts to me.
