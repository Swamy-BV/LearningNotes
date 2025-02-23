# Google Test getting started

## Integrate Google Test with CMake

```cmake
cmake_minimum_required(VERSION 3.21)
project(googletest_sample LANGUAGES CXX)

# Include FetchContent module to download external content
include(FetchContent)

# Declare GoogleTest repository and tag
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest
    GIT_TAG release-1.12.1
)

# Fetch GoogleTest properties
FetchContent_MakeAvailable(googletest)

# Add a static library target for the library code
add_library(sumLibrary STATIC LibraryCode.cpp)

# Add an executable target for the main application and link it with the library
add_executable(mainApp main.cpp)
target_link_libraries(mainApp PRIVATE sumLibrary)

# Add an executable target for the test runner and link it with the library and GoogleTest
add_executable(testRunner test.cpp)
target_link_libraries(testRunner PRIVATE sumLibrary GTest::gtest_main GTest::gmock_main)

# Enable testing and add test runner
enable_testing()
add_test(NAME testRunner COMMAND testRunner)
```

```cpp
// LibraryCode.cpp
int sum(int a, int b) {
    return a + b;
}
```

```cpp
// main.cpp
#include <iostream>

int sum(int a, int b);

int main() {
    int result = sum(3, 4);
    std::cout << "The sum of 3 and 4 is: " << result << std::endl;
    return 0;
}
```

```cpp
// test.cpp
#include <gtest/gtest.h>

// Declaration of the sum function
int sum(int a, int b);

// Test case for positive input values
TEST(SumTest, HandlesPositiveInput) {
    EXPECT_EQ(sum(1, 2), 3);
    EXPECT_EQ(sum(5, 7), 12);
}

// Test case for negative input values
TEST(SumTest, HandlesNegativeInput) {
    EXPECT_EQ(sum(-1, -2), -3);
    EXPECT_EQ(sum(-5, -7), -12);
}

// Test case for mixed input values (positive and negative)
TEST(SumTest, HandlesMixedInput) {
    EXPECT_EQ(sum(-1, 2), 1);
    EXPECT_EQ(sum(5, -7), -2);

    // Assert if not equal
    ASSERT_EQ(sum(2, 4), 6);
}

// Main function to run all the tests
int main(int argc, char **argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

---
# AAA (Arrange, Act, Assert)

AAA is a common pattern used in unit testing to structure test cases. It stands for Arrange, Act, and Assert, and it helps to make tests clear and maintainable.

1. **Arrange**: Set up the initial conditions and inputs for the test.
2. **Act**: Execute the code being tested.
3. **Assert**: Verify that the outcome is as expected.

Here is an example of how to use the AAA pattern in a Google Test case:

```cpp
#include <gtest/gtest.h>

// Function to be tested
int multiply(int a, int b) {
    return a * b;
}

// Test case using AAA pattern
TEST(MultiplyTest, HandlesPositiveInput) {
    // Arrange
    int a = 3;
    int b = 4;

    // Act
    int result = multiply(a, b);

    // Assert
    EXPECT_EQ(result, 12);
}
```

In this example:
- **Arrange**: The variables `a` and `b` are initialized with values 3 and 4.
- **Act**: The `multiply` function is called with `a` and `b`.
- **Assert**: The result is checked to ensure it equals 12.

Using the AAA pattern helps to keep test cases organized and easy to understand.


---

# TEST Macro

Google Test provides a macro `TEST` to define and register a test. The syntax for the `TEST` macro is as follows:

```cpp
TEST(TestSuiteName, TestName) {
    // Test code here
}
```

- `TestSuiteName`: The name of the test suite. This groups related tests together.
- `TestName`: The name of the specific test within the test suite.

Here is an example:

```cpp
#include <gtest/gtest.h>

// Function to be tested
int divide(int a, int b) {
    if (b == 0) throw std::invalid_argument("Division by zero");
    return a / b;
}

// Test case for divide function
TEST(DivideTest, HandlesPositiveInput) {
    EXPECT_EQ(divide(10, 2), 5);
    EXPECT_EQ(divide(9, 3), 3);
}

TEST(DivideTest, HandlesDivisionByZero) {
    EXPECT_THROW(divide(10, 0), std::invalid_argument);
}
```

In this example:
- `DivideTest` is the test suite name.
- `HandlesPositiveInput` and `HandlesDivisionByZero` are the test names.

Each `TEST` macro defines a separate test case that will be run independently by the Google Test framework.

---
## Types of Assertions in Google Test

Google Test provides two types of assertions: fatal and non-fatal.

### Fatal Assertions

Fatal assertions cause the current function to return immediately. They are prefixed with `ASSERT_`. If a fatal assertion fails, the subsequent code in the same function will not be executed.

Example:
```cpp
ASSERT_EQ(1, 1);  // This will pass
ASSERT_EQ(1, 2);  // This will fail and abort the current function
```

### Non-Fatal Assertions

Non-fatal assertions allow the current function to continue running even if the assertion fails. They are prefixed with `EXPECT_`. This is useful when you want to check multiple conditions in a single test.

Example:
```cpp
EXPECT_EQ(1, 1);  // This will pass
EXPECT_EQ(1, 2);  // This will fail but the function will continue
```

### List of Assertions

#### Equality Assertions
- `ASSERT_EQ(val1, val2)` / `EXPECT_EQ(val1, val2)`
    ```cpp
    ASSERT_EQ(1, 1);  // Pass
    EXPECT_EQ(1, 2);  // Fail
    ```

- `ASSERT_NE(val1, val2)` / `EXPECT_NE(val1, val2)`
    ```cpp
    ASSERT_NE(1, 2);  // Pass
    EXPECT_NE(1, 1);  // Fail
    ```

#### Relational Assertions
- `ASSERT_LT(val1, val2)` / `EXPECT_LT(val1, val2)`
    ```cpp
    ASSERT_LT(1, 2);  // Pass
    EXPECT_LT(2, 1);  // Fail
    ```

- `ASSERT_LE(val1, val2)` / `EXPECT_LE(val1, val2)`
    ```cpp
    ASSERT_LE(1, 1);  // Pass
    EXPECT_LE(2, 1);  // Fail
    ```

- `ASSERT_GT(val1, val2)` / `EXPECT_GT(val1, val2)`
    ```cpp
    ASSERT_GT(2, 1);  // Pass
    EXPECT_GT(1, 2);  // Fail
    ```

- `ASSERT_GE(val1, val2)` / `EXPECT_GE(val1, val2)`
    ```cpp
    ASSERT_GE(2, 2);  // Pass
    EXPECT_GE(1, 2);  // Fail
    ```

#### Boolean Assertions
- `ASSERT_TRUE(condition)` / `EXPECT_TRUE(condition)`
    ```cpp
    ASSERT_TRUE(true);  // Pass
    EXPECT_TRUE(false);  // Fail
    ```

- `ASSERT_FALSE(condition)` / `EXPECT_FALSE(condition)`
    ```cpp
    ASSERT_FALSE(false);  // Pass
    EXPECT_FALSE(true);  // Fail
    ```

#### String Assertions
- `ASSERT_STREQ(str1, str2)` / `EXPECT_STREQ(str1, str2)`
    ```cpp
    ASSERT_STREQ("hello", "hello");  // Pass
    EXPECT_STREQ("hello", "world");  // Fail
    ```

- `ASSERT_STRNE(str1, str2)` / `EXPECT_STRNE(str1, str2)`
    ```cpp
    ASSERT_STRNE("hello", "world");  // Pass
    EXPECT_STRNE("hello", "hello");  // Fail
    ```

- `ASSERT_STRCASEEQ(str1, str2)` / `EXPECT_STRCASEEQ(str1, str2)`
    ```cpp
    ASSERT_STRCASEEQ("Hello", "hello");  // Pass
    EXPECT_STRCASEEQ("Hello", "world");  // Fail
    ```

- `ASSERT_STRCASENE(str1, str2)` / `EXPECT_STRCASENE(str1, str2)`
    ```cpp
    ASSERT_STRCASENE("Hello", "world");  // Pass
    EXPECT_STRCASENE("Hello", "hello");  // Fail
    ```

#### Floating-Point Assertions
- `ASSERT_FLOAT_EQ(val1, val2)` / `EXPECT_FLOAT_EQ(val1, val2)`
    ```cpp
    ASSERT_FLOAT_EQ(1.0f, 1.0f);  // Pass
    EXPECT_FLOAT_EQ(1.0f, 2.0f);  // Fail
    ```

- `ASSERT_DOUBLE_EQ(val1, val2)` / `EXPECT_DOUBLE_EQ(val1, val2)`
    ```cpp
    ASSERT_DOUBLE_EQ(1.0, 1.0);  // Pass
    EXPECT_DOUBLE_EQ(1.0, 2.0);  // Fail
    ```

- `ASSERT_NEAR(val1, val2, abs_error)` / `EXPECT_NEAR(val1, val2, abs_error)`
    ```cpp
    ASSERT_NEAR(1.0, 1.1, 0.2);  // Pass
    EXPECT_NEAR(1.0, 1.3, 0.2);  // Fail
    ```

Using the appropriate type of assertion helps to control the flow of your tests and ensures that you get meaningful feedback from your test cases.

---
## C Strings and C++ Strings in Google Test

Google Test provides specific assertions to compare C strings and C++ strings. These assertions help to handle string comparisons correctly, considering the differences between C strings (null-terminated character arrays) and C++ strings (`std::string`).

### C String Assertions

For C strings, Google Test provides the following assertions:

- `ASSERT_STREQ(str1, str2)` / `EXPECT_STREQ(str1, str2)`
    ```cpp
    ASSERT_STREQ("hello", "hello");  // Pass
    EXPECT_STREQ("hello", "world");  // Fail
    ```

- `ASSERT_STRNE(str1, str2)` / `EXPECT_STRNE(str1, str2)`
    ```cpp
    ASSERT_STRNE("hello", "world");  // Pass
    EXPECT_STRNE("hello", "hello");  // Fail
    ```

- `ASSERT_STRCASEEQ(str1, str2)` / `EXPECT_STRCASEEQ(str1, str2)`
    ```cpp
    ASSERT_STRCASEEQ("Hello", "hello");  // Pass
    EXPECT_STRCASEEQ("Hello", "world");  // Fail
    ```

- `ASSERT_STRCASENE(str1, str2)` / `EXPECT_STRCASENE(str1, str2)`
    ```cpp
    ASSERT_STRCASENE("Hello", "world");  // Pass
    EXPECT_STRCASENE("Hello", "hello");  // Fail
    ```

### C++ String Assertions

For C++ strings, you can use the standard equality and inequality assertions:

- `ASSERT_EQ(val1, val2)` / `EXPECT_EQ(val1, val2)`
    ```cpp
    std::string str1 = "hello";
    std::string str2 = "hello";
    ASSERT_EQ(str1, str2);  // Pass
    EXPECT_EQ(str1, "world");  // Fail
    ```

- `ASSERT_NE(val1, val2)` / `EXPECT_NE(val1, val2)`
    ```cpp
    std::string str1 = "hello";
    std::string str2 = "world";
    ASSERT_NE(str1, str2);  // Pass
    EXPECT_NE(str1, "hello");  // Fail
    ```

### Example

Here is an example that demonstrates the use of both C string and C++ string assertions in Google Test:

```cpp
#include <gtest/gtest.h>
#include <string>

// Function to be tested
const char* getCString() {
    return "hello";
}

std::string getCppString() {
    return "hello";
}

// Test case for C strings
TEST(StringTest, HandlesCString) {
    // C string assertions
    ASSERT_STREQ(getCString(), "hello");
    EXPECT_STRNE(getCString(), "world");
}

// Test case for C++ strings
TEST(StringTest, HandlesCppString) {
    // C++ string assertions
    ASSERT_EQ(getCppString(), std::string("hello"));
    EXPECT_NE(getCppString(), std::string("world"));
}

// Main function to run all the tests
int main(int argc, char **argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

In this example:
- `HandlesCString` uses C string assertions to compare the result of `getCString` with expected values.
- `HandlesCppString` uses C++ string assertions to compare the result of `getCppString` with expected values.

Using the appropriate assertions for C strings and C++ strings ensures that your tests are accurate and meaningful.

---
## Assertions on Exceptions

Google Test provides assertions to verify that code throws or does not throw exceptions. These assertions help ensure that your code handles exceptional conditions correctly.

### `ASSERT_THROW` and `EXPECT_THROW`

These assertions verify that a specific exception is thrown.

- `ASSERT_THROW(statement, exception_type)` / `EXPECT_THROW(statement, exception_type)`
    ```cpp
    ASSERT_THROW(throw std::runtime_error("error"), std::runtime_error);  // Pass
    EXPECT_THROW(throw std::runtime_error("error"), std::logic_error);    // Fail
    ```

### `ASSERT_ANY_THROW` and `EXPECT_ANY_THROW`

These assertions verify that any exception is thrown.

- `ASSERT_ANY_THROW(statement)` / `EXPECT_ANY_THROW(statement)`
    ```cpp
    ASSERT_ANY_THROW(throw std::runtime_error("error"));  // Pass
    EXPECT_ANY_THROW(int x = 0);                          // Fail
    ```

### `ASSERT_NO_THROW` and `EXPECT_NO_THROW`

These assertions verify that no exception is thrown.

- `ASSERT_NO_THROW(statement)` / `EXPECT_NO_THROW(statement)`
    ```cpp
    ASSERT_NO_THROW(int x = 0);                           // Pass
    EXPECT_NO_THROW(throw std::runtime_error("error"));   // Fail
    ```

### Example

Here is an example that demonstrates the use of exception assertions in Google Test:

```cpp
#include <gtest/gtest.h>
#include <stdexcept>

// Function to be tested
void mayThrow(bool shouldThrow) {
    if (shouldThrow) {
        throw std::runtime_error("error");
    }
}

// Test case for exception assertions
TEST(ExceptionTest, HandlesThrow) {
    // Verify that an exception is thrown
    ASSERT_THROW(mayThrow(true), std::runtime_error);
    EXPECT_THROW(mayThrow(true), std::runtime_error);

    // Verify that any exception is thrown
    ASSERT_ANY_THROW(mayThrow(true));
    EXPECT_ANY_THROW(mayThrow(true));

    // Verify that no exception is thrown
    ASSERT_NO_THROW(mayThrow(false));
    EXPECT_NO_THROW(mayThrow(false));
}

// Main function to run all the tests
int main(int argc, char **argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

In this example:
- `HandlesThrow` uses different exception assertions to verify the behavior of the `mayThrow` function under various conditions.

Using exception assertions helps to ensure that your code correctly handles exceptional conditions and provides meaningful feedback when exceptions are thrown or not thrown as expected.