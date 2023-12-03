Make sure these boxes are checked before submitting/approving the PR

# General
  - [ ] The code works
  - [ ] The code is easy to understand
  - [ ] Follows coding conventions
  - [ ] Names are simple and if possible short and spelt correctly
  - [ ] There are no usages of [magic numbers](http://c2.com/cgi/wiki?MagicNumber)
  - [ ] No hard coded constants that could possibly change in the future
  - [ ] There is no commented out code
  - [ ] There is no dead code (inaccessible at Runtime)
  - [ ] No code that can be replaced with library functions
  - [ ] Variables are not accidentally used with null values
  - [ ] Code is not repeated or duplicated
  - [ ] No complex/long boolean expressions
  - [ ] No negatively named boolean variables
  - [ ] Constructors do not accept null/none values
  - [ ] `null` is not returned from any method
  - [ ] Loop iteration and off by one are taken care of
  - [ ] Loops have a set length and correct termination conditions
  - [ ] Blocks of code inside loops are as small as possible
  - [ ] Performance is considered

# Architecture
  - [ ] Design patterns if used are correctly applied
  - [ ] A class should have only a single responsibility (i.e. only one potential change in the software's specification should be able to affect the specification of the class)
  - [ ] Classes, modules, functions, etc. should be open for extension, but closed for modification
  - [ ] Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program
  - [ ] Many client-specific interfaces are better than one general-purpose interface.
  - [ ] Depend upon Abstractions. Do not depend upon concretions.

# API
  - [ ] API checks for correct oauth scope / user permissions
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
  - [ ] Comments should indicate WHY rather that WHAT the code is doing
  - [ ] All methods are commented in clear language.
  - [ ] All public methods/interfaces/contracts are commented describing usage


# Security
  - [ ] All data inputs are checked (for the correct type, length/size, format, and range)
  - [ ] Invalid parameter values handled such that exceptions are not thrown
  - [ ] No sensitive information is logged or visible in a stacktrace