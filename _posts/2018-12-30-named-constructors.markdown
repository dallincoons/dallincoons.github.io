---
title: Named Constructors To Make Our Lives Easier
---

Have you ever found yourself adding parameters with `null` as defaults in your constructors?

```php
class PackingSlip
{
	private $kit;
	private $kitGroup;

	public function __construct(KitInterface $kit = null, KitGroup $kitGroup = null)
	{
		$this->kit = $kit;
		$this->kitGroup = $kitGroup;
	}
}
```

This approach leads down a dark path:

```php
new PackingSlip(null, $kitGroup);
```

In other languages that support method overloading, this can be easily improved with multiple constructors. Even then
I think named constructors can be more idiomatic:

```php
class PackingSlip
{
    private __construct($model)
    {
       $this->somethingThatsHardToName = $model;
    }

    public static function forKit(KitInterface $kit)
    {
	return new self($kit);
    }

    public static function forKitGroup(KitGroupInterface $kitGroup)
    {
	return new self($kitGroup);
    }
}

PackingSlip::forKit($kit);
PackingSlip::forKitGroup($kitGroup)
```

Though in cases like this I would argue that it's better to just split up the PackingSlip class, probably into
some kind of polymorphic hierarchy. 

I like named constructors, but lately I've found myself using them as a tool for describing the purpose of the constructor to
improve readability:

```php
class PackingSlip
{
   protected $kit;
 
   private __construct(KitInterface $kit)
   {
      $this->kit = $kit;
   }

   public static function forKit(KitInterface $kit)
   {
       return new self($kit);
   }
}

