# Operators

It's nice to know that every operator in Ruby is a method, so when you say this:

`sum = first + second`

What you are really saying is:

`sum = first.+(second)`

what this means is that creating a class that supports operators boils down to defining a buch of instance methods, methods with name like + or -.

```
>class Document
>  attr_reader :content
>  def initialize(content)
>    @content = content
>  end
> 
>  def +(other)
>    Document.new("#{content} #{other.content}")
>  end
>end
```

`>total_document = Document.new("this is") + Document.new("nice")`

## A Sampling of Operators
Operators that you can overload: `+`, `-`, `/`, `*`, the modulo operator `%`, `&`, `|`, `^`, `<<`, `!`, `||`, `&&`, `and`, `or`.

some operators are binary, some unary, like `!`.

```
>name = []
=> []

>name << "testing"
>name << "operator"

>name
=> [
  [0] "testing",
  [1] "operator"
]
```

```
>class Document
>  #...
>  def !
>    Document.new "this is not #{content}"
>  end
>end
>
>doc = Document.new "some content"
=> #<Document:0x007fc657c5d0f8 @content="some content">
>doc.content
=> "some content"
>
>(!doc).content
=> "this is not some content"
```

`+` and `-` can be unary if defined with +@ or -@:

```
>class Document
>  #..
>  def +@
>    Document.new "I am sure that #{content}"
>  end
> 
>  def -@
>    Document.new "I doubt that #{content}"
>  end
>end
>
>doc = Document.new "content"
>
>(-(+doc)).content
=> "I doubt that I am sure that content"
```

You can even redefine `[]`:

```
>class Document
>  #...
>  def [](index)
>    content[index]
>  end
>end
>
>doc = Document.new "content"
>
>doc[2]
=> "n"
```

### So whe should define operators?

Depends it. The easiest case is where you find yourself building a class that has some natural and intuitive operators definitions.

Olsen says in the book about, in 98% of the crazy ideas you can have, you should not define operators for the classes you've created. When you define an operator, many assumptions appear, and it is good that you can handle with them.

Although he points out how, when well used, they are awesome. An example he gives is rspec by setting "equals" to see if the test fails.
 





