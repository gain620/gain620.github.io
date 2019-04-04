---
published: true
layout: single
title: "Using defer in Swift"
date: 2019-04-05
category: post
tags: [programming, ios, swift]
comments: true
---
The defer keyword has been introduced in Swift 2.0, although its usage seems to be very rare in real-world projects. However, using defer may improve your codebase enormously, so let's take a time to learn what on earth is "defer".

## What is defer?

```swift
func playMovie() {
	var movieName : String = "Sing Street"

	defer { print("Finished loading, now playing \(movieName)!") }

	print("Loading \(movieName)!!!")

	playQueue.append(movieName)
}

// Loading Sing Street!!!
// Finished loading, now playing Sing Street!
```
A defer keyword is used for executing code just before transferring program control outside of the scope that the statement appears in.
So as you see in the above example, defer block will be executed at the end.

## Real-world use cases
The most common use case seen around is opening and closing a context within a scope, for example when handling access to files. A "FileHandle" requires to be closed once the access has been finished. You can benefit from the defer statement to ensure you don’t forget to do this.

```swift
func writeFile() {
    let file: FileHandle? = FileHandle(forReadingAtPath: filepath)
    defer { file?.closeFile() }

    // Write changes to the file
}
```

A more advanced usage of the statement is by ensuring a result value to be returned in a completion callback. This can be very handy as it’s easy to forget to trigger this callback.

```swift
func getData(completion: (_ result: Result<String>) -> Void) {
    var result: Result<String>?

    defer {
        guard let result = result else {
            fatalError("We should always end with a result")
        }
        completion(result)
    }

    // Generate the result..
}
```

The statement makes sure to execute the completion handler at all times and verifies the result value. Whenever the result value is nil, the fatalError is thrown and the application fails.

## Bonus

If you use multiple defer statements in the same scope, they’re executed in reverse order of appearance — like a stack. This reverse order is a vital detail, ensuring everything that was in scope when a deferred block was created will still be in scope when the block is executed.

```swift
do {
    defer { print("1") }
    defer { print("2") }
}
//  2
//  1
```


#### References
[1.defer-usage-swift](https://www.avanderlee.com/swift/defer-usage-swift/)
[2.guard & defer](https://nshipster.com/guard-and-defer/)