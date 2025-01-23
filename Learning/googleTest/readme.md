---
title: "googleTest"
parent: Learning
permalink: "/learning/googleTest"
layout: default
---

# GoogleTest

## Introduction

- Test Suite: Group of one or more tests. When multiple tests in a test suite need to share common objects and subroutines, you can put them into a test fixture class.

- Test: Exercise a particular program path with specific input values and verify the results

- Test Fixture: Contain multiple tests that need to share common objects and subroutines.

## Assertions: Statements that check whether a condition is true (Assertion Reference [here](https://google.github.io/googletest/reference/assertions.html)).

- Result can be success, nonfatal or fatal failure.
- If fatal, aborts the function being tested.

Assertion are macros that can have different effects on the function:

- `ASSERT_*`: Generates fatal failures and abort the current function.
- `EXPECT_*`: Generates nonfatal failures which do not abort the current function.

To show a custom failure message, it is possible to stream it to an assertion:

	ASSERT_EQ(x.size(), y.size()) << "Vectors x and y are of unequal length";
	
	for (int i = 0; i < x.size(); ++i) {
	  EXPECT_EQ(x[i], y[i]) << "Vectors x and y differ at index " << i;
	}

For the complete list of assertions provided by GoogleTest, see the [Assertions Reference](https://google.github.io/googletest/reference/assertions.html).


## Creating a test

1. Use the `TEST()` macro to define and name a test function that does not return a value.
2. Along with valid C++ statements, use assertions to check values
3. Results are determined by assertions.
	
		TEST(TestSuiteName, TestName) {			--> Names should be valid C++ identifiers
			... test body ...											and not contain underscores (_)
		}																		--> Same TestSuiteName tests are grouped
																						(they belong to the same test suite)
   
Example:

	int Factorial(int n);  // Returns the factorial of n

	 // Tests factorial of 0.
	TEST(FactorialTest, HandlesZeroInput) {
	  EXPECT_EQ(Factorial(0), 1);
	}
	
	// Tests factorial of positive numbers.
	TEST(FactorialTest, HandlesPositiveInput) {
	  EXPECT_EQ(Factorial(1), 1);
	  EXPECT_EQ(Factorial(2), 2);
	  EXPECT_EQ(Factorial(3), 6);
	  EXPECT_EQ(Factorial(8), 40320);
	}

### Test Fixtures ([link](https://google.github.io/googletest/primer.html#same-data-multiple-tests))

A test fixture allows for multiple tests that use the same configurations to reuse that configuration code:

	#include <gtest/gtest.h>
	
	class SampleTest : public ::testing::Test {
	
	protected:					<-- protected since the members are accessed via sub-classes
	    void SetUp() override {
		std::cout << "Test up\n";		<-- I added this but standard output might not be always visible
	        // Code here will be executed immediately before each TEST_F
	    }
	    void TearDown() override {
     		std::cout << "Test down\n";		<-- I added this but standard output might not be always visible
	        // Code here will be executed immediately after each TEST_F
	    }
	    // Define your test object here, such as:
	    int testVariable = 10;
	};
	
	
	TEST_F(SampleTest, TestName) {		<-- Must be a TEST_F (_F stands for "fixture")
	    // Access your test object		    (allows access to objects and subroutines)
	    EXPECT_EQ(testVariable, 10);	    First argument must be name of fixture class
	    // Other test code...
	}

In this case, TestName is based on the SampleTest test fixture class and uses the SetUp and TearDown methods from it. Sometimes, the constructor/destructor of the test fixture should be used instead of SetUp/TearDown (see more [here](https://google.github.io/googletest/faq.html#CtorVsSetUp)).

### Running tests

After defining your tests, you can run them with `RUN_ALL_TESTS()`, which returns 0 if all the tests are successful, or 1 otherwise. Note that `RUN_ALL_TESTS()` runs all tests in your link unit–they can be from different test suites, or even different source files.

## gMock

gMock is a library or "framework" for creating mock classes for C++ that is included with googleTest. 

A mock object implements the same interface as a real object (to be used instead) AND specify at runtime how it will be used and called (which methods, arguments, how many times, etc).

There is a difference between fake objects and mock objects:
- Fake objects have "cheap" working implementations which are not suitable for production
- Mocks are pre-programmed with expectations, which form the specification for what is expected.

### Creating a Mock Class

1. Derive a class `MockTurtle` from `Turtle`
2. Take a virtual function of Turtle (gMock overrites the function from a base class with a virtual function automatically)
3. In `public:` section, write `MOCK_METHOD()`
4. Take the function signature (inputs, outputs and name of function) and paste it into the macro with commas separating the fields
   - If mocking a const method, add a forth parameter `(const)`
5. Since the virtual method is being overriding, it is suggested to add the `override` keyword: `(const, override)`
6. Do step 2 to 5 for every virtual function being mocked


		#include <gmock/gmock.h>  // Brings in gMock.
		class MockTurtle : public Turtle {														// #1 & #2
			public:																											// #3
				...
				MOCK_METHOD(void, PenUp, (), (override));									// #4 & #5
				MOCK_METHOD(void, PenDown, (), (override));
				MOCK_METHOD(void, Forward, (int distance), (override));
				MOCK_METHOD(void, Turn, (int degrees), (override));
				MOCK_METHOD(void, GoTo, (int x, int y), (override));
				MOCK_METHOD(int, GetX, (), (const, override));
				MOCK_METHOD(int, GetY, (), (const, override));
		};

### Using the mocks in tests

1. Import the gMock names from the `testing` namespace (namespaces are a good idea)
2. Create some mock objects
3. Specify expectations (how many times will it be called, what arguments, etc.)
4. Write code that uses the mocks
   - **Optionally, check results with googletest assertions (if mock is called more than expected or with wrong arguments)**
5. When a mock is destroyed, gMock will check if expectations have been satisfied

		#include "path/to/mock-turtle.h"
		#include <gmock/gmock.h>
		#include <gtest/gtest.h>
		
		using ::testing::AtLeast;                         // #1
		
		TEST(PainterTest, CanDrawSomething) {
		  MockTurtle turtle;                              // #2
		  EXPECT_CALL(turtle, PenDown())                  // #3
		      .Times(AtLeast(1));
		
		  Painter painter(&turtle);                       // #4
		
		  EXPECT_TRUE(painter.DrawCircle(0, 0, 10));      // #5
		}

## Setting Expectations

The right expectations must be set for the test to be evaluated correctly and not fail as result of unrelated changes. In gMock the `EXPECT_cALL()` is used to set an expectation on a mock method. The cardinality options can be seen [here](https://google.github.io/googletest/reference/mocking.html#EXPECT_CALL.Times):

    using ::testing::Return;
    ...
    EXPECT_CALL(turtle_object, GetX(matchers))     // Two arguments: the mock object and the method and its arguments 
        .Times(5)                                  // Method will be called 5 times (cardinality),
        .WillOnce(Return(100))                     // it will return 100 one time (the first time),
        .WillOnce(Return(150))                     // it will return 150 the second time
        .WillRepeatedly(Return(200));              // and then return 200 the remaining times.

### Another examples:

1. Specifying expected arguments:

    These can work by setting any generic comparison, as seen [here](https://google.github.io/googletest/reference/matchers.html#generic-comparison).

        // Expects the turtle to move forward by 100 units. (Equivalent to Eq(100))
        EXPECT_CALL(turtle, Forward( 100 ) );
   
        // Expects the turtle moves forward by at least 100 units.
        EXPECT_CALL(turtle, Forward( Ge(100) ) );


3. Not interested in the value of certain arguments:

    For this, the `_` can be used in place of an argument, meaning "anything goes" (Wildcard). The `_` is called a matcher and can be used inside `EXPECT_CALL()`.
        
        using ::testing::_;
        ...
        // Expects that the turtle jumps to somewhere on the x=50 line.
        EXPECT_CALL(turtle, GoTo( 50, _ ) );



# TODO: See if there is a reference to the 3 A's (Arrange Act Assert)

## Interesting stuff

