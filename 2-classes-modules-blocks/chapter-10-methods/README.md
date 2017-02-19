# methods of a class

Breaking your code up into many short, single-purpose methods not only plays to the strengths of the Ruby but also makes your whole application more testable.

## compressing

Olsen starts with this problem:

*The compression algorithm, which will take in a text string and produces two arrays. The first array would contain all the words found in the text, with no repeat. The second array will contain integer index, the length of it is equal of the words in the string, and the integer in each position give us wich word is, based on first array.*

string: `this specification is the specification for a specification`

first array: `[ "this", "specification", "is", "the", "for", "a" ]`

second array: `[ 0, 1, 2, 3, 1, 4, 5, 1 ]`

*this technique is the sort of thing you might do when you want to compress some text*

#### first stab

```
>class TextCompressor
>  attr_reader :unique, :index
>  def initialize(text)
>    @unique = []
>    @index = []
>
>    words = text.split
>    words.each do |word|
>      i = @unique.index(word)
>      if i
>        @index << i
>      else
>        @unique << word
>        @index << unique.size - 1
>      end
>    end
>  end
>end
```

```
>text = "this specification is the specification for a specification"
=> "this specification is the specification for a specification"
>compressor = TextCompressor.new(text)

>compressor.unique
=> [
  [0] "this",
  [1] "specification",
  [2] "is",
  [3] "the",
  [4] "for",
  [5] "a"
]
>compressor.index
=> [
  [0] 0,
  [1] 1,
  [2] 2,
  [3] 3,
  [4] 1,
  [5] 4,
  [6] 5,
  [7] 1
]
```

#### second stab

```
>class TextCompressor
>  attr_reader :unique, :index
>  def initialize(text)
>    @unique = []
>    @index = []
>
>    words = text.split
>    words.each do |word|
>      i = unique_index_of(word)
>      if i
>        @index << i
>      else
>        @index << add_unique_word(word)
>      end
>    end
>  end
>
>  def unique_index_of(word)
>    @unique.index(word)
>  end
>
>  def add_unique_word(word)
>    @unique << word
>    unique.size - 1
>  end
>end
```

#### third stab

```
>class TextCompressor
>  attr_reader :unique, :index
>  def initialize(text)
>    @unique = []
>    @index = []
>    add_text(text)
>  end
>
>  def add_text(text)
>    words = text.split
>    words.each { |word| add_word(word) }
>  end
>
>  def add_word(word)
>    i = unique_index_of(word) || add_unique_word(word)
>    @index << i
>  end
>
>  def unique_index_of(word)
>    @unique.index(word)
>  end
>
>  def add_unique_wird(word)
>    @unique << word
>    unique.size - 1
>  end
>end
```

## Composed method

What we have done is to apply the composed method technique. This technique advocates diving your class up into methods that have 3 caracteristics:

 1. each method should do a single thing - *your methods are not only wasier to write, they are also easier to understand*
 2. each method needs to operate at a single conceptual level - *A method that implements the business logic should not go into details of database, for example.*
 3. each method must to have a name that reflects its purpose.

The reason you should lean toward smaller methods is that all those compact, easy-to-comprehend methods will help you, and others, to get the details right =].

*Look at a class, and if it contains a lot of short, pointed methods it just feels like Ruby.*

Besides the fact that is **easier to test**.

## Other practical example

in some class, we have this two methods:

`def a_density; end`

`def b_density; end`

and then, this little confusing method:

```
def prose_rating
  if a_density > 0.3
    if b_density < 0.2
      return :really_a
    else
      return :somewhat_a
    end
  elsif a_density < 0.1
    if b_density > 0.3
      return :really_b
    end
    return :somewhat_b
  else
    return :about_right
  end
end
```

#### minor refactor

```
def prose_rating
  if a_density > 0.3
    if b_density < 0.2
      rating = :really_a
    else
      rating = :somewhat_a
    end
  elsif a_density < 0.1
    if b_density > 0.3
      rating = :really_b
    end
    rating = :somewhat_b
  else
    rating = :about_right
  end
  
  rating
end
```

#### final refactor

```
def prose_rating
  return :really_a if really_a?
  returb :somewwhat_a if somewhat_a?
  return :really_b if really_b?
  returb :somewwhat_b if somewhat_b?
  :about_right
end

def really_a?
  a_density > 0.3 && b_density < 0.2
end

def somewhat_a?
  a_density > 0.3 && b_density >= 0.2
end

def really_b?
  a_density < 0.1 && b_density > 0.3
end

def somewhat_b?
  a_density < 0.1 && b_density <= 0.3
end
```

## Final Considerations

Don't go too far in breaking up methods! Avoud the clutter. Taken to the dysfunctional extreme, it's possible to compose method yourself into a diffuse cloud of programming dust.

Getting into the habit of writing the short, pointy methods technique takes time and effort.

Olsen recommends us see the class ActiveRecord::Base, which has about 1800 non-comment lines that define about 200 methods.