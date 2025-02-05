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
