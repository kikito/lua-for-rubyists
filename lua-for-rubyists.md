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

# SOL &rArr;
## Simple Object Language

---

![fullscreen](images/sol.png)

---

# Lua &rArr;
## “Moon” in Portuguese
## (No Initials)

---
= data-transition='fade'

![fullscreen](images/lua-logo.png)

---
= data-transition='fade'

![fullscreen](images/earth-moon.png)

---

# Generalities

---

![float-left](images/matz.png)

## Yukihiro Matsumoto
> A general-purpose language to make programmers happy

---

![fullscreen](images/ruby-timeline.svg)

---

![fullscreen](images/websites.gif)

---

![float-left](images/roberto.png)

## Roberto Ierusalimschy
> Portable, embeddable, powerful, fast.

---

![fullscreen](images/lua-timeline.svg)

---

![fullscreen](images/videogames.jpg)

---

# Implementations

---

## Ruby

### MRI (1.8.7, 1.9.x, 2.x)
### JRuby
### Rubinius

---
= data-transition='fade'

![fullscreen](images/ruby-venn-1.svg)

---
= data-transition='fade'

![fullscreen](images/ruby-venn-2.svg)

---

## Lua

### Lua (5.0, 5.1, 5.2)
### LuaJIT
### eLua

---
= data-transition='fade'

![fullscreen](images/lua-venn-1.svg)

---
= data-transition='fade'

![fullscreen](images/lua-venn-2.svg)

---

# Size

---

## Lines of code

```bash
git clone https://github.com/ruby/ruby.git
rm -rf ruby/benchmark ruby/bootstraptest ruby/doc \
       ruby/ext ruby/sample ruby/test ruby/tool
cloc ruby
```

### &rArr; ~650k (C, C++, Ruby)

```bash
git clone https://github.com/LuaDist/lua.git
cloc lua/src
```

### &rArr; ~15k (C99)

---
## Ruby core:
```ruby
$ irb
> a = Object.constants.map{|c| Object.const_get(c)}
 => [ ... ]

> b = a.select{|c| c.is_a? Class}
 => [ Object, Module, Class, BasicObject, Method,
      NilClass, String, Symbol, Regexp, Range,
      Time, Date, File, Dir, TrueClass, FalseClass,
      Numeric, Integer, Fixnum, Float, Bignum,
      Rational, Complex, Thread, Fiber, ...
    ] (73)

> b.map{|c| c.methods.count}.inject(:+)
  => 7112

> b.map{|c| c.public_methods(false).count}.inject(:+)
  => 399
```

---

## Ruby Stdlib:

### www.ruby-doc.org/stdlib-2.1.0

```ruby

     set         yaml       minitest     erb
     base64      csv        mutex        webrick
     date        json       zlib         net/*
     fileutils   matrix     curses       socket
     pp          profile    rss          uri
                        ...

                       (~109)
```

* Presentation: “Ruby: Batteries Included”:

  http://www.confreaks.com/videos/2347

---

![float-left](images/gems.png)
## Ruby &rArr; gems
## rubygems.org
## ~70000 gems

---

## Lua:

Types (~7)

```bash
string, number, table, boolean, function, thread, nil
```

Libraries (~7)

```lua
string, math, table, os, io, coroutine, debug
```

Top-level functions (~30)

```lua
    assert          load        pcall     setmetatable
    collectgarbage  loadfile    print     tonumber
    dofile          loadstring  rawequal  tostring
    error           module      rawget    type
    gcinfo          newproxy    rawset    xpcall
    getfenv         next        unpack
    getmetatable    require     select
    ipairs          pairs       setfenv
```

---

![float-left](images/rocks.png)
## Lua &rArr; rocks
## luarocks.org
## ~700 rocks

---

# Batteries included

---

![fullscreen](images/batteries.png)

---

> **Artillery battery**: a unit of guns, mortars, rockets or missiles so grouped in order to facilitate better battlefield communication and command and control

---

![fullscreen](images/artillery-battery.jpg)

---

![fullscreen](images/destroyer.jpg)

---

![fullscreen](images/soldier.png)

---

![fullscreen](images/macgyver.jpg)

---

# Thank you
## Enrique García Cota (@otikik)
madrid-rb

---

# Appendix 1: Code

---
```lua
local name = "peter" -- or 'peter'

other_name = "john" -- global variable!

local age = 17
age = age + 1
local adult = age >= 18 -- boolean

local tname = type(name)
print(tname) -- string

```

---

```lua
local ADULT_AGE = 18
local function is_adult(age)
  return age >= ADULT_AGE
end

-- equivalent*
local is_adult = function(age)
  return age >= ADULT_AGE
end

local adult = is_adult(age)
print(type(is_adult)) -- function
```

---

```lua
local vowels = { 'a', 'e', 'i', 'o', 'u'}
print(vowels[1]) -- a

local person = {}
person['name'] = 'john'
person.age = 17
print(person.name) -- john
print(person.age) -- 17

local another_person = {name = 'john', age = 15}

print(type(vowels)) -- table
print(type(person)) -- table
```

---


