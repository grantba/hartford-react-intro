# Bad JavaScript

The following things are banned from your code:

| No! | Instead |
| --- | --- |
| `var` | `let` if it's reassigned, `const` otherwise |
| `document.getElementById()`, `document.getElementsByTagName()`, `document.getElementsByClassName()` | `document.querySelector`, `document.querySelectorAll` |
| String concatenation | Template literals |
| Prgrmmr abbrevs., such as `obj`, `str`, `bool`, `fn`, `arr` | Full words that describe what something is for, not what it is |
