# Unit Testing Reference Guide

A quick reference for understanding unit testing concepts and JUnit.

---

## What Is Unit Testing?

A **unit test** verifies that a small, isolated piece of code (a "unit") works correctly. Typically, a unit is a single function or method.

### Why Unit Testing Matters

| Benefit | Description |
|---------|-------------|
| **Catch bugs early** | Find problems before they reach production |
| **Enable refactoring** | Change code confidently knowing tests will catch breaks |
| **Document behavior** | Tests show how code is supposed to work |
| **Improve design** | Hard-to-test code is often poorly designed |

### The Testing Pyramid

```
        /\
       /  \      E2E Tests (few, slow, expensive)
      /----\
     /      \    Integration Tests (some)
    /--------\
   /          \  Unit Tests (many, fast, cheap)
  --------------
```

Most tests should be unit tests — they're fast, reliable, and pinpoint problems.

---

## Anatomy of a Unit Test

Every unit test follows the **Arrange-Act-Assert** pattern:

```java
@Test
void testAddition() {
    // Arrange: Set up the test data
    Calculator calc = new Calculator();

    // Act: Call the method being tested
    int result = calc.add(2, 3);

    // Assert: Verify the result
    assertEquals(5, result);
}
```

| Phase | Purpose |
|-------|---------|
| **Arrange** | Set up objects, inputs, and preconditions |
| **Act** | Call the method or function being tested |
| **Assert** | Check that the result matches expectations |

---

## Types of Test Cases

### Positive Tests (Happy Path)

Test that the code works with valid, expected inputs:

```java
@Test
void testDivide_validInputs() {
    assertEquals(5, calculator.divide(10, 2));
}
```

### Negative Tests (Error Cases)

Test that the code handles invalid inputs correctly:

```java
@Test
void testDivide_byZero_throwsException() {
    assertThrows(ArithmeticException.class, () -> {
        calculator.divide(10, 0);
    });
}
```

### Edge Cases (Boundary Conditions)

Test at the boundaries of valid input:

```java
@Test
void testIsEmpty_emptyString() {
    assertTrue(StringUtils.isEmpty(""));
}

@Test
void testIsEmpty_nullString() {
    assertTrue(StringUtils.isEmpty(null));
}

@Test
void testIsEmpty_whitespaceOnly() {
    assertTrue(StringUtils.isEmpty("   "));
}
```

---

## JUnit 5 Basics

**JUnit** is the standard testing framework for Java. JUnit 5 is the current version.

### Test Class Structure

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    private Calculator calculator;

    @BeforeEach
    void setUp() {
        calculator = new Calculator();
    }

    @Test
    void testAdd() {
        assertEquals(5, calculator.add(2, 3));
    }

    @Test
    void testSubtract() {
        assertEquals(1, calculator.subtract(3, 2));
    }
}
```

### Key Annotations

| Annotation | Purpose |
|------------|---------|
| `@Test` | Marks a method as a test case |
| `@BeforeEach` | Runs before each test (set up) |
| `@AfterEach` | Runs after each test (clean up) |
| `@BeforeAll` | Runs once before all tests (static) |
| `@AfterAll` | Runs once after all tests (static) |
| `@Disabled` | Skips a test |
| `@DisplayName` | Custom name for test in reports |

---

## Assertions

Assertions verify that actual results match expected results.

### Common Assertions

| Assertion | Purpose | Example |
|-----------|---------|---------|
| `assertEquals(expected, actual)` | Check equality | `assertEquals(5, result)` |
| `assertNotEquals(a, b)` | Check inequality | `assertNotEquals(0, result)` |
| `assertTrue(condition)` | Check condition is true | `assertTrue(list.isEmpty())` |
| `assertFalse(condition)` | Check condition is false | `assertFalse(user.isAdmin())` |
| `assertNull(object)` | Check for null | `assertNull(result)` |
| `assertNotNull(object)` | Check not null | `assertNotNull(user)` |
| `assertThrows(type, executable)` | Check exception thrown | See below |

### Testing Exceptions

```java
@Test
void testInvalidInput_throwsException() {
    IllegalArgumentException exception = assertThrows(
        IllegalArgumentException.class,
        () -> validator.validate(null)
    );

    // Optionally check the message
    assertEquals("Input cannot be null", exception.getMessage());
}
```

### Assertion Messages

Add a message to clarify failures:

```java
assertEquals(expected, actual, "Sum should be 5 when adding 2 and 3");
```

---

## Test Naming Conventions

Good test names describe what is being tested and the expected outcome:

```java
// Pattern: methodName_scenario_expectedResult

@Test
void add_twoPositiveNumbers_returnsSum() { }

@Test
void add_negativeAndPositive_returnsCorrectSum() { }

@Test
void divide_byZero_throwsArithmeticException() { }

@Test
void isEmpty_nullString_returnsTrue() { }
```

---

## Code Coverage

**Code coverage** measures what percentage of your code is executed by tests.

| Coverage Type | What It Measures |
|---------------|------------------|
| **Line coverage** | Percentage of lines executed |
| **Branch coverage** | Percentage of if/else branches taken |
| **Method coverage** | Percentage of methods called |

### Coverage Goals

- **80%+ line coverage** is a common target
- 100% coverage doesn't guarantee bug-free code
- Focus on testing important logic, not just hitting numbers

---

## Test-Driven Development (TDD)

TDD is a practice where you write tests *before* writing code:

1. **Red**: Write a failing test
2. **Green**: Write minimal code to pass the test
3. **Refactor**: Improve the code while keeping tests green

### TDD Benefits

- Forces you to think about requirements first
- Results in testable, modular code
- Tests serve as documentation
- Reduces debugging time

---

## Best Practices

### Do

- Test one thing per test method
- Use descriptive test names
- Keep tests independent (no shared state)
- Test edge cases and error conditions
- Run tests frequently

### Don't

- Test private methods directly
- Write tests that depend on each other
- Test framework/library code
- Ignore failing tests
- Write tests that are harder to read than the code

---

## Example: Complete Test Class

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

@DisplayName("StringUtils Tests")
class StringUtilsTest {

    @Test
    @DisplayName("reverse returns reversed string")
    void reverse_normalString_returnsReversed() {
        assertEquals("olleh", StringUtils.reverse("hello"));
    }

    @Test
    @DisplayName("reverse handles empty string")
    void reverse_emptyString_returnsEmpty() {
        assertEquals("", StringUtils.reverse(""));
    }

    @Test
    @DisplayName("reverse throws on null input")
    void reverse_nullString_throwsException() {
        assertThrows(NullPointerException.class, () -> {
            StringUtils.reverse(null);
        });
    }

    @Test
    @DisplayName("isPalindrome returns true for palindrome")
    void isPalindrome_palindrome_returnsTrue() {
        assertTrue(StringUtils.isPalindrome("racecar"));
    }

    @Test
    @DisplayName("isPalindrome returns false for non-palindrome")
    void isPalindrome_notPalindrome_returnsFalse() {
        assertFalse(StringUtils.isPalindrome("hello"));
    }
}
```

---

## Running Tests

### Command Line (Gradle)

```bash
# Run all tests
./gradlew test

# Run specific test class
./gradlew test --tests CalculatorTest

# Run with verbose output
./gradlew test --info
```

### In GitHub Actions

Tests run automatically when you push:

```yaml
- name: Run tests
  run: ./gradlew test
```

---

## Quick Reference

```java
// Basic test structure
@Test
void methodName_scenario_expectedResult() {
    // Arrange
    // Act
    // Assert
}

// Common assertions
assertEquals(expected, actual);
assertTrue(condition);
assertFalse(condition);
assertNull(object);
assertNotNull(object);
assertThrows(ExceptionType.class, () -> { code });
```

---

## Resources

- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)
- [Assertions Reference](https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html)
- [Test-Driven Development](https://martinfowler.com/bliki/TestDrivenDevelopment.html)
