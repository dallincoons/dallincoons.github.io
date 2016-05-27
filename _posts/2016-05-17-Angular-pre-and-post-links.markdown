Do you use link functions in Angular directives? Me too. But sometimes that's not always the best tool for the job. 

For a fantastic explanation of the difference between link, compile, pre, and post, I recommend this (yes this is a cop-out but this author does a better job than I ever could): http://www.jvandemo.com/the-nitty-gritty-of-compile-and-link-functions-inside-angularjs-directives/

To summarize the relevant infomartion for my blog post, use the pre link function when you want to run code before the child directive gets compiled. If you use post link function, all the child directives will be compiled
first. 

In my case, I'm working with a third party directive (namely, Ui-Grid). I wanted to add some functionality to it by adding a directive.

The problem I encountered was that I needed to add a property to the scope before the Ui-Grid directive ever ran. 

I solved this by adding my modification in the pre link function.