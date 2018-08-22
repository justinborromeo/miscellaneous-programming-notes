# Writing Unit Tests For Dummies

This article about writing unit tests is meant as a guide for the beginner software engineer. The code samples provided are written in Java but all the concepts are language-agnostic.

## What are Unit Tests?
Unit tests are short tests (<50 lines) which validate object behavior and logic. They differ from integration tests and system tests since external dependencies, such as databases, other web services, and disk I/O, are mocked (more on that later). As a result, good unit tests exclusively test logic and usually run in <5 milliseconds.

## Why Write Unit Tests?
Unit tests are the foundation of a robust test suite for three main reasons:

- They demonstrate that the logic of the code is sound and that the code works for all cases (happy path, edge cases, etc.).

- They run in a couple of milliseconds, allowing thousands of them to be run in a convenient amount of time. This is great because no developer wants to waste their time watching tests being run.

- They increase code readability…if you don’t know what a function is doing and don’t care about implementation, you can easily view expected behavior in the tests.
Ideally, the majority of a test suite consists of unit tests.


## The Three A’s of Writing Unit Tests
To write a good unit test, follow the 3 A’s: Arrange, Act, and Assert.

- Arrange: Instantiate test data and mock behavior of dependencies. 

- Act: Call the method that’s being tested. 

- Assert: Validate that the correct data is returned and/or the correct behavior occurs. This involves checking output, checking if an exception is thrown, or checking that one of the dependencies’ methods was executed the correct number of times.

## Example

What does this look like in practice? Say we have a class that retrieves some integer from a database and squares it (for the sake of brevity, imports are omitted):
```
public class DatabaseService(){
    public int getIntegerFromDatabase() throws DBException{
         //Some implementation
         //This method can throw DBException
    }
}
public class ClassToTest(){
    private static DatabaseService dbService;
    public ClassToTest(DatabaseService _dbService){
        this.dbService=_dbService;
    }
     
    public int squareInteger() throws SquarerException{
        int data = 0;
        try{
             data = dbService.getIntegerFromDatabase();
        }catch(SomeException e){
             throw new SquarerException();
        }    
        return Math.pow(data, 2); //return data^2   
    }
}
```
Tests for the squareInteger() function could look like this:
```
@Test
public void shouldSquareIntFromDB(){
    /* Arrange */
    // Mocking DatabaseService allows us to set test behaviour for
    // DatabaseService's method(s)
    mockDBService = mock(DatabaseService.class);
    int val = 4, expectedReturn = 16;
    // Set behaviour for mockDBService.getIntegerFromDatabase()
    when(mockDBService.getIntegerFromDatabase()).thenReturn(val);
    ClassToTest testClass = new ClassToTest(mockDBService);
    
    /* Act */
    try{
        int returnedVal = testClass.squareInteger();
    } catch (Exception e){
        fail(); // Fail test if any exception is thrown
    }
    /* Assert */
    assertEquals(expectedReturn, returnedVal);
    // This assertion will fail the test if the returned value isn't
    // equal to the expected value.
}
@Test
public void shouldThrowSquarerExceptionWhenDBExceptionOccurs(){
    /* Arrange */
    
    mockDBService = mock(DatabaseService.class);
    when(mockDBService.getIntegerFromDatabase()).thenThrow(new      DBException());
    ClassToTest testClass = new ClassToTest(mockDBService);
    /* Act */
    try{
        int returnedVal = testClass.squareInteger();
        /* Assert */
        fail(); // Fail test if exception is not thrown
    } catch (SquarerException e){
    
    } catch (Exception e){
        /* Assert */
       fail(); // Fail test if a non-SquarerException exception is
                // thrown
    }
}
```
There are a lot of other assertions that can be used but assertion syntax is language and framework-specific (read the docs!).

## Other Tips
Try to test the interface (the output) instead of the implementation (e.g. how many times was a function within called). Obviously, this doesn’t work for void functions.
Try to name your tests meaningfully (at the cost of brevity). Naming tests well will make it a lot easier to keep track of which cases the method being tested is failing for. Good naming strategies can be found here: https://dzone.com/articles/7-popular-unit-test-naming.
Write an individual test function for each input case. Breaking out each case into its own test function will make it easier to figure out where the test is failing. Having one big test function with all the cases will require you to run through the test with a debugger to find the point of failure.
Use dependency injection to make your code more testable since dependencies can be easily mocked. If you don’t know what dependency injection is: https://stackoverflow.com/questions/130794/what-is-dependency-injection
Use setup functions. If you find that code is being repeated in the “arrange” part of the test, see if your test framework has a setup function. Including instantiation of mocks and initialization of test data in the setup function will save you from rewriting the same code in each test.
Try to cover as many logical branches and lines of code as possible with your unit tests.
