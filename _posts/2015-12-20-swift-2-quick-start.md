---
layout: post
title:  "Swift 2 Quick Start"
date:   2015-12-20 23:50:00 +0800
categories: swift programming
---

Recently, Apple has open sourced their own programming language, Swift, which is currently in version 2.1. Just after a few days of their release in [GitHub](https://github.com/apple/swift), it became the most popular open sourced programming language. Apple, with contributors worldwide, is continuously developing and improving Swift, thus the more reason for us to start learning Swift. Apple's vision for Swift really is for people to use Swift in all kinds of cases such as web development as well. So, let's start learning Swift.

> This tutorial is for experienced programmers. *If you're beginning to learn programming, the best way to learn with Swift is by reading Apple's official book, [The Swift Programming Language](https://swift.org/documentation/), the official documentation for Swift.*

I suggest you use an Xcode Playground to follow this tutorial since it displays the contents of the variables as you write your code without needing to compile your code.

## Hello World

The simplest program you can make, as with most programming languages, is a Hello World program. To print out a `String`, you can simply use the `print` function: `print("Hello World!")`. That's it. No import statements, namespace, prefixes, main function, etc. Also note that Swift doesn't require you to put semi-colons at the end of one-line statements, so you can type code faster and get less errors when compiling. Although, you have to put semi-colons if you decide to write more than one statement in a single line (*Why would you??*)

## Variables and Constants
Now that you now how to print output, let's move on with variables and constants. In Swift, we declare variables with the `var` keyword. On the other hand, if you want a constant, you have to use `let`. The main difference between a variable and a constant is that with constants, you can't change it's value once you've assigned it one.

{% highlight swift %}

let pi = 3.14159265
var completed = false
completed = true

{% endhighlight %}

> To print out values of numbers or other types, you can simply use string interpolation, `"The value of pi is \(pi)"`.

As you've noticed from the example above, we did not need to explicitly state the type of the variable or constant at declaration. Swift automatically infers the type of the variable from the value you assign to it. So if you assign `10` to a variable, `var anInteger = 10` , the variable is an integer type, or an `Int`. In the examples above, `pi` has an inferred type of `Double`, and `completed` of type `Bool`. Once a variable is assigned a type, it can never change its type, so, you can't assign `completed` an `Int` type.

{% highlight swift %}

completed = 5 // error, won't compile

{% endhighlight %}

We can also explicitly state the type of a variable we declare:

{% highlight swift %}

let doubleValue: Double = 10

{% endhighlight %}

This way, `doubleValue` is of type double with a value `10.0`. These are some of the basic types for Swift: `Int`, `Double`, `Float`, `Bool`, and `String`.

#### Array

Lastly, you can create `Array`s using brackets around a type, such as `[Int]` for creating an array of integers.

{% highlight swift %}

let numbers: [Int] = [1, 4, 7, 10, 13, 16]
let heights = [170.5, 200.89, 145.0] // Inferred of type [Double]
var emptyNumbers: [Int] = [] // Create empty array

emptyNumbers.count == 0
numbers.count = 6

{% endhighlight %}

### Casting

Casting to other types is simple in Swift. The basic types of Swift are structs, so most of them also provide initializers for other type such as:

{% highlight swift %}

let withDecimal = 1.5
let withoutDecimal = Int(1.5) // Since Int has an initializer with a double parameter

{% endhighlight %}

### Optionals

Another unique feature of Swift are the use of Optional types. Optional types are types that can either have some value or none (`nil` or `null` in other programming languages). Optionals can be applied to all types, such as `Int`, or `String`. To indicate if a type is an optional, we simply append a `?` at the end of the type: `Int?` as an optional integer, and `String?` as an optional integer.

{% highlight swift %}

let doubleValueNil: Double? = nil

doubleValueNil == nil // true

let helloWorldString: String? = "Hello World!"

helloWorldString != nil // true

{% endhighlight %}

Take note that since an optional integer (`Int?`) is different to an integer (`Int`), you can't assign an optional to a non-optional (`Int?` -> `Int`). In order to assign the value of an optional, if it has a value, you have to unwrap the optional first. The simplest way to unwrap is through the usage of the force unwrap operator `!`.

{% highlight swift %}

let someValue: Int? = 10
var anInteger: Int = 0

anInteger = someValue // error
anInteger = someValue! // Works!

{% endhighlight %}

However, most of the time, **FORCE UNWRAPPING IS A BAD IDEA**. Try the same code above, but with `nil` assigned to `someValue`. The result is an error, specifically a runtime error - the code would compile, and the program will run, but the program will crash once the program tries to force unwrap an empty optional. In short, **your app will crash**. So, you might think that to prevent force unwrapping an empty optional, you will check if it's not nil first. Yes, that will be safer, and prevent your program from crashing. Although, Swift provides a better way for safely unwrapping an optional, which is called *optional binding*.

{% highlight swift %}

let someValue: Int? = 10
var anInteger: Int = 0

if let unwrappedOptional = someValue {
  // If someValue is not nil, it's value will be assigned to unwrappedOptional, which is now of type Int
  anInteger = unwrappedOptional
} else {
  print("someValue is empty")
}

{% endhighlight %}

## Operators

Swift mostly has the same operators with other languages, such as `+`, `-`, `*`, `/`, `%` for basic operations. `+` also supports `String`s and `Array`s. Swift also has shorthand operators for arithmetics: `+=`, `-=`, `*=`, and `/=`, where `a += b` is the same with `a = a + b`.

{% highlight swift %}

// Strings
let firstName = "Jane"
let lastName = "Doe"

let fullName = firstName + " " + lastName

// Arrays
let a = [1, 2]
let b = [3, 4]

let c = a + b // [1, 2, 3, 4]

{% endhighlight %}

Swift also has the basic comparison operators, `<`, `==`, `<=`, `>=`, `!=`, `!`. Take note that `!` for NOT is different from the `!` for force unwrapping optionals. `!` for NOT is a prefix, while `!` for unwrapping is a suffix.

## Control Flow

### Conditions

As you've seen from the example above in *optional binding*, Swift also has `if-else` statements. Swift, as with other modern languages, doesn't require parenthesis in conditions.

{% highlight swift %}

let x = 999
if x < 1000 {
  // ...
} else if x == 1000 {
  // ...
} else {
  // x is greater than 1000
}

{% endhighlight %}

Swift also has a `switch` statement. However, unlike other languages, it doesn't require you to put `break`s on every case, which is good since you rarely have to fall-through cases. Though, if you ever need to fall-through, you can always use the `fallthrough` keyword.

{% highlight swift %}

let x = 0
switch x {
  case 0:
    print("x is 0")
  case 1:
    print("x is 1")
  case 2, 3:
    print("x is 2 or 3")
  case 100..<1000: // 100, 101, ..., 999
    print("x has 3 digits")
  default:
    print("x is not 0 or 1")
}

{% endhighlight %}

### Loops

The most basic loop you can do in Swift is to iterate through a range, for example, from 0 to 9, using the `for-in` loop.

{% highlight swift %}

for i in 0..<10 { // Excluding 10
  print("i is \(i)") // Will print out "i is 0" up to "i is 9"
}

for i in 0...10 { // Including 10
  print("i is \(i)") // Will print out "i is 0" up to "i is **10**"
}

{% endhighlight %}

Of course, you can also do this with C-style loops with iterators:

{% highlight swift %}

for var i = 0; i < 10; i++ {
  // Code ...
}

{% endhighlight %}

Note that Apple **will remove** this C-style loop in Swift 3.0. So if you ever need to iterate through a loop with different increment magnitude, you can always use the `stride` method of numbers.

{% highlight swift %}

for i in 0.stride(to: 10, by: 2) {}
// is similar to for var i = 0; i < 10; i += 2 {}

// -- OR --

for i in 0.stride(through: 10, by: 2) {}
// is similar to for var i = 0; i <= 10; i += 2 {}

{% endhighlight %}

The next basic loop is the `while` loop, which is pretty much the same with most languages.

{% highlight swift %}

var x = 0
while x < 1000 {
  print(x)
  x++
}

{% endhighlight %}

Usually paired with the `while` loop is the `do-while` loop. In Swift, they call use `repeat-while` instead for a more readable language.

{% highlight swift %}

var x = 0
repeat {
  print(x)
  x++
} while x < 1000

{% endhighlight %}

## Functions

Functions with Swift are declared with the `func` keyword, followed by the function name, and a parenthesis containing the parameters if any. To indicate the function returns something, use `-> Type` after the parenthesis where Type is the return type.

{% highlight swift %}

// No return value (Void)
func printLineReturn() {
  print("")
}

// With Int as return value
func factorial(n: Int) -> Int {
  switch n {
    case 0, 1:
      return 1
    default:
      return n * factorial(n - 1)
  }
}

{% endhighlight %}

### Named Parameters

Functions in Swift have named parameters after the first parameter. By default, the parameter name is the same as the parameter's variable name. To change this, you can type in the name of the parameter before the variable name (to make the function more readable if necessary). You can also type in a parameter name for the first parameter to require a parameter name for it.

{% highlight swift %}

func addNumber(first: Int, second: Int) -> Int {
  return first + second
}

addNumber(1, second: 5)

func addNumber(first: Int, withNumber second: Int) -> Int {
  return first + second
}

addNumber(1, withNumber: 6)

func add(first first: Int, second: Int) -> Int {
  return first + second
}

add(first: 1, second: 8)

{% endhighlight %}

You can also remove the parameter name by using underscore, _ , in place of it.

{% highlight swift %}

func add(first: Int, _ second: Int) -> Int {
  return first + second
}

add(1, 7)

{% endhighlight %}

## Concluding Notes

So that's it for a quick start of Swift. I hope this tutorial helped you get started with Swift, or at least encourage you to learn Swift. There are still lots of topic I did not cover, such as tuples, Classes, Structs, Enums, etc. There's also an interesting feature for pattern matching in Swift:

{% highlight swift %}

let x = 0

switch x {
  case x where x < 0:
    print("x < 0")
  case x where x == 1000:
    print("x == 1000")
  default:
    print("x >= 0 && x != 1000")
}

{% endhighlight %}

If that doesn't interest you enough, skim through the [The Swift Programming Language](https://swift.org/documentation/) ebook to look for more advanced and cool stuff in Swift. If you want to see some examples of Swift code, I got some open source libraries and apps in [GitHub](https://github.com/chrisamanse).
