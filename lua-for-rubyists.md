---
author: Enrique García Cota
title: Lua for Rubyists
---
# Lua for Rubyists

## Enrique García Cota (@otikik)

### madrid-rb, 2014-01

---
# 2 main parts:

## Applications
## Lua vs ruby

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

## Part 1: Applications

---

![fullscreen](images/nginx.png)

---

![fullscreen](images/openresty.png)

---

![fullscreen](images/taobao.jpg)

---

![fullscreen](images/raspberry.png)

---

![fullscreen](images/techempower-1.png)

---

![fullscreen](images/techempower-2.png)

---

![fullscreen](images/redis.png)

---

> Key-value data store

---

```ruby
require "redis"
redis = Redis.new('localhost', 6379)

redis.set("name", "peter")
name = redis.get("name") # "peter"

redis.set("age", "25")
new_age = redis.incr("age") # 26
```
---

> Concurrent, but single threaded

---

![fullscreen](images/bartender.jpg)

---

```ruby
counter = redis.get('counter')

redis.incr('counter') if counter.is_a? Numeric
```

---

```ruby
script = <<-EOS
  local counter = redis.call("GET", KEYS[1])
  if type(tonumber(counter)) == "number" then
    return redis.call("INCR", KEYS[1])
  end
EOS

redis.eval(script, ["counter"])
```

---

PENDING: Include LuaInception?

---

![centered](images/vim.png)

---

```
brew install vim --with-lua
or
brew install macvim --with-lua
```

---

```bash
                    Startup     Speed

      Vim script    0           1.498s
      Python        0.0166s     0.027s (2000%)
      Luajit        0.0002s     0.001s (1152000%)
```
---

![fullscreen](images/neocomplete.gif)

---

![fullscreen](images/unite.gif)

---
= data-text='centered'

## Corona SDK

![centered](images/corona-sdk.png)

---

![fullscreen](images/corona-games.png)

---

![centered](images/corona-platforms.png)

---

![fullscreen](images/corona-apps.png)

---

![fullscreen](images/love2d.png)

---

# Part 2: Lua vs ruby

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
> Portable, powerful, embeddable, fast.

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

# Feel

---

Ruby &#9825;

```ruby
# ruby

even_numbers = (1..10).select(&:even?)

tweets.delete_if{ |t| t.older_than? 1.week }

```
---

```lua
-- lua
local name = "peter" -- or 'peter'

other_name = "john" -- global variable!

local age = 17
age = age + 1
local adult = age >= 18 -- boolean

local tname = type(name)
print(tname) -- string

```

---

PENDING: more work here

```ruby
def days_in_month(year, month)
  Date(year, month, -1).day
end
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

PENDING: tasks for a imperial destroyer

---

PENDING: conclusion

---

# Questions?
### Enrique García Cota (@otikik)
### madrid-rb

---

# Thank you! <span class="applause">&#9734;</span>


