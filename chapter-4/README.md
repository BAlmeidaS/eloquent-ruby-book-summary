# String API
### Single and Double Quotes
```
> 'isso é uma string com \'single quote\''
=> "isso é uma string com 'single quote'"
> "isso é uma string com 'double quote'"
=> "isso é uma string com 'double quote'"
```
```
> puts 'double quote has more interpreation. \t like a tab. \n and a new line'
double quote has more interpreation. \t like a tab. \n and a new line

> puts "double quote has more interpreation. \t like a tab. \nAnd a new line"
double quote has more interpreation. 	 like a tab.
And a new line
```

```
> words = "some words"
> puts "double quote can do interpolation. #{words} "
double quote can do interpolation. some words
```

### %q
```
> %q{a good exemple to 'why' use this "q" with the %}
=> "a good exemple to 'why' use this \"q\" with the %"
```
```
> %q( you can change the delimiter)
=> " you can change the delimiter"
```
```
> %q$ to can do
* many things,
* you know?$
=> " to can do\nmany things\nyou know?"
```
### %Q
```
> word = "ruby"
> %q{ dont do interpolation #{word}}
=> " dont do interpolation \#{word}"
> %Q{ upcase "q" does interpolation in #{word}}
=> " upcase \"q\" does interpolation in ruby"
```
## strip
```
> "   test   "
=> "   test   "

> "   test   ".lstrip
=> "test   "

> "   test   ".rstrip
=> "   test"

> "   test   ".strip
=> "test"
```
## chomp
remove the last new-line character in string

```
> "bruno\n\n".chomp
=> "bruno\n"
```
```
> "bruno\n\n".chomp.chomp.chomp.chomp
=> "bruno"
```

## chop
Remove the last character wherever that it is

```
> "bruno\n\n".chop
=> "bruno\n"
```
```
> "bruno\n\n".chop.chop.chop.chop
=> "bru"
```

## sub
```
> "python is awesome".sub("python", "ruby")
=> "ruby is awesome"
```

## gsub
```
> "i say python, python, python".sub("python", "ruby")
=> "i say ruby, python, python"

> "i say python, python, python".gsub("python", "ruby")
=> "i say ruby, ruby, ruby"
```

## split
```
> "i want to split this phrase".split
=> [
  [0] "i",
  [1] "want",
  [2] "to",
  [3] "split",
  [4] "this",
  [5] "phrase"
]
```
```
> "and:this:one:too".split(":")
=> [
  [0] "and",
  [1] "this",
  [2] "one",
  [3] "too"
]
```

## BANG
```
> a = "I really like python"
=> "I really like python"

> a.sub("python", "ruby")
=> "I really like ruby"

> a
=> "I really like python"

> a.sub!("python", "ruby")
=> "I really like ruby"

> a
=> "I really like ruby"
```

## String is a collection of chars

`> phrase = "Ping \nPong"`

#### array
```
> phrase[3]
=> "g"
```

#### each_byte
```
> phrase.each_byte { |b| puts b }
80
105
110
103
32
10
80
111
110
103
```

#### each_line
```
> phrase.each_line { |line| puts line }
Ping
Pong
```

##Strings are mutable
```
> first = "knoc"
=> "knoc"
> last = first
=> "knoc"
> first[-1] = "k"
=> "k"
> first
=> "knok"
> last
=> "knok"
```