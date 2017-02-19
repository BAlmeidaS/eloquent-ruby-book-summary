# Dynamic Typing

## Duck Typing
Instead of create an Abstract class like the following:

```
class BaseDocument
  def title
    raise "Not Implemented"
  end
  def title=
    raise "Not Implemented"
  end
  def author
    raise "Not Implemented"
  end
  def author=
    raise "Not Implemented"
  end
end

class Document < BaseDocument; ...; end
class LazyDocument < BaseDocument; ...; end
```

And create Document and LazyDocument extending it. Just create those two classes respecting some interface:

```
class BaseDocument
  attr_accessor :title, author
  def initialize title, author
    @title = title
    @author = author
  end
  
  def tags
    #returns all tags of document
  end
end

class BaseDocument
  attr_writer :title, author
  
  def title
    #do something different to return title
  end
  
  def author
    "Always the same"
  end
end
```

## Using Dynamic Typing

Supose that, as a new feature, you have to create two new classes, Author and Title.
```
class Title
  attr_accessor :long_name, :short_name
  def initialize(long_name, short_name)
    @long_name = long_name
    @short_name = short_name
  end
end

class Author
  attr_writer :first_name, :second_name
  def initialize(first_name, second_name)
    @first_name = first_name
    @second_name = second_name 
  end
end  
```

Because dynamic typings, you dont have to change nothing in Documents Classes.

```
title = Title.new "The long title", "TST"
author = Author.new "Some", "Name"
BaseDocument.new title, author 
```

The only concern that Duck Type Document could have, it would be about some interface that Title or Author should be implemented.

Instead of typing variables, create some clarify names for them =]. **Avoid cryptic variables**, as *c = 1* or *au = "bruno"*

*Ruby Philoshophy "if the method is there, it is the right object"*