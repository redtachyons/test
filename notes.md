a = "foo"
b = "bar"
c = { a => b }





GC

* Collect unused objects automatically
* No need of manual intervention

First phase

* Mark and sweep (1.8)
* Two phases
  * Mark: Mark all living objects
  * Sweep: garbage collect all unmarked objects
* Traversible objects from root
* C extensions ?
* Advantages
  * Simple
  * Works well
* Disadvantages
  * throughput
  * Pause time

Lazy sweep

* reduce pause time
* step by step

Bitmap (ruby 2.0)

* linux fork optimisation
* object modification


Generational GC (2.1)

* To address throughput issue
* divides the heap into several spaces several generations
* Young and old
* Young: New objects
* Old: Objects which survived 3 GC
* Most of the objects die young
* Minor GC and Major GC
* Minor GC is fast and is enough for most of the time

Incremental Garbage collection
* splits gc execution process into several fine grainted processes and interleave gc process and ruby process
* Shorter individual pause => Consistent perfomence
* Half is done in lazy sweep
* white object: Not marked object
* Grey object: Marked, but may have reference to white objects
* Marked, but no reference

(1) All existing objects are marked as white 
(2) Clearly living objects such as objects on the stack marked Grey. 
(3) Pick one grey object, visit each object it references and color it grey. Change the color of the original object to black. Repeat until there are no grey objects left only black and white. 

(4) Collect white objects because all living objects are colored black. 

(3) In incremental

* Write barriers

Ruby 2.2

* Not enough write barriers
* write barrier unprotected  objects
*  write barrier protected objects



Object retention
```ruby
100_000.times do
  foo = "a string"
end
```

```ruby
RETAINED = []
100_000.times do
  RETAINED << "a string"
end

```
Diffrence with python

* Ruby uses free list
* Python asks for memory
* Reference count inside objects
* reset reference to 0 when no longer in use


Deffragmentation
slow due to extra overhead for keeping the structure


When it runs

more than malloc limit
lazy sweep when we are out of free slots in the heap


Links

https://speakerdeck.com/ericqweinstein/the-hitchhikers-guide-to-ruby-gc
http://atdot.net/%7Eko1/activities/rubyconf2013-ko1_pub.pdf
https://www.sitepoint.com/ruby-uses-memory/
https://blog.heroku.com/incremental-gc
https://blog.codeship.com/visualizing-garbage-collection-ruby-python/
http://patshaughnessy.net/2012/3/23/why-you-should-be-excited-about-garbage-collection-in-ruby-2-0
https://samsaffron.com/archive/2014/04/08/ruby-2-1-garbage-collection-ready-for-production
https://thorstenball.com/blog/2014/03/12/watching-understanding-ruby-2.1-garbage-collector/
https://samsaffron.com/archive/2013/11/22/demystifying-the-ruby-gc
https://github.com/benoittgt/understand_ruby_memory
https://speakerdeck.com/laurocaetano/garbage-collection-em-ruby
https://medium.com/@rcdexta/whats-the-deal-with-ruby-gc-and-copy-on-write-f5eddef21485
