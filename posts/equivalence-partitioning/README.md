# Equivalence Partitioning

Equivalence partitions are ranges of values that can be treated the same for testing purposes. For example, given a function that adds two numbers together, it may be valuable to check that it can add `1` to `2`. However, once you've verified that, verifying that `1` can be added to `3` is unlikely to reveal any new insights into the code. That's because `2` and `3` are part of the same equivalence partition.

## Equivalence Partitions and Boundaries

Equivalence partitions are always specific to the context. For example, a function that should accept an array of no more than 10 string elements might have the following partitions:

* Empty array
* Array with between 1 and 10 strings
* Array with 11 or more strings

A boundary is where values change from one partition to another. For example, the above case has the following boundaries:

* Array with 1 string (boundary between empty and 1-10)
* Array with 10 strings (boundary between 1-10 and 11 or more)

Boundaries are also useful to test because they're the most likely place for mistakes to occur.

How many partitions and boundaries you test for a piece of code should be proportional to how likely or critical a missed failure is, as well as how generic the code is. If piece of code being used incorrectly has safety implications, it's probably useful to assert behavior for every partition and every boundary. Similarly, a generic utility library that could be used in any number of contexts should provide cover a lot of partitions and boundaries. The rest of the time, it's OK to stick to partitions and boundaries that are the most common or express the purpose of the code the best.

In formulating which boundaries and partitions you want to test, consider the following cases.

### Strings

* An empty string
* A single character
* Multiple characters
* String with newlines
* String with unicode characters
* The maximum string length on the platform. The longest string supported by the JavaScript spec is 2^53, but in practice the number supported by each runtime is much lower.

### Numbers

* `-1`
* `0`
* `1`
* Integers greater than 1
* Integers less than -1
* Postive rational numbers
* Negative rational numbers
* Positive irrational numbers
* Negative irrational numbers
* Postive integer boundary
* Highest integer supported on the platform
  * There's a built-in constant representing this which you can access with `Number.MAX_SAFE_INTEGER`
* Highest decimal supported on the platform
  * There's a built-in constant representing this which you can access with `Number.MAX_VALUE`
* Lowest integer supported on the platform
  * There's a built-in constant representing this which you can access with `Number.MIN_SAFE_INTEGER`
* Lowest decimal supported on the platform
  * There's a built-in constant representing this which you can access with `Number.MIN_VALUE`
* Positive infinity
  * There's a built in constant representing this which you can access with `Number.POSITIVE_INFINITY`
* Negative infinity
  * There's a built in constant representing this which you can access with `Number.NEGATIVE_INFINITY`
* `NaN`

### Booleans

The only legal values for Booleans are `true` and `false`.

### Arrays

* Empty array
* Array with 1 element
* Array with more than one element

### Objects

* Empty object
* Object with 1 property
* Object with more than one property

### Dates

* Years, months, days, hours, and minutes
* Time periods that cross between days, months, and years
* Time periods that last less than a millisecond
* Time periods that last more than 24 hours
* December 31st, 2016 (contains a leap second)
* February 29th, 2020 (leap day)
* Second Sunday in March (Daylight Savings Time)
* First Sunday in November (Daylight Savings Time)

## Watch Out!

* You may want to check all data types with `null` and `undefined` as well, especially in untyped environments.

## Additional Resources

| Resource | Description |
| --- | --- |
| [MDN: Infinity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/POSITIVE_INFINITY) | MDN's guide to `Infinity`, which includes what different calculations with infinity should evaluate to. |
| [Wikipedia: Equivalence Partitioning](https://en.wikipedia.org/wiki/Equivalence_partitioning) | Wikipedia's article on equivalence partitioning |
