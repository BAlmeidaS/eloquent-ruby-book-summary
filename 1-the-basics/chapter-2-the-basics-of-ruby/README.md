##2 - capitulo

*escreva um código idiomático!*

###if
```
if some_bool
  do_something
end
```

###unless - *if-not*

```
unless some_bool
  do_something
end
```

###while
```
while something_is_true
  do_something
end
```

###until
```
until something_is_false
  do_something
end
```

###One-line Presentation
```
do_something < if | unless | while | until > some_condition
```

--

### each
```
array.each do |item|
  do_something(item)
end
```

### for - *nao idiomatico*

```
for item in array
  do_something(item)
end
```

--

### case
```
case something
when is_true_for_this_case
  do_something(something)
when is_other_thing
  do_something
else
  do_the_default_thing
end
```

#### case 2#
```
x = case something
    when is_something then return_1
    when other_case then return 2
    else default_return
    end
```

Cases usam o operador *===*, o que faz permitir fazer cases como tipos de classe, por exemplo.

##in the wild

### ?: operator - ternario
```
variable = some_type_of_cheking ? return_for_true : return_for_false
```
 
### define a variable if variable is different of nill

```
@variable = '' unless @variable
OR
@variable ||= ''
``` 






