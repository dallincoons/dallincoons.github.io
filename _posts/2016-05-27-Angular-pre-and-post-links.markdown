---
title: Angular Pre and Post links

---

Do you use link functions in Angular directives? Me too. But sometimes that's not always the best tool for the job.

For a fantastic explanation of the difference between link, compile, pre, and post, I recommend [this](http://www.jvandemo.com/the-nitty-gritty-of-compile-and-link-functions-inside-angularjs-directives/) (yes this is a cop-out). To summarize, in case you're too lazy to read that: *Pre* and *post* links are useful when you have directives nested inside directives.

Use the *pre link* function when you want to run code in the parent directive __before__ the child directive gets compiled. If you use post link function, all the child directives will be compiled
first before the parent. 

In my case, I'm working with a third party directive (namely, Angular Ui Grid). Angular UI grid doesn't provide a server side implementation for filtering and sorting and so I wanted to wrap it in my own directive so that before Angular Ui grid ever gets compiled, my wapper directive will add that functionality to my scope.

The problem with this approach is that Ui Grid would run before I ever had a chance to add the functionality. After the Grid runs, it's too late to add this functionality. 

The reason why this didn't work is because I was using the *link* function, which acts as a post link function, so the child directives were running before the parent. 

I solved this by adding my modification in the pre link function.