#Ruby Style Guide
Adapted from [GitHub Ruby styleguide](https://github.com/styleguide/ruby), itself influenced by [bbatsov's ruby-style-guid](https://github.com/bbatsov/ruby-style-guide)

If you're working in OptINnow, you'll notice that Opportunity isn't following any consistent styles. The app has passed through several Rails versions and developers, so the code is all over the place. Moving forward, let's adhere to the styles.


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

- No spaces after `(`, `[` or beore `]`, `)`

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

- Never use for, unless you know exactly why. Most of the time iterators should be used instead. for is implemented in terms of each (so you're adding a level of indirection), but with a twist - for doesn't introduce a new scope (unlike each) and variables defined in its block will be visible outside it.

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

