---
author: Enrique García Cota
title: Lua for Rubyists
---
# Lua for Rubyists

## Enrique García Cota

madrid-rb, 2014-01

---

# 2 main parts:

## Lua
## Applications

---

# Lua
## Compared with Ruby

---

# It's Lua, not LUA

---

PENDING: Lua logo

---

PENDING: Earth + Moon

---

| **Ruby**                           | **Lua**                         |
|------------------------------------|---------------------------------|
| Yukihiro, Japan                    | Roberto, Brazil                 |
| PENDING: Image of matz             | PENDING: Image of Roberto(joke) |
| Make programmers happy             | Embeddable > Elegant > Fast     |

---

| **Ruby**                           | **Lua**                         |
|------------------------------------|---------------------------------|
| Yukihiro, Japan                    | Roberto, Brazil                 |
| PENDING: Image of matz             | PENDING: Image of Roberto       |
| Make programmers happy             | Embeddable > Elegant > Fast     |

---

# Size

---

# Ruby (MRI)

```bash
git clone https://github.com/ruby/ruby.git
rm -rf ruby/benchmark ruby/bootstraptest ruby/doc \
       ruby/ext ruby/sample ruby/test ruby/tool
cloc ruby
```

## &rArr; ~650k (C, C++, Ruby)

---

# Lua (5.2.3)

```bash
git clone https://github.com/LuaDist/lua.git
cloc lua/src
```

## &rArr; ~15k (C99)

---

# Batteries included

---

# PENDING: Rabbit with/without batteries

---

Artillery battery: PENDING definition

---

![](images/artillery-battery.jpg)

---

Pending: Image of soldier

---

# Ruby: Core + stdlib

---
## Ruby core:
```ruby
$ irb
> Object.constants.map{|c| Object.const_get(c)}
 => [ ... ]

> _.select{|c| c.is_a? Class}
 => [ Object, Module, Class, BasicObject, Method,
      NilClass, String, Symbol, Regexp, Range,
      Time, Date, File, Dir, TrueClass, FalseClass,
      Numeric, Integer, Fixnum, Float, Bignum,
      Rational, Complex, Thread, Fiber, ...
    ] (73)

> _.map{|c| c.methods.count}.inject(:+)
  => 7112

> _.map{|c| c.public_methods(false).count}.inject(:+)
  => 399
```

---

## Ruby Stdlib:

* &rArr; http://www.ruby-doc.org/stdlib-2.1.0/
* 109 packages: `set`, `base64`, `date`, `erb`, `yaml`, `csv`, `json`, `rss`, `minitest`, `net/*`, `zlib`, `webrick`, ...
* Presentation: [Ruby: Batteries Included](http://www.confreaks.com/videos/2347-mwrc2013-ruby-batteries-included)

---

# Lua:

## types

    string, number, boolean, function, table, thread, nil

## libraries

    string, table, math, os, io, coroutine, debug

## top-level functions

    require, print, pairs (~30)

---

