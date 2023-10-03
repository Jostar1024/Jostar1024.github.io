---
layout: post
title:  "The Philosophy of Software Design Book Review"
date:   2023-10-03 18:00:00 +0800
categories: book design 
---

Writing software is hard, why? The Philosophy of Software Design is the book that tells you why. The book is about the complexity of software and how the programmers can deal with it. There are 5 things I think need to be noted.


# What is complexity ?

Software with complexity is a software that is not easily modified or understood by others. Software is continuously developed by many people, complexity is therefore incremental.

Complexity manifests itself in three ways: change amplification, cognitive load, unknown unknown. Unknown unknown is a good word for memorization, but not for understanding.  I found another word that makes a lot of sense: unimaginable unknown. It&rsquo;s unimaginable what kind of difficulties you&rsquo;ll have when you start a new project.

One of the causes of complexity is code dependencies. Dependencies are unavoidable and cannot be removed. However, we could manage the dependencies, by creating a clear and obvious interface, and hiding the implementation details. For example, if I&rsquo;m developing a microservice, and the other microservice want to use our data, should I just give it the access to the Database and let it query the DB directly? No. We should add a new API endpoint for retrieving the data so that other microservices depend on the API endpoint. This dependency allows me to control who can use this API, what can be modified, which DB we choose. As long as other services depend on the API endpoint, we can migrate to a different Database without worrying about impacting other services.


# Design is crucial and design should be done twice.

Design is a step before writing the actual code. The goal of the design step is to figure out what to write and how the newly written code fits into the current codebase. Without this step, the programmer is likely to write the code that works for now, and only solve the current problem with a workaround. Soon the workarounds pile up, the complexity increases, and the code becomes difficult to change. Experienced programmer knows that working code isn&rsquo;t enough and would design for the future not just present.

The recommended way for design step is to write comments. When designing a new feature, write comments about the design process, design choices, use cases etc. Also, the comment is the informal part of the interface describing the things that are not in the code.

Some people might ask why not just read the code? There are several reasons:

1.  Code reflects what you did, not why.
2.  If the module is deep, reading the module&rsquo;s source code would be a waste of time to just use the module.
3.  The user of the module should only read the interface inputs, outputs, and the comments to know what the module does. For example, I don&rsquo;t need to read the whole Linux file system source code to understand what the API does, the code tells me the details not the design and how I can use it.

When designing, always think about a second solution, or more solutions. When comparing each solution about what the pros and cons and the programmer can make a better decision.


# Write deep module

When facing complexity, the first thing we want to do is to get rid of it. But if you can&rsquo;t get rid of the complexity, you hide it. One way to hide complexity is through modular design, where each module consists of the interface and the implementation. The user of the module should only know the interface, while the maintainer of the module takes care of the implementation details. Ideally, the user gets the high-level understanding by looking at the interface and reading the interface documents. The Linux File System API is a perfect example. I never notice the complexity within the API.


# Define errors out of existences.

When we write the software&rsquo;s happy path, we think of only one case, under one set of data, and we deploy the program. But as we continue to develop the software, more data and edge cases appear, the software may crash, we need to handle the error. The easiest way is to add a special handling for this case(a try catch). But we should first consider the whole design of the program (maybe even further the whole business), can we get rid of this kind of error by design or redesign? If we can and the redesign simplifies the overall logic, we should probably use the redesign.


# Choose a good names

Naming is a kind of abstraction, giving the reader a simplified view of a complex implementation. We have many names that we can understand without a second thought: process, function, hashmap etc. When writing business logic, it&rsquo;s hard to choose a good name. My experience with naming is to name the function or variable with a concrete meaning, such as `blog_that_has_comments`


That&rsquo;s it! I&rsquo;d recommend a programmer to read this book.

