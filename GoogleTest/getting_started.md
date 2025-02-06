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
- `ASSERT_NE(val1, val2)` / `EXPECT_NE(val1, val2)`

#### Relational Assertions
- `ASSERT_LT(val1, val2)` / `EXPECT_LT(val1, val2)`
- `ASSERT_LE(val1, val2)` / `EXPECT_LE(val1, val2)`
- `ASSERT_GT(val1, val2)` / `EXPECT_GT(val1, val2)`
- `ASSERT_GE(val1, val2)` / `EXPECT_GE(val1, val2)`

#### Boolean Assertions
- `ASSERT_TRUE(condition)` / `EXPECT_TRUE(condition)`
- `ASSERT_FALSE(condition)` / `EXPECT_FALSE(condition)`

#### String Assertions
- `ASSERT_STREQ(str1, str2)` / `EXPECT_STREQ(str1, str2)`
- `ASSERT_STRNE(str1, str2)` / `EXPECT_STRNE(str1, str2)`
- `ASSERT_STRCASEEQ(str1, str2)` / `EXPECT_STRCASEEQ(str1, str2)`
- `ASSERT_STRCASENE(str1, str2)` / `EXPECT_STRCASENE(str1, str2)`

#### Floating-Point Assertions
- `ASSERT_FLOAT_EQ(val1, val2)` / `EXPECT_FLOAT_EQ(val1, val2)`
- `ASSERT_DOUBLE_EQ(val1, val2)` / `EXPECT_DOUBLE_EQ(val1, val2)`
- `ASSERT_NEAR(val1, val2, abs_error)` / `EXPECT_NEAR(val1, val2, abs_error)`

Using the appropriate type of assertion helps to control the flow of your tests and ensures that you get meaningful feedback from your test cases.
