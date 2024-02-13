# Lab 3 - Bugs and Commands
---
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

## Failure-inducing Input (Test)

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
@Test
  public void testReversed2() {
    int[] input1 = {1, 2, 3};
    assertArrayEquals(new int[]{3, 2, 1}, ArrayExamples.reversed(input1));
  }
}
```
> Here, we `input1` is an `int[]` where it has `{1, 2, 3}` and when we call the `reversed()` method on `input1` then we should expect the new array as `{3, 2, 1}`.

```
%FAILED 1,testReversed2(ArrayTests)
%TRACES 
arrays first differed at element [0]; expected:<3> but was:<0>
```
This is our **symptom** after running the test. Uh oh, that means that our expected array does not match with the reversed array when we call the `reversed()` method. The test immediately fails at the iteration section of our `reversed()` method and we should check back (since the first element in the new array when reversing was `0` but we both know that it should be `3`). Let's look at the iteration more closely...

## The Bug
Ah-ha! We can see that assigning the variables `newArray` and `arr` are swapped around.
```
//segment of the reversed() method
for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
The idea of how you can think of this bug is that we should put the elements from `arr` into `newArray`.  However, `arr[i] = newArray[arr.length - i - 1]` means that we are taking the element from `newArray` into that specific index in `arr`. 
> Note, that `newArray` is new and `int`. By default when we don't assign a value to `int`, it will be `0`. That's why our actual value is `0`.

How would this look like? Well, we should create a new `int[]` array named something like `newArray` (for convention) with the same length as `arr`. Then, we can iterate through `arr` **BUT** we need to ensure that the element obtains a new index.

```

```
