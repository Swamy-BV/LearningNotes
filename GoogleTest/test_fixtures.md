# Introduction to Google Test Test Fixtures

Google Test provides a powerful framework for writing and running C++ tests. One of the key features of Google Test is the ability to use test fixtures. Test fixtures allow you to reuse the same configuration of objects across multiple tests, making your tests more organized and easier to maintain.

## What is a Test Fixture?

A test fixture is a class that contains the common setup and teardown code for a group of tests. By using a test fixture, you can ensure that each test starts with a known state and that any necessary cleanup is performed after the test runs.

## Syntax

To create a test fixture in Google Test, follow these steps:

1. Define a fixture class that inherits from `::testing::Test`.
2. Override the `SetUp()` method to initialize any resources needed for the tests.
3. Override the `TearDown()` method to clean up any resources allocated in `SetUp()`.
4. Use the `TEST_F` macro to define tests that use the fixture.

Here is an example:

```cpp
#include <gtest/gtest.h>
#include <iostream>

// Define the fixture class
class MyTestFixture : public ::testing::Test {
protected:
    void SetUp() override {
        // Code here will be called immediately after the constructor (right before each test).
        value = 1;
        std::cout << "SetUp: value = " << value << std::endl;
    }

    void TearDown() override {
        // Code here will be called immediately after each test (right before the destructor).
        std::cout << "TearDown: value = " << value << std::endl;
    }

    // Class members declared here can be used by all tests in the test suite.
    int value;
};

// Use the TEST_F macro to define tests that use the fixture
TEST_F(MyTestFixture, Test1) {
    EXPECT_EQ(value, 1);
    std::cout << "Test1: value = " << value << std::endl;
    value++;
}

TEST_F(MyTestFixture, Test2) {
    EXPECT_EQ(value, 1);
    std::cout << "Test2: value = " << value << std::endl;
    value += 2;
}
```

Output:
```
SetUp: value = 1
Test1: value = 1
TearDown: value = 2
SetUp: value = 1
Test2: value = 1
TearDown: value = 3
```

In this example, `MyTestFixture` is a test fixture class that initializes an integer `value` to 1 before each test. The `TEST_F` macro is used to define two tests, `Test1` and `Test2`, which both use the fixture.

By using test fixtures, you can ensure that each test starts with a known state and that any necessary cleanup is performed after the test runs. This makes your tests more reliable and easier to maintain.

---

## Setting Up and Tearing Down a Test Suite

In addition to setting up and tearing down individual tests, Google Test also allows you to set up and tear down entire test suites. This can be useful when you need to perform expensive operations that should only be done once for a group of tests.

To set up and tear down a test suite, follow these steps:

1. Define static methods `SetUpTestSuite` and `TearDownTestSuite` in your test fixture class.
2. Implement the `SetUpTestSuite` method to perform any setup required for the entire test suite.
3. Implement the `TearDownTestSuite` method to perform any cleanup required for the entire test suite.

Here is an example:

```cpp
#include <gtest/gtest.h>
#include <iostream>

// Define the fixture class
class MyTestSuiteFixture : public ::testing::Test {
protected:
    static void SetUpTestSuite() {
        // Code here will be called once for the entire test suite before any test runs.
        shared_resource = new int(42);
        std::cout << "SetUpTestSuite: shared_resource = " << *shared_resource << std::endl;
    }

    static void TearDownTestSuite() {
        // Code here will be called once for the entire test suite after all tests have run.
        std::cout << "TearDownTestSuite: shared_resource = " << *shared_resource << std::endl;
        delete shared_resource;
        shared_resource = nullptr;
    }

    // Class members declared here can be used by all tests in the test suite.
    static int* shared_resource;
};

// Initialize static member
int* MyTestSuiteFixture::shared_resource = nullptr;

// Use the TEST_F macro to define tests that use the fixture
TEST_F(MyTestSuiteFixture, Test1) {
    EXPECT_EQ(*shared_resource, 42);
    std::cout << "Test1: shared_resource = " << *shared_resource << std::endl;
}

TEST_F(MyTestSuiteFixture, Test2) {
    EXPECT_EQ(*shared_resource, 42);
    std::cout << "Test2: shared_resource = " << *shared_resource << std::endl;
}
```

Output:
```
SetUpTestSuite: shared_resource = 42
Test1: shared_resource = 42
Test2: shared_resource = 42
TearDownTestSuite: shared_resource = 42
```

In this example, `MyTestSuiteFixture` is a test fixture class that sets up a shared resource before any tests in the suite run and cleans it up after all tests have finished. The `SetUpTestSuite` and `TearDownTestSuite` methods are used to manage the shared resource.

By using test suite setup and teardown, you can optimize your tests by performing expensive operations only once, rather than before each individual test. This can significantly reduce the overall runtime of your test suite.

---
