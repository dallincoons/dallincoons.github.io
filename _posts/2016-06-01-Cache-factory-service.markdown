---
title: Cache Factory service

---

In the process of creating an Angular service that uses the Http protocol to fetch data, I wanted a way to cache data. I proceeded to use Angulars `$cacheFactory`. However, I kept getting this error: `[$cacheFactory:iid] CacheId 'RxHttpData' is already taken!`

This error was because there were many places in which this service was being called, and everytime it was used, I would create a new $cacheFactory with the same Id. Since you can't have multiple $cacheFactory's with the same Id, it blew up. 

I was able to solve this by first extracting the creation of the $cacheFactory into another service. All this service does is to return the $cacheFactory:

    .service('CacheService', ['$cacheFactory', function ($cacheFactory) {

		return $cacheFactory('RxHttpData');

	}]);
    
I included CacheService into the service that was originally instantiating $cacheFactory. This acts as a singleton and as a result, the $cacheFactory service is only instantiated once. 