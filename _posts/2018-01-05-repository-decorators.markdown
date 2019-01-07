---
title: Using the decorator design pattern with repositories 
---

I recently encountered something in the legacy app I'm working in, where the author added caching to at least a dozen or so repositories. The worst part of this is that the person who added the caching funtionality went back through all the repositories and commented it out for some reason (apparently the caching just wasn't working out).

With a little bit of design pattern know-how, this process could be simplified, and concerns could be separating which would adhere better to the Single Responsiblity Principle. Here's what I mean. Instead of caching data in here:

```php
class SomeRepository
{
   public function all()
   {
      //get stuff 
      //cache stuff
   }
}
```

We could create a 'decorator' object around it

```php
class SomeRepository
{
   public function all()
   {
      //get stuff
   }
}

class SomeRepositoryCacheDecorator
{
   protected $repository;

   public function contruct(SomeRepository $repository)
   {
      $this->repository = $repository;
   }

   public function all()
   {
      $stuff = $this->repository->all();
      //cache stuff
      return $stuff;
   }
}
```

And now, when you bind your repository in the IOC container, just wrap it in the decorator:

```php
$this->app->bind(SomeRepositoryInterface::clsss, function () {
    return new SomeRepositoryCacheDecorator(new SomeRepository());
});
