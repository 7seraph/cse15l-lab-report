# Lab 3 - Bugs and Commands
---
## Part 1: Bugs
One of the bugs in the week 4 lab was assigning variables to create a "new" array. In `ArrayExamples.java` the implementation of the `reversed(int[] arr)` method follows: create a copy of the array `arr` -- the parameter of `reversed()` and return the same array but the elements in the reversed order. The `reversed(int[] arr)` method was already created for us.
```
public class ArrayExamples {
// Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
}
```
Nice, so we created a new array named `newArray` with the length of `arr`. Next, we iterate through and assign the elements from `arr` into the `newArray` array. Looks good so far! Let's run JUnit and ensure that our method works as intended!

### Failure-inducing Input (Test)

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testReversed2() {
    int[] input2 = new int[]{5, 6, 7, 8, 9};
    assertArrayEquals(new int[]{9, 8, 7, 6, 5}, ArrayExamples.reversed(input2)); Expected [9] but was [0]
  }

  @Test
  public void testReverseInPlaceLen3() {
    int[] input = {3, 2, 1};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{1, 2, 3}, input);
  }

  @Test
  public void testReversedLen3() {
    int[] input = {0, 1, 2};
    assertArrayEquals(new int[]{2, 1, 0}, ArrayExamples.reversed(input)); Expected [2] but was [0]
  }

  @Test
  public void testReversed3() {
    int[] input1 = {1, 2, 3};
    assertArrayEquals(new int[]{3, 2, 1}, ArrayExamples.reversed(input1)); Expected [3] but was [0]
  }
}
```
> Here, we see that there are 3 tests that fail. All of the failures had the actual value of the first element in the array as `0`. Since they all have the same symptom, we could look at one of them. Let's look at `testReversed3()`.  `input1` is an `int[]` where it has `{1, 2, 3}` and when we call the `reversed()` method on `input1` then we should expect the new array as `{3, 2, 1}`.

`testReverseInPlace()`, `testReversed()`, and `testReversedInPlaceLen3()` are 3 tests that did not induce a failure.

```
java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
...E.E.E.
Time: 0.01

There were 3 failures:
FAILURES!!!
Tests run: 6,  Failures: 3
```


This is what we see when we compile and run our tests with `java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests`. This is our **symptom** after running the test. Uh oh, that means that our expected array does not match with the reversed array when we call the `reversed()` method. The test immediately fails at the iteration section of our `reversed()` method and we should check back (since the first element in the new array when reversing was `0` but we both know that it should be `3`). Let's look at the iteration more closely...

### The Bug
Ah-ha! We can see that assigning the variables `newArray` and `arr` are swapped around. This is the bug **before**:
```
//segment of the reversed() method
for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
The idea of how you can think of this bug is that we should put the elements from `arr` into `newArray`.  However, `arr[i] = newArray[arr.length - i - 1]` means that we are taking the element from `newArray` into that specific index to `arr`. Therefore, the elements in `arr` would be all 0s.
> Note, that `newArray` is a new `int[]`. By default when we don't assign a value to `int`, it will be `0`. That's why our actual value was `0` and the test failed.

How would we fix this? Well, we should create a new `int[]` array named something like `newArray` (for convention) with the same length as `arr`. Then, we can iterate through `arr` **BUT** we need to ensure that the element obtains a new index. We want to "copy" the elements in `arr` to `newArray`, just with a reversed order. 

```
//segment of the updated reversed() method
for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
The is the bug **after**. Now the `for-loop` correctly copies all the elements from `arr` to `newArray`. We can run JUnit test again to see if that fixed the bug.
```
java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
......
Time: 0.009

OK (6 tests)
```
Woohoo! All of our tests run without any failure, ensuring that the methods did as we intended it to do. 

## Part 2: Researching Commands
