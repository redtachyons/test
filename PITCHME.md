# Garbage collector in ruby, why should I care!


---?image=assets/bg.jpg

# Ugly Indian Initiative

+++

![Quint Image1](images/thequint_ugly_indian.jpg)

+++

![Quint Image2](thequint_ugly_indian2.jpg)
---
# Garbage In ruby ?
---

# Aboobacker MK

Software Engineer @ Redpanthers

@tachyons in github
@_tachyons in twitter

---
## Redpanthers
![Redpanthers](images/redpanthers.logo)
### We love conferences

Group photo here

---
# GC in a language designed for happiness
---

# Let's Talk about memmory

+++
![RAM](https://upload.wikimedia.org/wikipedia/commons/7/7c/RAM_module_SDRAM_1GiB.jpg)
> Source : https://commons.wikimedia.org/wiki/File:RAM_module_SDRAM_1GiB.jpg

---

Stack: for static memory allocation

Heap: Dynamic memory allocation

+++

![Stack vs HEAP](https://i.imgur.com/HB2GtHg.png)

---

# Ruby stores everything in heap

** Except fibres
---

# Every thing is an object

---

# Objects everywhere

---

# We have to clean it
---

#Grabage collector

* Also responsible Object allocation(Garbage creation)
* Allocate in empty slots 
* Allocate new page when empty slots aren't available

---

---


```ruby
a = "foo"
b = "bar"
c = { a => b }
```

![image](images/root.png)
---
Collect all unused objects
---
# History
---
Mark and Sweep (Ruby 1.8)

* Mark all living objects
* Remove unmakrked objects 

---

![mark](images/msweep.png)
---
Simple, But causes parogram pause
---
Lazy sweep (1.9)
---

Bitmap marking (Ruby 2.0)

* Copy on write optimisation

---

# Generational GC

* Yound and old
* Addresses throughput issue
* Most objects die young

---

Incremental GC

* Intereleave GC process and Ruby process
* Shorter individual pause
* consistent perfomenece

---
* white object: Not marked object
* Grey object: Marked, but may have reference to white objects
* Marked, but no reference

---
# Object retention
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
---

# Diffrence with python GC

* Ruby uses free list
* Python asks for memory
* Reference count inside objects
* reset reference to 0 when no longer in use

---
# Defragmentation

---
# Slow?

---

Thanks

+++

