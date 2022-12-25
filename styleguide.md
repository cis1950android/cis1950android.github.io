# **CIS1950 Kotlin Style Guide**

This is the official style guide of CIS1950-201: Android Development in Kotlin. Please stick to this guide when writing code for your homeworks and projects. Consistency is key for clean, readable code.

    Before writing code, ask yourself: will I ever be ashamed of this?

## **Naming Conventions**

### Syntax

- Classes & Interfaces &rarr; UpperCamelCase. For example: `StudentCalendar`
- Methods (functions) &rarr; lowerCamelCase. For example: `saveReminder`
- Variables &rarr; lowerCamelCase. For example: `val studentName = "Natalie"`
- Constant Variables &rarr; upper case, separated by underscores. For example: `const val CIRCLE_RADIUS = 5f`
- Acronyms &rarr; actonyms are to be treated as normal words, not written in all-caps. BAD example: `val HTTPHandler = handler()`. GOOD example: `val HttpHandler = handler()`

### Semantics

- Methods (functions) &rarr; MUST start with a verb or `onAction` syntax. BAD example: `fun nameSaved()` GOOD example: `fun saveName()`, BAD example: `fun whenNameIsSaved() `, GOOD example: `onNameSaved()`
- Variables &rarr; should be a good representative of their use. Never use one-letter names (except for loop counters).
