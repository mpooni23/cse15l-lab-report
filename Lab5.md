# Week 9 - Putting it All Together

# PART 1

For this lab report, we are asked to describe a debugging scenario as a conversation on Piazza. It should start with an original post from a student showing a symptom and a description of a guess at some possible bug with some sense of what the failure-inducing input is. It should have a response from a TA asking a leading question or suggesting a command to try. There should be a screenshot/terminal output showing what information the student got from trying the TAs suggestion, and a clear description of what the bug is. It should involve at least a Java file and a bash script. Describing the bug should involve reading some output at the terminal, resulting from running one or more commands.

# **1.  Original Piazza Post and Response**

Original Post from Student:
Hello, I am experiencing an issue with my code. I am trying to merge two sorted lists of integers into a single list, by calling a method called **merge**. The **merge** method takes the two sorted lists as its parameters. The merge algorithm runs a while loop, running from the beginning to the lengths of the lists comparing elements in the first list with the elements in the second list. It starts the comparison starting from index 0 of the first list, with the element at index 0 of the second list. The smaller of the two elements gets added to a new combined list, and its index gets incremented. Also the index of the list from which the element was copied to the new combined list gets incremented. However, I seem to be running into a series of bugs while running the Junits. It says "array lengths differed, expected.length=4 actual.length=2;". I can't figure out how to fix them. My guess here would be something to do with the way the integers are being added to the merged list. Any advice would be helpful and appreciated! I've included the output of the junit tests below for reference. Please let me know, thank you!

```
manasapooni@Manasas-MBP lab7 % bash test.sh
JUnit version 4.13.2
.E.E
Time: 0.02
There were 2 failures:
1) testMerge1(ListExamplesTests)
array lengths differed, expected.length=4 actual.length=2; arrays first differed at element [2]; expected:<x> but was:<end of array>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:89)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:285)
        at org.junit.Assert.assertArrayEquals(Assert.java:300)
        at ListExamplesTests.testMerge1(ListExamplesTests.java:12)
        ... 9 trimmed
Caused by: java.lang.AssertionError: expected:<x> but was:<end of array>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:87)
        ... 15 more
2) testMerge2(ListExamplesTests)
array lengths differed, expected.length=6 actual.length=4; arrays first differed at element [4]; expected:<d> but was:<end of array>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:89)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:285)
        at org.junit.Assert.assertArrayEquals(Assert.java:300)
        at ListExamplesTests.testMerge2(ListExamplesTests.java:19)
        ... 9 trimmed
Caused by: java.lang.AssertionError: expected:<d> but was:<end of array>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:87)
        ... 15 more

FAILURES!!!
Tests run: 2,  Failures: 2

manasapooni@Manasas-MBP lab7 %
```
# **2. Response From TA**

Hey! Can you please send me a private post with your code listing. I can try the code on my side to figure out any issues. From the errors that you see in your junits, it seems obvious that the length of the combined array is lesser than the expected size. Let's analyze this a little bit more.

One reason this could happen, is if there is a bug in incrementing the indices of the arrays. Are you correctly incrementing the indices of the list from which an element has been promoted to the combined list? Also you might want to see if the legnths of your sorted lists are different. If not, while comparing and promoting elements to the combined array, you could see a early termination as the shorter list might run out of elements. These are the few points I might consider initially based on your error description.

From, 
Your TA

# **3. Another screenshot/terminal output showing what information the student got from trying that, and a clear description of what the bug is.**
From Student:

Hey, thank you for your suggestions. I inspected my code and I noticed that the incrementing of the indices of the arrays was happening properly. From closer inspection, it seems that while the while condition has a bug. If we are running through both the lengths of the list, then we might encounter the end of the shorter list earlier than the longer one. I was however surprised in some scenarios, where I found we were reaching the end of the long list earlier than compared to the shorter list.
In the worst case scenario, if all the elements of the first list is smaller than the second list, we would reach the end of the first list earlier when there are still elements in the second list. Similarly if the elements in the second list are smaller than the elements in the first list, we might reach the end of the second list earlier. So it is a problem, where the elements in the first list or the second list are not being copied to the combined list on an early termination of the other list. So to fix the issue, I ran a loop to copy over the remaining elements from the first list or second list into the combined array based on the early while loop termination. This solved the issue!

```
manasapooni@Manasas-MBP lab7 % bash test.sh
JUnit version 4.13.2
..
Time: 0.015

OK (2 tests)

manasapooni@Manasas-MBP lab7 %
```

# **4a. The file & directory structure needed**
```
manasapooni@Manasas-MBP lab7 % ls -lR
.:
total 28
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23 1461 Dec  3 22:50 ListExamples.class
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23 1435 Dec  3 22:50 ListExamples.java
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23 1095 Dec  3 22:50 ListExamplesTests.class
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23  747 Dec  3 18:16 ListExamplesTests.java
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23  152 Dec  3 22:50 StringChecker.class
drwxr-s--- 2 cs15lfa23nz ieng6_cs15lfa23 4096 Dec  3 18:16 lib
-rwxr----- 1 cs15lfa23nz ieng6_cs15lfa23  169 Dec  3 18:16 test.sh

./lib:
total 428
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23  45024 Dec  3 18:16 hamcrest-core-1.3.jar
-rw-r----- 1 cs15lfa23nz ieng6_cs15lfa23 384581 Dec  3 18:16 junit-4.13.2.jar
manasapooni@Manasas-MBP lab7 %
```

# **4b. The contents of each file before fixing the bug**

ListExamples.java 

```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    return result;
  }
}
```
# **4c. Full command line (or lines) you ran to trigger the bug**

```
manasapooni@Manasas-MBP lab7 % ./test.sh
++ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar ListExamples.java ListExamplesTests.java
++ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
JUnit version 4.13.2
.E.E
Time: 0.021
There were 2 failures:
1) testMerge1(ListExamplesTests)
array lengths differed, expected.length=4 actual.length=2; arrays first differed at element [2]; expected:<x> but was:<end of array>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:89)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:285)
        at org.junit.Assert.assertArrayEquals(Assert.java:300)
        at ListExamplesTests.testMerge1(ListExamplesTests.java:12)
        ... 9 trimmed
Caused by: java.lang.AssertionError: expected:<x> but was:<end of array>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:87)
        ... 15 more
2) testMerge2(ListExamplesTests)
array lengths differed, expected.length=6 actual.length=4; arrays first differed at element [4]; expected:<d> but was:<end of array>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:89)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:285)
        at org.junit.Assert.assertArrayEquals(Assert.java:300)
        at ListExamplesTests.testMerge2(ListExamplesTests.java:19)
        ... 9 trimmed
Caused by: java.lang.AssertionError: expected:<d> but was:<end of array>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:87)
        ... 15 more

FAILURES!!!
Tests run: 2,  Failures: 2

manasapooni@Manasas-MBP lab7 %
```
# **4d. A description of what to edit to fix the bug**

```
manasapooni@Manasas-MBP lab7 % git diff ListExamples.java
diff --git a/ListExamples.java b/ListExamples.java
index 4dd46f2..7c67c21 100644
--- a/ListExamples.java
+++ b/ListExamples.java
@@ -34,8 +34,14 @@ class ListExamples {
         index2 += 1;
       }
     }
+    while(index1 < list1.size()) {
+      result.add(list1.get(index1));
+      index1 += 1;
+    }
+    while(index2 < list2.size()) {
+      result.add(list2.get(index2));
+      index2 += 1;
+    }
     return result;
   }
-
-
 }
```
# **4e. Contents of each file after fixing the bug**

```
manasapooni@Manasas-MBP lab7 % cat ListExamples.java
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }
}
```

# PART 2

I think one cool and important skill I learned in this course was how to use git. I know that git is heavily used in the real world and I learned how to add files, check-in and check-out files from the repository. I also learned how to use the git desktop. I also learned how to use the vim editor from the command line and found it to be a very interesting editor with a bunch of different features. Although, it was a bit difficult to get used to the editor at first, after practcing with vim I was able to see how fast and efficient vim was as an editor and how it allows me to stay within my terminal. The third thing I learned was ow to use the find and grep commands. They have a number of command line options which are really powerful. Finally, I learned how to create and run shell scripts. I also found it very cool learning how to run a server and it gave me insights into how programmers in the real world are able to work remotely.
