---
title: Don't Mock What You Don't Own 
---

The maxim "Don't Mock What You Don't Own" was cryptic to me when I first heard it. Even searching the internet
for clues wasn't much help. I've since learned from experience why this is a rule espoused by those who have
adopted the discipline of TDD.

I recently started working in a large system whose test count came to a whopping total of two - and both tests were
broken. In the succeeding months as I worked to build up a test suite that could be called passable, I mocked
out an interface that came from a library which adds csv downloads.

```php
\Excel::shouldReceive('create->export')->once();
```

This was all well and fine until one day I needed to upgrade the library. By this point I had forgotten all
about the devious mock waiting in the bushes for me. When I upgraded the library, the export function had been
removed, but as far as my test could tell, export had been called and all was well.

It wasn't until I got the bug report that I realized my mistake. Now my code actually uses the library and I can sleep well knowing that if the library tries any funny business that I'll be aware of it. 

That being said there may be cases where you don't want your test to use the library directly. Then you can wrap
the library in an object of you creation, and you're free to create a test double for your own class. You'll still have to figure out a way to test it, either through a test that you're ok with using the code you don't "own", or even testing it manually, but at least the library won't be pestering your test suite anymore. 
