---
layout: post
title: A Quick Summary of How Ruby is Interpreted
---

In light of the new Just-In-Time compiler that was added to Ruby 2.6, I would like to give a very brief summary of how Ruby is interpreted and the changes that the new JIT compiler makes.

Here is a flowchart which goes over the main steps by which Ruby is interpreted from Ruby script to binary code.  I will not cover what binary code is or what the difference is between interpreted vs compiled languages in this post.  However if you would like to learn more about those subjects I suggest these posts: [How Does a Computer Physically Store Binary Code?](http://androidgrl.github.io/2019/01/01/binary/), and [A Deeper Inspection Into Compilation And Interpretation](https://dev.to/vaidehijoshi/a-deeper-inspection-into-compilation-and-interpretation-8bp).

![interpretation](/public/RubyInterpretation.png)

As shown in the chart, Ruby is interpreted in four steps:

1. Ruby script is "tokenized" into tokens.
2. The tokens are "parsed" into Abstract Syntax Tree nodes.
3. The AST nodes are "compiled" into YARV byte code.
4. YARV byte code is "evaluated" into binary code.

Steps 1-3 take up about 30% of Ruby's run time.  With the inclusion of Bootsnap in Rails 5.2, YARV byte code is cached, so that the parsing and compiling steps do not have to be repeated if the same Ruby code is run again.

Step 4, the evaluation of YARV byte code into binary code takes up about 70% of Ruby's run time.  With the inclusion of the optional YARV-MJIT compiler in Ruby 2.6, binary code is cached, so that the evaluation step does not have to be repeated the second time the interpreter sees the same YARV instructions.

For a more detailed explanation of the information summarized here see Shannon Skipper's blogpost [Ruby's New JIT](https://medium.com/square-corner-blog/rubys-new-jit-91a5c864dd10).

