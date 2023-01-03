# **CIS1950 Kotlin Style Guide**

The official style guide of CIS1950-201: Android Development in Kotlin. Please stick to this guide when writing code for your homeworks and projects. Consistency is key for a clean, readable code.

    Before writing code, ask yourself: will I ever be ashamed of this at any point in time?

## **Naming Conventions**

### Syntax

- Classes & Interfaces &rarr; UpperCamelCase. For example: `StudentCalendar()`
- Methods (functions) &rarr; lowerCamelCase. For example: `saveReminder()`
- Variables &rarr; lowerCamelCase. For example: `val studentName = "Natalie"`
- Constant Variables &rarr; uppercase, separated by underscores. For example: `const val BALL_RADIUS = 5f`
- Acronyms &rarr; acronyms are to be treated as regualr words, i.e. not written in all-caps.

  ```kotlin
  // BAD
  val HTTPHandler = handler()

  // GOOD
  val HttpHandler = handler()
  ```

- View ID &rarr; lowercase, separated by underscores. The name ends with the view tag (`button, text, edit_text`, etc) when possible
  ```xml
  <Button>
  android:id="@+id/submit_button"
  ...
  </Button>
  ```

### Semantics

- Methods (functions) &rarr; MUST start with a verb or `onAction` syntax.

  ```kotlin

   // Example:
   // 1. a function that does something after the name is saved
   // 2. a function saves student name into database

  // BAD
  fun studentName() {} // 1.
  fun whenNameIsSaved() {} // 2.

  // GOOD
  fun saveStudentName() {} // 1.
  fun onNameSaved() {} // 2.
  ```

- Variables &rarr; should be a good representative of their use. Never use one-letter names (except for loop counters).

  ```kotlin
  // BAD
  val x = 5
  classMember.examScore = x

  // GOOD
  val score = 5
  classMember.examScore = score
  ```

### Declarations

- Visibility Modifiers
  - All variables and fields not used outside the scope of their encompassing class MUST be declared with the `private` modifier.
  - The `public` modifier is assumed for variables with no modifiers and thus should not be used explicitly. Example:
    ```kotlin
    // BAD EXAMPLE
    public val myPublicNumber = 5
    private val myPrivateNumber = 3
    // GOOD EXAMPLE
    val myPublicNumber = 5
    private val myPrivateNumber = 3
    ```

### Readability

- Line Length &rarr; lines are at most **100** characters long
- Vertical Spacing &rarr; there MUST be **exactly one blank line** between methods for clarity

### Function Documentation

- All functions MUST have a documentation block that includes:
  - A _brief_ description of functionality
  - `@return` block tag specifying the return value
- Follow this example for reference

  ```kotlin
  /**
  *
  * delete students with a grade less than 60% from the list
  * @return number of students deleted
  */
  fun deleteBelowSixty(): Int {

  }
  ```

### Comments

    Clear ambiguity, avoid repetition

### Curly Braces

- All curly braces start on the same line as preceding code
- `else` statements start on the same line as preceding curly brace

```kotlin
// BAD
fun delete()
{
    if (isDeleted)
    {
        // ...
    }
    else
    {
        // ...
    }
}

// GOOD
fun delete() {
    if (isDeleted) {
        // ...
    } else {
        // ...
    }
}
```

### Semicolons

- Just don't use them. Ever.

### Getters & Setters

- In Kotlin, direct access to fields is preferred over using getters & setters, so they will be avoided.

### When Statements

- Separate cases by commas if they fall within the same action
- Must be exhaustive. So either:
  - include all possible values of the conditioned variable
  - include an `else` branch

```kotlin
//Assume all possible values for `input` are 1, 2, 3, and 4
// BAD
when(input) {
    1 -> executeForOneOrTwo()
    2 -> executeForOneOrTwo()
    3 -> executeForThree()
}

// GOOD
when(input) {
    1, 2 -> executeForOneOrTwo()
    3 -> executeForThree()
    4 -> println("case 4")
}

// GOOD
when(input) {
    1, 2 -> executeForOneOrTwo()
    3 -> executeForThree()
    else -> println("case 4")
}
```

### `val` vs. `var`

- Only use `var` if you know the variable will change
- Rule of thumb: declare everything as `val`, switch to `var` if you needed to change it later

### Nullable Types

- It is preferred to declare variables and funciton return types as nullable `?` where a `null` value can take place
- Use `!!` as a last resort _if and only if_ you are 100% sure the variable will be defined beforehand (e.g. a view that WILL be initialized in `onCreate`)

```kotlin
/**
* Kotlin style guide for CIS1950-201 Spring 2023 at the University of Pennsylvania. Permission for use in future semesters is hereby granted.
*
* @author Ali Krema (c)
*
*/
```
