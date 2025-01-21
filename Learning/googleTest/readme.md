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

## Assertions: Statements that check whether a condition is true.

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



Ver os 3 A (arrange act assert)

## Interesting stuff

