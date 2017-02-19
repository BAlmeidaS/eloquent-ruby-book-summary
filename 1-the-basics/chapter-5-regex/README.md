# Regular Expression
Some simple considerations:

- "." match any single-character 
- "\d" match any digit
- "[0123456789]" match any digit
- "[0-9]" match any digit
- "\w" match any letter
- "\s" match any white space
- "[0-9a-f] match any hexadecimal
- "[AM|am]" match "AM" *OR* "am"
- "B*" match zero or more "B"s
- "[aeiou]*" match zero or more vowels
- "C+" match one or more "C"s

regular expressions in ruby is build with sintax of forward slashes:

`/[a-z]*12[3|4|5]/`

## =~ operator

```
> /\d\d:\d\d (AM|PM)/ =~ "03:30 PM"
=> 0
```
```
> /\d\d:\d\d (AM|PM)/ =~ "Test"
=> nil
```
```
> /test/ =~ "what the position that starts to match this test?"
=> 44
```

##### ambidextrous
```
> "what the position that starts to match this test?" =~ /test/
=> 44
```

##### case insensitive with i
```
> "this is a TEST" =~ /test/
=> nil
> "this is a TEST" =~ /test/i
=> 10
```

## beginning and ending of string
### \A *beginning*
```
> "string starts with letter c?" =~ /c/
=> 26
> "string starts with letter c?" =~ /\Ac/
=> nil
```

### \z *ending*
```
> "string ends with letter c?" =~ /c/
=> 24
> "string ends with letter c?" =~ /c\z/
=> nil
```

## beginning and ending of multiline strings
```
> text = "this is a long text
* that we are going to use
* to see how it works ^ and $."
```

### ^ *beginning*
```
> text =~ /^how/
=> nil
> text =~ /^this/
=> 0
```

### $ *ending*
```
> text =~ /\.works/
=> nil
> text =~ /\.$/
=> 72
```

## additional infos

### ? is for optional

```
> "dog's house" =~ /dog'?s house/
=> 0
> "dogs house" =~ /dog'?s house/
=> 0
```

### Assigning matches in parameters
*match must be on the left side*
```
> /(?<animal>\w+)'s house/ =~ "dog's house"
=> 0
> animal
=> "dog
```
