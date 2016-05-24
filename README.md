# Booleans

![Dolphin Guy](http://i.giphy.com/RdkwfjGlsdnRm.gif)

## Objectives

1. Describe the `Bool` data type
1. Create Boolean variables with literal values
1. Use comparison operators on Boolean variables
1. Use logic operators on Boolean variables

## Understanding Booleans

You are already familiar with creating `Int` variables and constants, which can store single numeric integer values, like

```swift
var numberOfApples = 7
let numberOfOranges = 12
```

In this lesson, we will learn about the boolean data type, which represents a value that can either be true or false. Swift provides constant literal values for both possibilities, which can be used like the integer literals you are already familiar with:

```swift
let isTheSkyBlue = true
let canHumansFly = false
```

Creating and using a variable of this type also works like the types you already know:

```swift
var isTheGrassGreen = false
isTheGrassGreen = true
```

In both of these examples, the Swift compiler has inferred the type from our use of the literal values, but we can also explicitly write out the type if we want to:

```swift
let canDolphinsWalk: Bool = false
```

## Comparing values

A common use of the `Bool` type is as a result of a comparison of other values. Comparing two values in Swift is done with an *operator*, which is a special symbol that you use to check, combine or change one or more values.

For example, we can compare the two integer variables from our earlier example, to see if they are equal, using the equal-to operator:

```swift
let doWeHaveAsManyApplesAsOranges = numberOfApples == numberOfOranges // false, because 7 is not equal to 12
```

The result in this case is of course `false`, because 7 and 12 are not equal numbers. We can also determine if two values are **not** equal, like this:

```swift
let compareApplesToOranges = numberOfApples != numberOfOranges // true, because 7 is indeed not equal to 12
```

In this case, the result is `true`. We may also be interested in learning if we have more apples than oranges, for this we have operators for greater and less than:

```swift
let moreApplesThanOranges = numberOfApples > numberOfOranges // false, because 7 is not greater than 12
let lessApplesThanOranges = numberOfApples < numberOfOranges // true, because 7 is less than 12
```

Finally, there are also comparison operators for greater and less than or equal. Those will either be true if the two operands are equal or if the left hand side is greater, or respectively less, than the right hand side.

```swift
let lessOrTheSameNumberOfApplesAndOranges = numberOfApples <= numberOfOranges // true, because 7 is less than 12

numberOfApples = 12
let moreOrTheSameNumberOfApplesAndOranges = numberOfApples >= numberOfOranges // true, because 12 is not greater than 12, but 12 is equal to 12
```

These comparisons might not seem too useful on their own, but you will learn later how you can use them in *conditional expressions* to execute different statements in your programs, depending on the value of these kind of conditions.

## Logical operations

In the last example, we already saw a simple logical statement for our program, we were able to determine if two values are greater than or equal to each other. Boolean values can also be combined using *logical operators* to formulate more complex logical statements about variables. 

The logical `NOT` operator inverts the value of a Boolean, so that `true` becomes `false` and vice versa. This operator is a *unary* operator, because it operates on a single value, in contrast to the *binary* comparison operators, which operate on two values. The operator is put in front of the operand, without any whitespace between them:

```swift
let asManyApplesAsOranges = false
let notAsManyApplesAsOranges = !asManyApplesAsOranges // true
```

It can be read as *not* `asManyApplesAsOranges` to make its use as a prefix clearer. If we choose our variable names carefully, we can ensure that such logical expressions can be read like this and make our code more readable in that way.

The logical `AND` operator forms a logical expression which is `true` if both values are `true`.

```swift
let isTheSkyBlue = true
let isTheGrassGreen = true
let canHumansFly = false
let canDolphinsWalk = false

let isTheSkyBlueAndTheGrassGreen = isTheSkyBlue && isTheGrassGreen // true, because both values are true
let canHumansFlyAndIsTheSkyBlue = canHumansFly && isTheSkyBlue // false, because canHumansFly is false
let canHumansFlyAndDolphinsWalk = canHumansFly && canDolphinsWalk // false, because both values are false
```

Since the statement will be `false` if a single value is `false`, an expression `canHumansFlyAndIsTheSkyBlue` will stop evaluating after checking `canHumansFly`, because that is already `false`. This method is called *short circuiting*. If the second value is the result of a function, that function would not even be called:

```swift
func printIfCalled() -> Bool {
	print("Function is called.")
	return true
}

let fullEvaluation = true && printIfCalled() // Will print "Function is called."
let shortCircuit = false && printIfCalled() // Nothing will be printed, because of short circuiting
```

In contrast to that, the logical `OR` operator will evaluate to `true` if at least one of the values is `true`:

```swift
let isTheSkyBlue = true
let isTheGrassGreen = true
let canHumansFly = false
let canDolphinsWalk = false

let isTheSkyBlueOrTheGrassGreen = isTheSkyBlue || isTheGrassGreen // true, because both values are true
let canHumansFlyOrIsTheSkyBlue = canHumansFly || isTheSkyBlue // true, because isTheSkyBlue is true
let canHumansFlyOrDolphinsWalk = canHumansFly || canDolphinsWalk // false, because both values are false
```

We already saw the logical `OR` in action, without having to write it out when we used the *less than or equal* operator earlier. We can write a function that works exactly like that operator, using just the *less than* and the *equal to* operator:

```swift
func lessThanOrEqual(first: Int, to second: Int) -> Bool {
	return first < second || first == second
}

let A = 7
let B = 12
let C = 12

let isAlessThanOrEqualToB = lessThanOrEqual(A, to: B) // true, because 7 is less than 12
let isBlessThanOrEqualToC = lessThanOrEqual(B, to: C) // true, because 12 is equal to 12
let isClessThanOrEqualToA = lessThanOrEqual(C, to: A) // false, because 12 is not less than 7 and it is also not equal to 7
```

It is also possible to combine multiple logical operations to form more complex statements:

```swift
let isTheSkyBlue = true
let isTheGrassGreen = true
let canHumansFly = false
let canDolphinsWalk = false

let result = isTheSkyBlue && isTheGrassGreen || canHumansFly || canDolphinsWalk // true
```

In cases like this, it can be hard to figure out what is going on, so we can use parentheses to make the same expression much clearer:

```swift
let result = (isTheSkyBlue && isTheGrassGreen) || (canHumansFly || canDolphinsWalk) // true
```

When writing code, you should always prefer making it clearer to making it shorter, to make it easier for other people to understand what you meant, but also to make your own life easier when you come back to the code later on.
