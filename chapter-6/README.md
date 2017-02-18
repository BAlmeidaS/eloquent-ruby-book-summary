# Symbols
There can only ever be **one instance** of any given symbol. If I mention :all twice or more in my code, it is always exactly the same :all.

symbols are immutable

```
> a = :a
=> :a
> b = :a
=> :a

> a == b
=> true
> a === b
=> true
> a.eql? b
=> true
> a.equal? b
=> true
```

```
> a = "a"
=> "a"
> b = "a"
=> "a"

> a == b
=> true
> a === b
=> true
> a.eql? b
=> true
> a.equal? b
=> false
```

Russ Olsen says: *"You want to use strings for data, for things that you might want to truncate, turn to uppercase, or concatenate. Use symbols when you simply want an intelligible thing that stands for something in your code."*