# React Hooks

Hooks must start with the word "use".

## Basic Hooks

There are three basic hooks that get used throughout most React apps:

* `const [someState, setSomeState] = useState(initialState)`
	* Stateful code
	* Variant is `const [state, dispatch] = useReducer(reducer, initialArgument)`, used if state is an object with independent subvalues
* `useEffect(() => console.log("Hi!"), [dependencyOne, dependencyTwo])`
	* Contains imperative code, possibly with effects
	* Mutations, subscriptions, timers, logging
	* Run after every render unless constrained
	* Can return a function that will clean up any lingering objects when the component unloads
	* Variant is `useLayoutEffect()`, used if you're directly manipulating the DOM
	* An empty dependency array means only run the effect once on mount
* `useContext(someContextObject)`

## Advanced Hooks

* `const memoizedFunction = useCallback(someFunction, dependencies)`
	* Gives you a consistent reference, prevents unnecessary rerenders
	* Necessary when using functions in dependency arrays
* `const expensiveResult = useMemo(functionWithExpensiveOperation, dependencies)`
* `const someRef = useRef(initialValue)`
	* Keeps its current value in its `.current` property

## Rules of Hooks

Hooks follow 2 rules:

* Only call hooks at the top level of components
* Only call hooks in components

## Custom Hook Ideas

* `useCopyToClipboard`
* `usePageBottom`
* `useWindowSize`
* `useDeviceDetect`

## Watch Out!

* Hooks must always be called in the same order, which is why you can't use them inside conditionals or loops.
