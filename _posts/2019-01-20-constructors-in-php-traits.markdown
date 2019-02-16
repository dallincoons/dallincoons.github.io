---
title: Constructors in Traits
---

Traits are a handy way for sharing functionality in multiple classes, and since php doesn't support multiple inheritance, this is the next best thing. But of course, like most tools, there are a myriad of ways in which traits can be abused. 

Sometimes I come across constructor functions inside of traits. My advice is, just don't it. As a companion to the theoretical arguments such as constructors 'should be specific to a class to which they belong', I'll offer a specific, practical reason. 

When you put a constructor in a trait, you've made it much more impractical to do something like:

```php
public function __construct(param1, param2)
{
   parent::__construct(param1)
}
``` 

Sure, I supposed you could add a parent constructor call to the trait, but you don't really have any way of knowing what that parent will be. You'll make your life easier by always keeping constructors out of traits.


