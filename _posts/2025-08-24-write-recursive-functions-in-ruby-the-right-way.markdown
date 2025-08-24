---
layout: post
title:  How to write recursive functions in Ruby the right way
description:
date:   2025-08-24 00:31:46.882708 -0500
author: sdemian
image:  '/images/2025-08-24-write-recursive-functions-in-ruby-the-right-way.png'
tags:   [ruby, resursion, TCO, tail-call-optimization]
tags_color: '#477690'
featured: true
---
## Have you ever wondered why it is not so easy to calculate the factoria of number 100000 in Ruby

Factorial calculation is a classical problem, when we are talking about the recursions in the Ruby programing language. Can one use Ruby to calculate the factoria of **1000!** - absolutely
Here is a simple example of the factorial function in Ruby:

```ruby
def fact(n)
  return 1 if n <= 1
  n * fact(n - 1)
end
```

### Let's run it:
```ruby
puts fact(5)
120
=> nil
```

Easy right!

### Now let's do it for some slightly bigger number:
```ruby
puts fact(100000)
(irb):3:in 'Object#fact': stack level too deep (SystemStackError)
```

Wow! That was not really expected! So what happened?

To understand the problem better, let's take a look at the sequence of operations that would happen if we want to calculate previous **fact(5)**:

```ruby
puts fact(5)

#=> 5 * fact(4)
#=> 5 * (4 * fact(3))
#=> 5 * (4 * (3 * fact(2))
#=> 5 * (4 * (3 * (2 * fact(1)))
#=> 5 * (4 * (3 * (2 * 1)))
#=> 5 * (4 * (3 * 2))
#=> 5 * (4 * 6)
#=> 5 * 24
#=> 120
```

From the example above it is obvious that operations keep stacking up with each recursive call to **fact** function.
First the Ruby interpreter is expanding to the very end of the recursion to return **1** to satisfy the **return condition** at **n <= 1**, and second it reduces expression to a single calculated value in the end.
Since during the recursive call the interpreter keeps track of all the previous values, it will keep all these intermediate values in the stack and since the stack size is limited, it will eventually on the big numbers like **100000** cause a SystemStackError, or stack overflow.

### Tail recursion

There is a better way how the previous **fact** function can be rewritten to pass the intermediate value inside parameters argument of the function call:

```ruby

def fact(n, memo=1)
  return memo if n <= 1
  fact(n-1, n * memo)
end
```

Please note that we have to initialize the starting value of the **memo** to 1 so that it will be correctly multiplied in next iterations, otherwise the value of the **memo** should be set during the function call like **fact(5, 1)**


Now let's look at the sequence of operations for the newly modified function **fact**:

```ruby
puts fact(5)

#=> fact(4, 5)
#=> fact(3, 20)
#=> fact(2, 60)
#=> fact(1, 120)
#=> 120
```

Much cleaner right, but also we achieved another effect and now we can call this new refined **fact** function a special **tail-recursive** function. A function is considered a **tail-recursive** if the recursive call is the very last operation performed before the function returns its result. This means that after the recursive call returns, no further computation or operations are needed within the current function's scope.

Now let's try to calculate the **fact(100000)** with new **tail-recursive** variant of the function:

```ruby
puts fact(100000)
(irb):16:in 'Object#fact': stack level too deep (SystemStackError)
```

This will still cause the **SystemStackError**, but why?

It turns out that that the Ruby interpreter needs to keep track of where to return after each execution of the function. Each recursive call to the **fact** method gets added to the call stack.


### Tail call optimization (TCO) in Ruby

Ruby has a way to tell to the interpreter to optimize the tail-recursive call in the runtime.
When tail call optimization takes place the tail recursion will work like a loop. Interpreter replaces each time the topmost stack frame with a new one, instead of stacking up the call stack.

By default tail call optimization is not enabled in the Ruby, but it can be enabled at runtime with a compile option:

```ruby
RubyVM::InstructionSequence.compile_option = {
  tailcall_optimization: true,
  trace_instruction: false
}

def fact(n, memo=1)
  return memo if n <= 1
  fact(n-1, n * memo)
end

puts fact(100000)
```

Now you will be able to get the calculated value of the **100000!** and there should be no **SystemStackError** error.

### Why TCO is not enabled by default in Ruby

Major problem with TCO is that it messes up the call stack and stack traces, which makes debugging harder, however if you know what you are doing, you can enable the TCO during the runtime and have all the power of the Tail call optimization (TCO) in Ruby.

### Further reading

  - Blog post from **Guido van Rossum** about the [Tail Recursion Elimination in Python](https://neopythonic.blogspot.com/2009/04/tail-recursion-elimination.html).

Congratulations 🏆 on learning about **How to write recursive functions with TCO** in Ruby.
