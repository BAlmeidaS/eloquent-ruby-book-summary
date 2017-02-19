# Everything is an Object
Classes act as containers for methods.
Classes are also factories for making instances.

**Self** is what ruby assumes when you call a method without object reference.

If you don't specify a super class, the new class automatically becomes a direct subclass of **Object**. like this:

```
Class Document
  # lot of things
end
```

#### superclass
```
class RomanceNovel < Document
  # things
end
```

## Being an Object
All Ruby object can trace their ancestry back to Object

```
> class Doc
* end

puts Doc.new
#<Doc:0x007fea7eaf3f28>
```

```
> class Doc
*   def to_s
*     "hey i am a Doc"
*   end
* end

> puts Doc.new
hey i am a Doc
```

### eval
eval method is defined by Object

**eval takes a string and executes it as if were Ruby code**

```
> eval "2 + 2"
=> 4
> eval "puts 'Bruno'"
Bruno
```

## Public, Private and Protected
all methods are public by default

### private
```
> class Doc
*   private
*   def size
*     "dont know my size"
*   end
* end
```

OR

```
> class Doc
*   def size
*     "dont know my size"
*   end
*   private :size
* end
```

```
> Doc.new.size
NoMethodError: private method `size' called for #<Doc:0x007fea7ead94c0>
```

**private methods are callable from subclasses.**

```
> class Test < Doc
*   def a
*     size
*   end
* end
=> :a
> Test.new.a
=> "dont know my size"
```

### protected
Any instance of a class can call a protected method on any other instance of the class. If we made method "a_method" protected in A, any instance of A could call "a_method" on any other instance of A, including instances of subclasses of A.

```
> class A
*   def run
*     A.new.a_method
*   end
*   private
*   def a_method
*     puts "a bit confusing"
*   end
* end

> A.new.run
NoMethodError: private method `a_method' called for #<A:0x007fea7eb61be0>
```

```
> class A
*   def run
*     A.new.a_method
*   end
*   protected
*   def a_method
*     puts "a bit confusing"
*   end
* end

> A.new.a_method
NoMethodError: protected method `a_method' called for #<A:0x007fea7e968668>

> A.new.run
a bit confusing
```

### send

```
> class A
*   private
*   def a_method
*     puts "a bit confusing"
*   end
* end

> A.new.send(:a_method)
a bit confusing
```

## examples of methods
##### require
`require "date"`

##### attr_accessor family
```

> class Person
*   attr_accessor :salary
*   attr_reader :name
*   attr_writer :password
* end
```



