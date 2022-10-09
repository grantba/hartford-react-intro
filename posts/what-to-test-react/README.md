# What To Test: React Components

One of the most difficult things in testing is deciding what to test and what not to test. When testing React components, consider the following questions:

* **What does the component do with its props?** Statically display them? Invoke them? Use them to conditionally render things?
* **What state does the component have, and under what circumstances does it change?** These usually point toward test cases.
* **What other components does this component render, and what are their props?** What state do they have and how does it change?
* **What kinds of interactions can users have with the component?** Are there things that can be clicked on, typed in, or changed?
* **What happens when child components invoke functions?** Do the functions change state or otherwise alter what's rendered?

The answers to these questions will guide you toward the things you need to test. Some general guidelines:

## What To Test

Test the public API of the component.

### Props

* You may want separate cases for any equivalence partitions and boundaries for those props
* If a prop is optional, test what happens with and without it
* Test different combinations of props, including their partitions and boundaries
* If the component has child components, make sure they render
* Are there styles bound to props?

### State

* Don't try to test the state directly, always read and modify the state the way a user would
* Look for conditional logic
* Look for all the ways the state can be changed, including user actions and higher-order functions
* If a component has multiple pieces of state, test combinations
* Are there styles bound to state?

### User Actions

* What should happen when things are clicked, typed in, dragged, or otherwise used? How would that be observed by a user?
* Look for network calls, higher-order functions being called, or context changing

## What Not To Test

Don't test things that aren't in the public API or aren't owned by the component you're testing.

### Implementation Details

* Static content
* Internal functions, variable names, or signatures that aren't part of the component's API
* The APIs of child components that are never used independently of the parent
* The APIs of functions that are only used in this component
* Anything that isn't visible to or interactable by a user
* Internal styles that aren't bound to anything

## External Code

* Any external styles
* Third-party libraries, including React
* External web services
* File systems
* Utilities that aren't owned by the component

## Watch Out!

* If your tests break a lot as you're doing normal development, your tests are probably too coupled to the implementation. You should be able to refactor your code freely without any of your tests failing as long as the component's API and behavior stays the same.
* Conversely, if you change the API of a component or its behavior, your tests _should_ fail. If they don't, your tests aren't giving you enough confidence that your code still works.
