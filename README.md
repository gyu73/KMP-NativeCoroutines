# KMP-NativeCoroutines

A library to use Kotlin Coroutines from Swift code in KMP apps.

## Installation

Add the Kotlin library to your common dependencies:
```kotlin
implementation("com.rickclephas.kmp:kmp-nativecoroutines-core:0.1.0")
```

and add the Swift library to your `Podfile`:
```ruby
pod 'KMPNativeCoroutinesCombine'
```

## Usage

To use Kotlin Coroutines from Swift you will need to:
1. Add some extension properties/functions to your Kotlin native code.
2. Use the wrapper functions in Swift to get Combine publishers.

### Flows

#### Kotlin

Create an extension property to expose the `Flow` as a `NativeFlow` to Swift:

```kotlin
val Clock.timeNative
    get() = time.asNativeFlow()
```

#### Swift Combine

Use the `createPublisher(for:)` function to get an `AnyPublisher` for the `NativeFlow`:

```swift
let publisher = createPublisher(for: clock.timeNative)
```

### Suspend functions

#### Kotlin

Create an extension function to expose the suspend function as a `NativeSuspend` to Swift:

```kotlin
fun RandomLettersGenerator.getRandomLettersNative() =
    nativeSuspend { getRandomLetters() }
```

#### Swift Combine

Use the `createFuture(for:)` function to get an `AnyPublisher` for the `NativeSuspend`:

```swift
let future = createFuture(for: randomLettersGenerator.getRandomLettersNative())
```