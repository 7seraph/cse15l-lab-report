# Lab 5 - Putting it All Together
---
Suppose that our directory is structure as such. Upon working on an assignment during lab section, a student encountered an issue. The student is confused why this issue/bug occurs and decides to post it on EdStem.
```
Example directory structure, file contents in parentheses

  list-example-grader/
    grading-area/
      lib/
        hamcrest-core-1.3.jar
        junit-4.13.2.jar
    |-  IsA.class
    |-  ListExamples.class
    |-  ListExamples.java
    |-  StringChecker.class
    |-  test-results.txt
    |-  TestListExamples.class
    |-  TestListExamples.java
  lib/
    hamcrest-core-1.3.jar
    junit-4.13.2.jar
  student-submission/
    |-  ListExamples.java
  |-  code
  |-  git-output.txt
  |-  grade.sh
  |-  GradeServer.java
  |-  Server.java
  |-  TestListExamples.java

```
## Post on EdStem
### Shell Syntax Error?
"I get an error at line 64 which is calculating the score with grade.sh however, it's saying that ")-" is a syntax error. I thought that it could be the spaces and so I removed the space and tried `bash grade.sh` but it still failed. Grade is also printing `/tests` when it should be a numerical value."
[screenshot of their error]

**TA Response**:
Hmm, there is a lot of variables assigned to different expressions. What are the values of each variable? Do they match appropriately? In other words, is there a way to check if each variable is assigned properly? How could we check? 

**Student Response (Updated)**: 
