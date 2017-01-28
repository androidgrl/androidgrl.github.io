---
layout: post
title: The Namespace Resolution Operator, aka the "double colon operator"
---

At work I saw an interesting version of the namespace resolution operator, aka the double colon operator.  Previously I had only seen it used to gain access inside scoped modules.  Such as gaining access to the ID defined inside module B below:

```
module A
  module B
    ID = 3
  end
end

puts A::B::ID
>> 3
```

But this time it was used at the beginning of a scoped chain of modules like inside module B below:

```
module C
  ID = 3
end

module A
  module C
  ID = 4
    module B
      ID = ::C::ID
    end
  end
end

puts A::C::B::ID
>> 3
```

This is called the root namespace resolution operator and it specifies that you are looking for a root level module.  A root level module is one that is not scoped inside another module.  So in this case, it is the module C defined on top which has the ID of 3.

Why was this needed?  It was needed so that it wouldn't find the scoped module A::C's ID instead.  For example if we removed the root operator like below, it would return 4 instead of 3.

```
module C
  ID = 3
end

module A
  module C
  ID = 4
    module B
      ID = C::ID
    end
  end
end

puts A::C::B::ID
>> 4
```

In fact, if we did not have the ID = 4 defined inside the scoped module C, it would error out and never find the root level module C ID, like below.

```
module C
  ID = 3
end

module A
  module C
    module B
      ID = C::ID
    end
  end
end

puts A::C::B::ID
>> error
```

Why does the scoped A::C take precedence over the root level C in the above case?
Because when you call C::ID inside of module B, it starts from where it is inside the scope and moves outward through it's surrounding modules.  It then finds the outer module A::C and looks for an ID there.  Because it found a module C, it stops there and does not continue even though it has no ID defined, and does not continue to look for the root module C.

Also it is important to note that when two modules have the same name but are scoped differently they are completely different modules.  In fact they might as well have different names.  For example below:

```
module C
  ID = 1
end

module A
  module C
    ID = 2
  end
end

puts C::ID
>> 1
puts A::C::ID
>> 2
```

This is not to be confused with monkey patching a module, for example the code below first defines a root level module C with a constant of ONE, then it monkey patches the same root level module to add another constant TWO.  You can monkey patch a module or class as many times as you want, Ruby doesn't care.

```
module C
  ONE = 1
end

module C
  TWO = 2
end

puts C::ONE
>> 1
puts C::TWO
>> 2
```

However, if you tried to monkey patch into a module with the same name but on a different scoped level it would not work because they're two entirely different modules.

```
module C
  ONE = 1
end

module A
  module C
    TWO = 2
  end
end

puts C::TWO
>> error
```
