# Unit Testing Notes
> :calendar: *August 25, 2017*

*"Whenever you are tempted to type something into a print statement or a debugger expression, write it as a test instead."* - Martin Fowler

*"Test until fear leads to boredom."* - [JUnit](http://junit.org/junit4/faq.html#atests_5)

### AAA
 - **Arrange** - The initial test setup. Instantiate a class, assign variables, and/or create mocks.
 - **Act** - Invoke the behavior to be tested.
 - **Assert** - Verify that the *expected* result matches the *actual* result.

### FIRST
 - **Fast** - The faster your tests run, the more often you'll run them.
 - **Isolated** - Tests must be independent of external factors and other tests as well.
 - **Repeatable** - You should obtain the same results every time the test is run.
 - **Self-verifying** - Tests should be unambigous. Tests that prove nothing have no benefit.
 - **Timely** - Tests should be written before writing the production code.

### CORRECT
 - **Conformance** - Does the value conform to an expected format?
 - **Ordering** - Is the set of values ordered appropriately?
 - **Range** - Is the value within reasonable minimum and maximum values?
 - **Reference** - Does the code reference anything external?
 - **Existence** - Does the value exist?
 - **Cardinality** - Are there enough values?
 - **Time** - Is everything happening at the right time?
