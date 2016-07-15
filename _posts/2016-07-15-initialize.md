---
layout: post
title: What is initialize used for in Ruby?
---

Does initialize need to be used all the time in a class?  No.
You only need it to set instance variables and to allow passing of arguments when instantiating a class.

**Example one:** *You don't need it to instantiate a class*

Let's make a class with a single instance method and no initialize method.

```
class Holiday
  def statement
    "I'm going to the beach"
  end
end
puts Holiday.new
puts Holiday.new.statement
```

If we run the code, the "puts" outputs the following, and we see that Holiday.new instantiates an object just fine and we can call the method statement on it:

```
#<Holiday:0x007fe194093d00>
I'm going to the beach
```

**Example two:** *You don't need it to use attr_accessors*

Let's make a class with an attr_accessor and no initialize method.  We instantiate two different holiday objects, and then using the attr_accessors set a separate location attribute for each.

```
class Holiday
  attr_accessor :location
  def statement
    "I'm going on holiday to #{location}"
  end
end
holiday1 = Holiday.new
holiday2 = Holiday.new
holiday1.location = "Europe"
holiday2.location = "Hawaii"
puts holiday1.statement
puts holiday2.statement
```

The output shows that the attr_accessors still work without the initialize method.

```
I'm going on holiday to Europe
I'm going on holiday to Hawaii
```

**Example three:** *You DO need it to set instance variables*

The following is a class that tries to set an instance variable @word to equal "whatever".
The output is nothing, because instance variables need to be put inside an initialize method.

```
class Random
  @word = "whatever"
  def whatever
    @word
  end
end
puts Random.new.whatever
```

The following will correctly result in an output of "whatever".

```
class Random
  def initialize
    @word = "whatever"
  end
  def whatever
    @word
  end
end
puts Random.new.whatever
```

**Example four:** *You DO need it to allow arguments to be passed in when instantiating a Class*

The following code tries to pass in a string argument into the "new" method.

```
class Random
end

puts Random.new("whatever")
```

This results in an error.

```
new.rb:35:in `initialize': no implicit conversion of String into Integer (TypeError)
        from new.rb:35:in `new'
        from new.rb:35:in `<main>'
```

You need to specify that there are arguments in the initialize method for "new" method to be able to take any.
However, you don't have to actually do anything with the arguments in the initialize method.

```
class Random
  def initialize(word)
  end
end

puts Random.new("whatever")
```

This will result in the object being successfully instantiated, as shown in the output below.

```
#<Random:0x007fbbb9170cd8>
```

If you wanted to actually have access to the attribute then you would have to set it as an instance variable inside the initialize method, and set an attr_reader.

```
class Random
  attr_reader :word
  def initialize(word)
    @word = word
  end
end

puts Random.new("whatever").word
```

Which will output "whatever".

