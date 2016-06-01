---
title: Angular Pre and Post links

---

Do you use link functions in Angular directives? Me too. But sometimes that's not always the best tool for the job.

For a fantastic explanation of the difference between link, compile, pre, and post, I recommend [this](http://www.jvandemo.com/the-nitty-gritty-of-compile-and-link-functions-inside-angularjs-directives/) (yes this is a cop-out). To summarize, in case you're too lazy to read that: *Pre* and *post* links are useful when you have directives nested inside directives.

Use the *pre link* function when you want to run code in the parent directive __before__ the child directive gets compiled. If you use post link function, all the child directives will be compiled
first before the parent. 

In my case, I'm working with a third party directive (namely, Angular Ui Grid). I wanted to add some functionality to it. My backend expects a string to be passed to it when I'm sorting or filtering the grid data. It makes sense that Ui Grid doesn't provide functionality for this because everybodies backend will have a different implementation. However I found myself writing the same logic over and over every time I wanted to implement sorting or filtering.

My solution was to wrap the Ui Grid directive in my own directive, where I can add this feature before Ui Grid runs. 

The problem I encountered was Ui Grid would run before I ever had a chance to add the configuration for this functionality. That's because I was using the *link* function, which acts as a post link function, hence why the child directives were running before the parent. 

I solved this by adding my modification in the pre link function.