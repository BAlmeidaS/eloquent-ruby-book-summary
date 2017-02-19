## Array

`words = [ 'little', 'dog', 'things', 'wonder' ]`

`words = %w{ little dog things wonder}`

## Hash

*Hash Rocket:*  **=>**


`a_hash = { "I" => 1, "dont" => 2, "like" => 1,  "spam" => 932 }`

`book_authour = {:first_name => "Russ", :last_name => "Olsen" }`

`book_authour = {first_name: "Russ", last_name: "Olsen" }`

## Arrays and Hashes from Method Calls

### Arrays
```
def echo_all(*args)
  args.each {|a| puts a}
end
```

```
def echo_at_least_two(first_arg, *middle_args, last_arg)
  puts "the first #{first_arg}"
  middle_args.each { |arg| puts "a middle argument #{arg}" } 
  puts "the last #{last_arg}"
end
```

The jargon for a star used in this context is **SPLAT**, as in *splat names*.
Thinking of an exploding array, whit elements flying every which way.

*Two different ways:*

```
def authors(*names)
  "#{names.join(" ")}"
end
> authours("Bruno", "Almeida")
```
```
def authors(names)
  "#{names.join(" ")}"
end
> authours( ["Bruno", "Almeida"] )
``` 

### Hashes
```
def echo_some_hash_keys(hash)
  puts hash[:name]
  puts hash[:age]
end
```
`> echo_some_hash_keys({ name: "bruno", age: 27 })`

`> echo_some_hash_keys(name: "bruno", age: 27 )`

`> echo_some_hash_keys(name: "bruno")`

## Running into collection
```
words = [ "palavras", "ao", "vento" ]
film = { title: "Matrix", genre: "sci fi" }
```

#### Each
```
> words.each { |o| puts o }
palavras
ao
vento

> film.each { |o| puts o }
title
Matrix
genre
sci fi

> film.each { |k, v| puts v }
Matrix
sci fi
```

#### find_index
```
> words.find_index {|o| o == "ao"}
=> 1
```

#### map
```
> words.each { |o| o.upcase }
=> [
  [0] "palavras",
  [1] "ao",
  [2] "vento"
]

> words.map { |o| o.upcase }
=> [
  [0] "PALAVRAS",
  [1] "AO",
  [2] "VENTO"
]
```

#### inject
```
> count_of_letters = words.inject(0) { |result, word| result + word.size }
=> 15
```

#### Order Hash and Array
Ambos, Arrays e Hashes, em ruby são **ordenados**.

## BANG
Ruby convention is that an exclamation poin at the end of a method name indicates that the method is the dangerous or surprising verion of a pair of methods
```
> a = [1,2,3]
> a.reverse
=> [
  [0] 3,
  [1] 2,
  [2] 1
]
> a
=> [
  [0] 1,
  [1] 2,
  [2] 3
]
```
```
> a = [1,2,3]
> a.reverse!
=> [
  [0] 3,
  [1] 2,
  [2] 1
]
> a
=> [
  [0] 3,
  [1] 2,
  [2] 1
]
```

##SET
```
> require "set"
=> true
> words = [ '1', '2', '2', '3' ]
=> [
  [0] "1",
  [1] "2",
  [2] "2",
  [3] "3"
]
> Set.new words
=> [
  [0] "1",
  [1] "2",
  [2] "3"
]
```

