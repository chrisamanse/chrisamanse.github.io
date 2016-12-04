---
layout: post
title:  "Catching Multiple Errors in Swift"
date:   2016-12-03 22:41:00 -0800
categories: swift
---

Currently, I'm building a one-time password generator app, and for the part in validating user input, I'm using Swift's error-handling statements to catch errors in the input. In order to write less code, I tried catching multiple errors in a catch statement:

```swift
do {
  try validate(input)
} catch InvalidInput.noAccount, InvalidInput.noKey {
  // No account and no key
}
```

As it turns out, it's not yet possible in Swift. Therefore, I tried to find "ways" to catch multiple errors in Swift.

## First Solution: Recursive Enum

My first attempt to solve this is to add a case in the `enum` that has an associated value of an array of cases:

```swift
enum InvalidInput: Error {
  case noAccount
  case noKey
  indirect case errors([InvalidInput])
}
```
 
Now, for the catch statement, all I have to do is catch the `InvalidInput.errors` case:

```swift
do {
  try validate(input)
} catch InvalidInput.errors(let errors) where errors == [.noAccount, .noKey] {
    // Handle no account, and no key case
}
```

That's great! However, since `errors` is an array, the **order matters** when comparing with another array. Thus, if `errors` is equal to `[.noKey, .noAccount]`, the error will not be caught by the catch statement above. To fix this, we can use a `Set` instead of an `Array`. But, we still have to conform the `InvalidInput` enum to the `Hashable` protocol. That seems to complicate our code more.

## Second Solution: OptionSet

My first attempt was not really a pretty solution. The reason is that I still tried to use an enum. The beauty of Swift's error handling is that we can throw **any type** that conforms to the `Error` protocol. That means, we can use a `struct` instead that conforms to `OptionSet`.

```swift
struct InvalidInput: OptionSet, Error {
  public var rawValue: UInt8
  
  public init(rawValue: UInt8) {
    self.rawValue = rawValue
  }
  
  static let noAccount = InvalidInput(rawValue: 1 << 0)
  static let noKey     = InvalidInput(rawValue: 1 << 1)
}
```

We can now simply throw an `InvalidInput` type instead of creating an array of errors:

```swift
func validate(_ input: Input) throws -> Void {
  var errors: InvalidInput = []
  
  if !input.hasAccount {
    errors.insert(.noAccount)
  }
  
  if !input.hasKey {
    errors.insert(.noKey)
  }
  
  guard errors.isEmpty else {
    throw errors
  }
  
  print("No errors found")
}
```

For the catch statement, we can catch the error variable instead:

```swift
do {
  try validate(input)
} catch let error as InvalidInput {
  // Handle error
}
```

### Error messages

We can even extend the `InvalidInput` type to give it's error messages:

```swift
extension InvalidInput {
  var errorMessages: [String] {
    let messages = [String]()
    
    if self.contains(.noAccount) {
      messages.append("Account is required.")
    }
    
    if self.contains(.noKey) {
      messages.append("Key is required.")
    }
    
    return messages
  }
}
```

Finally, here's our catch statement:

```swift
do {
  try validate(input)
} catch let error as InvalidInput {
  let message = error.errorMessages.joined(separator: " ")
  showAlert(title: "Found Errors", message: message)
}
```

If we have more options, we can even have catch statements that catches specific options only:

```swift
do {
  try validate(input)
} catch [.invalidAccount, .invalidKey] as AddAccountInvalidInput {
  // Handle invalid inputs
} catch [.accountExists, .noKey] as AddAccountInvalidInput {
  // Account exists, and no key
} catch .noAccount {
  // No account
}
```

That's it! By using an `OptionSet` instead, we can have more flexible catch statements. This is especially useful for showing errors in a form. Instead of having one error message, we can inspect if the thrown error contains specific errors, and display that error in the corresponding input field.

Here's the final code:

```swift
struct InvalidInput: OptionSet, Error {
  public var rawValue: UInt8
  
  public init(rawValue: UInt8) {
    self.rawValue = rawValue
  }
  
  static let noAccount = InvalidInput(rawValue: 1 << 0)
  static let noKey     = InvalidInput(rawValue: 1 << 1)
  
  var errorMessages: [String] {
    let messages = [String]()
    
    if self.contains(.noAccount) {
      messages.append("Account is required.")
    }
    
    if self.contains(.noKey) {
      messages.append("Key is required.")
    }
    
    return messages
  }
}
```
