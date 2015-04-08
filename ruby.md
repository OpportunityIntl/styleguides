#Ruby Style Guide
Adapted from [GitHub Ruby styleguide](https://github.com/styleguide/ruby), itself influenced by [bbatsov's ruby-style-guid](https://github.com/bbatsov/ruby-style-guide)

If you're working in OptINnow, you'll notice that Opportunity isn't following any consistent styles. The app has passed through several Rails versions and developers, so the code is all over the place. Moving forward, let's adhere to these styles.


##Coding style
- Use soft-tabs with 2 spaces
- Try to keep lines fewer than 80 characters
- Use spaces around operators; after commas, colons, and semicolons; around `{` and before `}`

```ruby
sum = 1 + 2
a, b = 1, 2
1 > 2 ? true : false
[1, 2, 3].each { |e| puts e }
```

- No spaces after `(`, `[` or before `]`, `)`

```ruby
some(arg).other
[1, 2, 3].length
```

- Indent `when` as deep as `case`

```ruby
case
when song.name == "Misty"
  puts "Not again!"
when song.duration > 120
  puts "Too long!"
else
  song.play
end
```

##Syntax
- Use `def` with parentheses when there are arguments. Omit the parentheses when the method doesn't accept any arguments.

```ruby
def some_method
  # blah blah blah
end

def some_method_with_arguments(arg1, arg2)
  # blah blah blah
end
```

- Never use `for`, unless you know exactly why. Most of the time iterators should be used instead. `for` is implemented in terms of `each` (so you're adding a level of indirection), but with a twist - `for` doesn't introduce a new scope (unlike `each`) and variables defined in its block will be visible outside it.

```ruby
arr = [1, 2, 3]

# bad
for elem in arr do
  puts elem
end

# good
arr.each do |elem|
  # blah blah blah
end

# also good
arr.each { |elem| puts elem }
```

- Avoid the ternary operator `(?:)` except in cases where all expressions are extremely trivial. However, do use the ternary operator `(?:)` over `if/then/else/end` constructs for single line conditionals.
```ruby
# bad
result = if some_condition then something else something_else end

# good
result = some_condition ? something : something_else
```

- Don't use the `and` and `or` keywords in conditionals. Always use `&&` and `||` instead. See [this article](http://devblog.avdi.org/2010/08/02/using-and-and-or-in-ruby/) for more information regarding the difference.
- Avoid using `unless` with `else`. Rewrite these with the positive case first.

```ruby
# bad
unless success?
  puts "failure"
else
  puts "success"
end

# good
if success?
  puts "success"
else
  puts "failure"
end
```

- Prefer `{...}` over `do...end` for single-line blocks. Avoid using `{...}` for multi-line blocks (multiline chaining is always ugly). Always use `do...end` for "control flow" and "method definitions" (e.g. in Rakefiles and certain DSLs). Avoid `do...end` when chaining.
```ruby
names = ["Bozhidar", "Steve", "Sarah"]

# good
names.each { |name| puts name }

# bad
names.each do |name|
  puts name
end

# good
names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

# bad
names.select do |name|
  name.start_with?("S")
end.map { |name| name.upcase }
```

- Avoid `return` where not required.
```ruby
# bad
def some_method(some_arr)
  return some_arr.size
end

# good
def some_method(some_arr)
  some_arr.size
end
```

- Use spaces around the `=` operator when assigning default values to method parameters:
```ruby
# bad
def some_method(arg1=:default, arg2=nil, arg3=[])
  # do something...
end

# good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
  # do something...
end
```

- Use `||=` freely to initialize variables.
```ruby
# set name to Bozhidar, only if it's nil or false
name ||= "Bozhidar"
```

- Don't use `||=` to initialize boolean variables. (Consider what would happen if the current value happened to be false.)
```ruby
# bad - would set enabled to true even if it was false
enabled ||= true

# good
enabled = true if enabled.nil?
```

- Never put a space between a method name and the opening parenthesis.
```ruby
# bad
f (3 + 2) + 1

# good
f(3 + 2) + 1
```

- Use `_` for unused block parameters.
```ruby
# bad
result = hash.map { |k, v| v + 1 }

# good
result = hash.map { |_, v| v + 1 }
```

##Naming

- Use `snake_case` for methods and variables.
- Use `CamelCase` for classes and modules. (Keep acronyms like HTTP, RFC, XML uppercase.)
- Use `SCREAMING_SNAKE_CASE` for other constants.
- The names of predicate methods (methods that return a boolean value) should end in a question mark. (i.e. Array#empty?).
- The names of potentially "dangerous" methods (i.e. methods that modify `self` or the arguments, `exit!`, etc.) should end with an exclamation mark. Bang methods should only exist if a non-bang method exists. [More on this](http://dablog.rubypal.com/2007/8/15/bang-methods-or-danger-will-rubyist).
