# Equality between classes

Along the chapters, Olsen modify and create many `Documents`, now we are trying to create a way to find equality between them.

He decide to create some kind of identifier object for the documents.

```
class DocumentIdentifier
  attr_reader :folder, :name
  def initialize(folder, name)
    @folder = folder
    @name = name
  end
end
```

The idea is, to locate any given document you need both document name and its folder.
Though, this did not compare effectively two documents, he propose to enhance this class.

#### equal in what sense?
Ruby has 4 ways to compare classes: `eql?`, `equal?`, `==` and `===`

## equal?
Ruby use `equal?` to test for object identity. It is going to return true only if both a and b, `a.equals?(b)`, references to identically the same objects. It will be nice if you don't override equal?. Ever.

## ==

*Double equals for Everyday Use*. It is the operator that habitually we redefine. The default implementation do the same of `equal?`, verify object identity. So Olsen propose this implementation:

```
class DocumentIdentifier
  #...
  def ==(other)
    return false unless other.instance_of(self.class)
    folder == other.folder && name == other.name
  end
end
```

`nil` is just a kind of object from another class, our guard clause will hold it.

trying to speed up the cheking:

```
class DocumentIdentifier
  #...
  def ==(other)
    return true if other.equal?(self)
    return false unless other.instance_of(self.class)
    folder == other.folder && name == other.name
  end
end
```

#### checking for any subclasses of document

```
class DocumentIdentifier
  #...
  def ==(other)
    return true if other.equal?(self)
    return false unless other.kind_of?(self.class)
    folder == other.folder && name == other.name
  end
end
```

This will avooid return false for every subclask of DocumentIdentifier

#### and how to check two independent classes?

```
class DocumentPointer
  attr_reader :folder, :name
  def initialize(folder, name)
    @folder = folder
    @name = name
  end
  
   def ==(other)
    return false unless other.respond_to?(:folder)
    return false unless other.respond_to?(:name)
    folder == other.folder && name == other.name
  end
end
```

### The well-behaved equality

respect the **symmetry** property, if a == b then b == a!!! *this don't occour between DocumentPointer and DocumentIdentifier.*

respect the **transitive** property, if a == b and b == c then a == c.

Olsen writes about how hard is to obey this common behavior (exemplified in previous properties), so he ends with the question, do you really wants to implement the operator? You could create a method `is_same_document?`, and avoiding, at least a little, these problems.

## ===
The main use of this is in *case statements*. Some uses cases:
```
location = 'area 51'
case location
  when /area.*/ #...
  when /roswell/ #...
  else #...
end
```
```
object = MyClass.new
case object
  when MyClass #...
  when OtherClass #...
  else #...
end
```

By default, `===` calls the double equals method. *Its probably a good idea to leave === alone unless doing so results in really ugly case statements.*

## eql?

It is usefull when you use your object as a key in hash.

### a dive into hash
*The idea behind a hash is to build a thing that works a lot like an array. The feature that makes hashes special is that they can take things other than just number as indexes.*

To avoid massive searches, hash tables improve the performance with a divide-and-conquer strategy. *Instead of maintaining a single key/value list, a typical hash table implementation maintains a number of lists, or* **buckets***. By spreading out the stuff that's stored in the table across a number of buckets, a hsh table can do things dramaticcaly faster.* Perhaps this behavior changes after Ruby 1.9, when Olsen books was written.

*The challenging thing with this scheme is picking the right bucket: If you are saving a new key/value pair, which bucket to use? When you go looking for that same key, how do you know which bucker you picked originally?*

*The idea foes like this: You define a method on all of your objects, a method which returns a hash value. The hash value is a more or less a random number somehow generated from the value of the object. When you need to store a key/value pair in you hash table, you pull the hash valeu from the key. You then use that number to pick a bucket - typically by using the modulo operator (hash_code % number_of_buckets) - and you store your key/value pair in that bucket. Later on when you are looking to retrieve the value asssociated with some key, you get the hash code for the key again and use it to pick the right bucket to search.* 
  
*hash codes needs to be stable*, it can't generate different hash codes from the same object at some time. *and they must be consistent with the value of the key*, if two keys are equal, then, they must return same hash code.

The Hash class uses the `eql?` method to decide if two keys are in fact the same key.

### The well-behaved hash key

The default implementation of `eql?` from the `Object class`, is based on object identity.

The default `eql?` method returns true only if the other object is identically the same as this object. The default `hash` method returns the `object_id` of the object, which is guaranteed to be unique.

As long as you follow the hash **Prime Directive - that if a.eql?(b) then a.hash == b.hash**.

At this point Olse returns to DocumentIdentifier to give us a good implementation of `eql?` and `hash`. *Given this, we want to make sure that both fields hava a say in the hash code.*

```
class DocumentIdentifier
  #...
  
  def hash
    folder.hash ^ name.hash
  end
  
  def eql?(other)
    return false unless other.instance_of?(self.class)
    folder == other.folder && name == other.name
  end
end
```

*Getting your objects to work as hash table keys is no time to be imaginative about cross-class equality*

## final considerations

Olsen will talk more about this latter, but keep in mind that `>=`, `<`, and even the `<=>` operator, that evaluates if a is greater than, equal than, or less then b, are some kind of equalities.