---
title: My favorite reason to use the repository pattern
---

Not everyone is in love with the [Repository Pattern](https://martinfowler.com/eaaCatalog/repository.html), which is understandable, because it has a way of complicating things and adding a lot of seemingly unneccessary code, especially in small, [Active Record](https://www.martinfowler.com/eaaCatalog/activeRecord.html) style apps.  And you know what? I actually agree in a lot of cases. It can be overkill depending on what you're working on. You'll rarely if ever find me purporting a "one size fits all" solution.

That being said, let me tell you my favorite reason to use the Repository Pattern: it can dramatically speed up your tests.

A repository can be seen as simply a collection of data records. Where the data is stored isn't important, that's merely an implimentation detai, which is the whole point of repositories. That means that our app doesn't know or care how the data is being store, it just knows that it's being stored somewhere. You could have a simple in-memory repository that has the same methods as a repository that is backed by a database and your code treats it all the same.

When it comes to testing, loading up a framework and spinning up a database instance are all things that slow down tests. When tests are slow, we tend to not want to run our tests, and if we're not running our tests there's no point in writing them, and now we're back to being like 90 percent of the programming world and we've lost our super powers.  

Or, we can create a "fake" repository which implements the same interface and has the same outward behavior as a "real" repository, but everything happens without a database. For example it stores, updates, and deletes records, but it can use just an array to store data records.
 
When you're writing tests, you can inject your fake repository where a real repository normally goes (hopefully you're coding to an interface), and now your tests no longer require a database to run.

Additonally, you can write a test that tests both your real repository and your fake repository, for the purposes of verifying that both have the exact same outward behavior, which allows you to use them interchangeably. Atfirst it seems weird to test a "fake" class, but you'll get used to it. Enjoy your blazingly fast tests!
