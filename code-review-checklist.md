

Please make sure these boxes are checked before submitting or approving the PR :+1:

# General
  - [ ] The code works, is easy to understand and follows coding conventions on PSR-2
  - [ ] Names are simple and if possible short and spelt correctly
  - [ ] There are no usages of [magic numbers](http://c2.com/cgi/wiki?MagicNumber)
  - [ ] No hard-coded constants that could change in the future
  - [ ] There is no commented-out code
  - [ ] There is no dead code (inaccessible at Runtime)
  - [ ] No code that can be replaced with library functions
  - [ ] Variables are not accidentally used with null values
  - [ ] Code is not repeated or duplicated
  - [ ] No complex/long boolean expressions and No negatively named boolean variables
  - [ ] Constructors do not accept null/none values
  - [ ] `null` is not returned from any method
  - [ ] Loop iteration and off-by-one are taken care of and have a set length and correct termination conditions
  - [ ] Blocks of code inside loops are as small as possible
  - [ ] Performance is considered

# Code-Style
  - [ ] All properties and methods in camelCase
  - [ ] Constant names in UPPER_CASE
  - [ ] All class names in StandlyCase
  - [ ] Opening brace of classes or functions on a new line
  - [ ] Opening brace of if-for on the same line
  - [ ] Use code auto-formatting (PHPshorm Ctrl+Alt+L)
  - [ ] Describing the fields of the @property class
  - [ ] All variables on a new line and do not use multiple assignments ($a = $b = $c = 1)
  - [ ] Dont use long lines of code that go off the screen (Maximum 120 characters)

# Code-Flow
  - [ ] DRY (Dont repeat your code)
  - [ ] Clear variable names without $result, $array, $data, $return etc
  - [ ] Clear method names setData, getData, isData etc
  - [ ] Each method should contain the type of incoming and outgoing data
  - [ ] Use proper quotes '' and ""
  - [ ] Use properly public and private for methods and properties
  - [ ] Class structure (properties, constructor, methods)
  - [ ] Don't use nested if conditions
  - [ ] Do not put SQL queries in a loop
  - [ ] We use constants for naming constant numbers and strings
  - [ ] Controller->Service->Repo
  - [ ] All requests to Entity via Repo
  - [ ] Use conditions through ?? instead of ?:
  - [ ] Dont use root slashes in the object in the code, only when connecting through use
  - [ ] Only array formation [], and do not use the old array()

# Architecture
  - [ ] Design patterns if used are correctly applied
  - [ ] A class should have only a single responsibility 
  - [ ] Classes, modules, functions, etc. should be open for extension but closed for modification
  - [ ] Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program
  - [ ] Many client-specific interfaces are better than one general-purpose interface.
  - [ ] Depend upon Abstractions. Do not depend upon concretions.

# API
  - [ ] API checks for correct OAUTH scope/user permissions
  - [ ] APIs and other public contracts check input values and fail fast
  - [ ] Any API change should be reflected in the API documentation
  - [ ] APIs return correct status codes in responses

# Logging
  - [ ] Logging should be easily discoverable
  - [ ] Required logs are present
  - [ ] Debugging code is absent
  - [ ] No `print_r`, `var_dump` or similar calls exist
  - [ ] No stack traces are printed
  
# Documentation
  - [ ] Comments should indicate WHY rather than WHAT the code is doing
  - [ ] All methods are commented on in clear language.
  - [ ] All public methods/interfaces/contracts are commented describing usage


# Security
  - [ ] All data inputs are checked (for the correct type, length/size, format, and range)
  - [ ] Invalid parameter values handled such that exceptions are not thrown
  - [ ] No sensitive information is logged or visible in a stack trace
