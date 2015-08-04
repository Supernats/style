class: center, middle

# Style

---

class: center, middle

## Multi-line method chaining.

---

> When continuing a chained method invocation on another line keep the `.` on the second line.
> > -- style guide

```ruby
# bad
one.two.three.
  four

# good
one
  .two
  .three
  .four
```

---

> When continuing a chained method invocation on another line keep the `.` on the first line.
> > -- Nathan

```ruby
# bad
one.two.three.
  four

# good
one.
  two.
  three.
  four
```

---

class: center, middle

## `!!`

---

> Avoid the use of `!!`.
> > -- style guide

```ruby
# bad
x = 'test'
# obscure nil check
if !!x
  # body omitted
end

x = false
# double negation is useless on booleans
!!x # => false

# good
x = 'test'
unless x.nil?
  # body omitted
end
```

---

> Don't go crazy with `!!`. Consider having that functionality in a boolean method that is called elsewhere. 
> > -- Nathan

```ruby
# bad
x = 'test'
# obscure nil check
if !!x
  # body omitted
end

x = false
# double negation is useless on booleans
!!x # => false

# good
def x?
  !!x
end

x = 'test'
unless x?
  # body omitted
end
```

---

class: center, middle

## Parens and Params

---

> Omit parentheses around parameters for methods that are part of an internal DSL (e.g. Rake, Rails, RSpec), methods that have "keyword" status in Ruby (e.g. `attr_reader`, `puts`) and attribute access methods. Use parentheses around the arguments of all other method invocations.
> > -- style guide

```ruby
class Person
  attr_reader :name, :age

  # omitted
end

temperance = Person.new('Temperance', 30)
temperance.name

puts temperance.age

x = Math.sin(y)
array.delete(e)

bowling.score.should == 0
```

---

> Omit parentheses around paremeters for a method that is being used for its side-effect rather than its return. If the method is being used for its return, use parentheses.
> > -- Nathan

```ruby
class Person
  attr_reader :name, :age

  def self.create(name, age)
    new(name, age).after_init_stuff
  end
end

class RailsPerson < ActiveRecord::Base
  attr_accessible :name, :age
end

# Uses same API regardless of inheritance
temperance = Person.create 'Temperance', 30
rails_temperance = RailsPerson.create 'Temperance', 30

temperance.name
puts temperance.age

array.delete e
el = array.delete(e)

bowling.score.should == 0
```

---

class: center, middle

## Bang Methods

---

> The names of potentially dangerous methods (i.e. methods that modify `self` or the arguments, `exit!` (doesn't run the finalizers like `exit` does), etc.) should end with an exclamation mark if there exists a safe version of that dangerous method.
> > -- style guide

```ruby
# bad - there is no matching 'safe' method
class Person
  def update!
  end
end

# good
class Person
  def update
  end
end

# good
class Person
  def update!
  end

  def update
  end
end
```

---

> The names of potentially dangerous methods (i.e. methods that modify `self` or the arguments, `exit!` (doesn't run the finalizers like `exit` does), etc.) should end with an exclamation mark. If there is a safe version of the dangerous method, all the better.
> > -- Nathan

```ruby
# okay - there is no matching 'safe' method,
# but thank you for warning me.
class Person
  def update!
  end
end

# less okay - will `update` modify some remote state somewhere?
class Person
  def update
  end
end

# good
class Person
  def update!
  end

  def update
  end
end
```

---

class: center, middle

# Thanks for listening to me rant!
