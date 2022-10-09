# JavaScript Modules

Modules are a way to provide increased isolation and reusability between files. Traditionally, browser JavaScript includes multiple files by including them in `<script>` tags and put the contents of the files in the global scope. This creates situations where scripts in one file can accidentally change something in the scripts from another file.

## Export Syntax

Most of the time, a file will only have one export: A function, object, class, or value that some other module will import. Put the words `export default` in front of the thing you're exporting:

```ts
export default function someFunction(){
   //
}
```

If the file has multiple things to export, put the word `export` in front of each of them:

```ts
export const a = "1"              // Named export `a`
export function someFunction(){   // Named export `someFunction`
  //
}
export class SomeClassName {      // Named export `SomeClass`
  //
}
```

Note that you can default export expressions and declarations, but not statements.

A file can have both default and named exports.

## Import Syntax

To import a module, use the format:

```ts
import what from "./module/location/here"
```

To import the default export of a module, give it a name:

```ts
import someFunction from "./some-function"
```

Note that you're not required to use the same name for the function/class/value on the import. Additionally, the path to the module is relative to the location of the file doing the import, does not need to include `.js`, and _must_ start with `.` or `..`.

To import named exports, use braces:

```ts
import { a, someFunction, someClass } from "../modules/wherever/here"
```

## npm Modules

When an import statement starts with something other than `.` or `..`, the compiler assumes you're installing an npm module. By default, it looks for an `index.js` in a folder in `node_modules` with the name of the package:

```ts
import lodash from "lodash" // Get the default export from `/node_modules/lodash/index.js`
import { map, filter, reduce } from "lodash" // Get named exports `map`, `filter`, and `reduce` from `/node_modules/lodash/index.js`
```

## Watch Out!

* Node.js has traditionally used a different module system called CommonJS. You can tell something is using CommonJS because of the use of `require()` and `module.exports` statements. CommonJS modules are similar to ES modules in that they solves the same problem and share similar syntax. The biggest difference is that CommonJS module imports are dynamic (evaluated while the code is running) whereas ES Module imports are done statically ahead of time. Additionally, CommonJS is a library used in the Node ecosystem, whereas ES Modules are actually part of the JavaScript language.
* Importing named exports looks a lot like destructuring, but it's a different syntax doesn't work the same way. You can't export an object as a default export and use `{}` to destructure out properties.

## Additional Resources

| Resource | Description |
| --- | --- |
| [JavaScript Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) | MDN's guide to modules |
| [ES Modules: A Cartoon Deep Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/) | A mozilla blog explaining in deep detail how modules work |
| [Node: CommonJS](https://nodejs.org/docs/latest/api/modules.html) | Official documentation on CommonJS, the competing module system included with Node |
