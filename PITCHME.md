# Garbage collector in ruby, why should I care!


+++

# Aboobacker MK

Software Engineer @ Redpanthers

@tachyons in github
@_tachyons in twitter

---

Last minute backup talk

---

# Let's Talk about memmory

---

Stack: for static memory allocation

Heap: Dynamic memory allocation

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

Grabage collector
---


```ruby
a = "foo"
b = "bar"
c = { a => b }
```

![image](images/root.png)
---

Goodbye!

+++

