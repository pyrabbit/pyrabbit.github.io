---
layout: post
title: Before and After Callbacks with Ruby
---


Disclosure, this is just a concept and not necessarily the most effective way of implementing your own before and after callbacks using Ruby.

I always loved using the before_action method from the ActiveController gem that is commonly used in Ruby on Rails implementations. I wanted to challenge myself to replicate this feature as much as I can and this is the closest solution I could come up with. So this was just me having some fun and experimenting with Ruby blocks.

```ruby
# Variables to store the list of actions that have callbacks
@before_actions = Hash.new {|hash,key| hash[key] = Array.new}
@after_actions = Hash.new {|hash,key| hash[key] = Array.new}

# Defining the before_action method
# action is the callback to be executed, methods
# is an array of actions that have callbacks assigned to them

def before_action(action, methods)
  methods.each do |m|
    @before_actions[m] << action
  end
end

def after_action(action, methods)
  methods.each do |m|
    @after_actions[m] << action
  end
end

# block used inside or methods that allows us to
# use these callbacks

def execute_callbacks
  @before_actions.each {|k,v| v.each {|v| send(v)}}
  yield
  @after_actions.each {|k,v| v.each {|v| send(v)}}
end

# declaring the before and after actions that we want to occur
before_action :first_do_this, [:do_something]
after_action :lastly_do_this, [:do_something]

def first_do_this
  puts "this occurs first"
end

def lastly_do_this
  puts "this occurs last"
end

# Our method that we want to work around. Kudos if you can help me
# figure out how to get this to work without having to call
# execute_callbacks in each one

def do_something
  execute_callbacks do
    puts "hello world"
  end
end
```

I would have to do some testing to decide whether or not I would actually want to use something like this. If you any suggestions for improvements I would love to hear them! It would help me as well as other I'm sure.
