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
The `less` command has a bunch of options and there are 4 that I want to highlight.
### less -N <filename>
This command option shows line numbers in the file.
```
trank@LAPTOP-R6OGQ529 MINGW64 ~/docsearch/technical
cat 911reports/chapter-1.txt
```
This is what we get after we press enter.
```1
      2
      3
      4 "WE HAVE SOME PLANES"
      5
      6     Tuesday, September 11, 2001, dawned temperate and nearly cloudless in the eastern United States. Millions of men and women readied thems      6 elves for work. Some made their way to the Twin Towers, the signature structures of the World Trade Center complex in New York City. Others 
      6 went to Arlington, Virginia, to the Pentagon. Across the Potomac River, the United States Congress was back in session. At the other end of 
      6 Pennsylvania Avenue, people began to line up for a White House tour. In Sarasota, Florida, President George W. Bush went for an early mornin      6 g run.
      7
      8     For those heading to an airport, weather conditions could not have been better for a safe and pleasant journey. Among the travelers were      8  Mohamed Atta and Abdul Aziz al Omari, who arrived at the airport in Portland, Maine.
      9
     10 INSIDE THE FOUR FLIGHTS
     11
     12 Boarding the Flights
     13
     14     Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.    
     15
     16     When he checked in for his flight to Boston, Atta was selected by a computerized prescreening system known as CAPPS (Computer Assisted P     16 assenger Prescreening System), created to identify passengers who should be subject to special security measures. Under security rules in pl     16 ace at the time, the only consequence of Atta's selection by CAPPS was that his checked bags were held off the plane until it was confirmed 
     16 that he had boarded the aircraft. This did not hinder Atta's plans.
     17
     18     Atta and Omari arrived in Boston at 6:45. Seven minutes later, Atta apparently took a call from Marwan al Shehhi, a longtime colleague w     18 ho was at another terminal at Logan Airport. They spoke for three minutes.
     19
     20     It would be their final conversation.
     21
     22     Between 6:45 and 7:40, Atta and Omari, along with Satam al Suqami, Wail al Shehri, and Waleed al Shehri, checked in and boarded American     22  Airlines Flight 11, bound for Los Angeles. The flight was scheduled to depart at 7:45.
     23
     24     In another Logan terminal, Shehhi, joined by Fayez Banihammad, Mohand al Shehri, Ahmed al Ghamdi, and Hamza al Ghamdi, checked in for Un     24 ited Airlines Flight 175, also bound for Los Angeles. A couple of Shehhi's colleagues were obviously unused to travel; according to the Unit     24 ed ticket agent, they had trouble understanding the standard security questions, and she had to go over them slowly until they gave the rout     24 ine, reassuring answers.
```
> With `./technical` as the directory, we can display the number of lines of a specific file. Note that this is not all of the file. You can press `enter` to go "down" the file. Especially with readings and code programs, `less -N <filemame>` will help with locating the exact position of what we desire within the file. For example, we might want to know what line of the program works or what specific passage we are interested in. Additionally, it helps with not losing track of where you were reading. I know that sometimes with a lot of words on the screen, we may forget where we left off.

And we can also use it with programming files too
```
trank@LAPTOP-R6OGQ529 MINGW64 ~/docsearch
less -N Server.java
```
And this is what we will see:
```
 1 // A simple web server using Java's built-in HttpServer
      2
      3 // Examples from https://dzone.com/articles/simple-http-server-in-java were useful references
      4
      5 import java.io.IOException;
      6 import java.io.OutputStream;
      7 import java.net.InetSocketAddress;
      8 import java.net.InetAddress;
      9 import java.net.URI;
     10
     11 import com.sun.net.httpserver.HttpExchange;
     12 import com.sun.net.httpserver.HttpHandler;
     13 import com.sun.net.httpserver.HttpServer;
     14
     15 interface URLHandler {
     16     String handleRequest(URI url) throws IOException;
     17 }
     18
     19 class ServerHttpHandler implements HttpHandler {
     20     URLHandler handler;
     21     ServerHttpHandler(URLHandler handler) {
     22       this.handler = handler;
     23     }
     24     public void handle(final HttpExchange exchange) throws IOException {
     25         // form return body after being handled by program
     26         try {
     27             String ret = handler.handleRequest(exchange.getRequestURI());
     28             // form the return string and write it on the browser
     29             exchange.sendResponseHeaders(200, ret.getBytes().length);
     30             OutputStream os = exchange.getResponseBody();
     31             os.write(ret.getBytes());
     32             os.close();
     33         } catch(Exception e) {
     34             String response = e.toString();
     35             exchange.sendResponseHeaders(500, response.getBytes().length);
     36             OutputStream os = exchange.getResponseBody();
     37             os.write(response.getBytes());
     38             os.close();
     39         }
     40     }
     41 }
     42
     43 public class Server {
     44     public static void start(int port, URLHandler handler) throws IOException {
```
> If we wanted to read a file that is not `.txt`, `less` can also apply the number of lines in a `java` program. One thing to also note is that `cat` could work too! `cat -n <filename>` would also do the same as `less -N <filename>`. The only difference is that with `cat`, you are not in the "infinite loop" of the screen. 
### less -p <String> <filename>
### less -s <filename>
### less -X <filename>

