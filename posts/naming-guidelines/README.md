# General Naming Guidelines

## Formatting

* Use the same formatting style as the language itself

## Do

* Use full dictionary words except for "id", "http", "url", and other domain-specific terms
* Less than 20 characters, fewer than 4 words
* Use precise, concrete words that could only apply to this value
* Use meaningful names
* Use rich single words instead of multiple simple words
* Use domain terms
* Prefer collective nouns to pluralization (eg "people" vs "persons")
* Respect singular vs plural
* Use opposites precisely (eg. old/new, open/close)

## Don't

* No single-letter names
* Never use more than one `_` in a row,
* Don't shadow names
* No silly names
* Don't encode the type in the name
* Use ambiguous terms like `data` and `manager`
* Don't have multiple names that are different but synonymous
* No homophones
* Have names that differ by more than 1-2 characters or by their order

## Suffixes and Prefixes

* Don't use numeric suffixes (eg. `person2`)
* Use qualifiers (minimum, maximum, average) as suffixes not prefixes
* Never use them `_` as a prefix or suffix
* No meaningless suffixes like `data`

## Booleans

* Use `is` and `has` prefixes for functions (but not variable names)
* Use positive names (eg. `hasError` instead of `hasNoError`)
* Use boolean-friendly names, also positive

## Constants

* Name constants after what they represent not their values

## OOP

* Class names should be noun-phrases that don't assume any particular state
* Methods should be verb-phrase names
  * Method prefixes:
    * Accessors should start with `get`, `set`, `is`, or `has`
    * `get`-prefixed methods shouldn't have side effects
    * `is`- and `has`-prefixed methods must return booleans
    * `set-` prefixed methods must not return values
    * `validate`-, `check`-, and `ensure`-prefixed methods should throw an error if there's a problem and otherwise return the value
    * Method names that start with transformation verbs (eg. `calculate`-, `normalize`-) should return transformed values rather than changing state
* Name local and instance boolean variables shouldn't use `is` or `has` prefixes
