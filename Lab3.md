# Lab Report 3 - Bugs and Commands

# PART 1

# **1. A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)**

```
    @Test
    public void testReversedOddElements() {
        int[] input1 = {9, 8, 7, 6, 5, 4, 3, 2, 1};
        assertArrayEquals(new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9}, ArrayExamples.reversed(input1));
    }
```

# **2. An input that doesn’t induce a failure, as a JUnit test and any associated code**

```
    @Test
    public void testReversed() {
        int[] input1 = {};
        assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1));
    }
```

# **3. The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)**

![Image](Symptom as output of running tests.png)

The symptom shows that the arrays differed at the element location zero. This means there is a mismatch between the expected and actual output.

# **4. The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)**

The before code is as follows :

```
    static int[] reversed(int[] arr) {
        int[] newArray = new int[arr.length];
        for(int i = 0; i < arr.length; i += 1) {
          arr[i] = newArray[arr.length - i - 1];
        }
        return arr;
    }
```

The fix is given below :

```
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        newArray[i] = arr[arr.length - i - 1];
      }
      return newArray;
    }
```

The reason for the bug is even though a newArray has been created with the same length as the old array arr, the assignment within the loop is incorrect. We can see that the old array is being assingmed values for the newly created array.
Hence, all the elements in the old array will be set to 0.  Also the function incorrectly returns the old array. Therefore as part of the fix, the assignments are reversed, where the new array is assigned values from the old array and the contents of the new array is being returned from the function.

# PART 2
I chose the find command. The 4 interesting command line options for the find command are:
1) -name pattern - finds the file or directories which matches the given pattern
2) -type [bcdpflsD] - finds the files of the given type where f is for a regular file and d is for a directory
4) -size n[cwbkMG] - finds the files with the given size 
5) -exec command -  executes the given command on the matched files 

# 1. If we want to find files which begin with "Chapter" with any file name extension recursively from the current directory and print the result we issue the following command.

```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -name "chapter*.*" 
./technical/911report/chapter-11.txt
./technical/911report/chapter-8.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-1.txt
```

# 2. If we want to find directories which begin with "911" recursively from the current directory and print the result we issue the following command.

```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -name "911*"
./technical/911report
```

# 3. If we want to find all the files with the name that have pre-push.sample recursively from the current directory and print the result, we issue the following command.

```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -name  "pre-push.sample" -type f
./.git/hooks/pre-push.sample
```

# 4. If we want to find all the directories recursively from the current directory and list them then we can issue the command below.
   
```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -type d 
.
./technical
./technical/911report
./technical/biomed
./technical/plos
./technical/government
./technical/government/Alcohol_Problems
./technical/government/Media
./technical/government/Gen_Account_Office
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Post_Rate_Comm
./lib
./.git
./.git/objects
./.git/objects/pack
./.git/objects/info
./.git/refs
./.git/refs/tags
./.git/refs/heads
./.git/refs/remotes
./.git/refs/remotes/origin
./.git/info
./.git/logs
./.git/logs/refs
./.git/logs/refs/heads
./.git/logs/refs/remotes
./.git/logs/refs/remotes/origin
./.git/hooks
./.git/branches
```

# 5. If we want to find all the files with size greater than 1000k, where k is in units kibibytes (units of 1024 bytes) recursively from the current directory and list them then we can issue the command below.
```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -type f -size +1000k
./.git/objects/pack/pack-f3e64844a2bd252cbb7d4b547cb60beb349fd441.pack
```

# 6. If we want to find all the directories with size greater than 10k, where k is in units kibibytes (units of 1024 bytes) recursively from the current directory and list them then we can issue the command below.
   
```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -type d -size +10k
./technical/biomed
./technical/plos
./technical/government/Media
```

# 7. If we want to find files which contain the string "Tuesday, September 11, 2001" and print the filename,the line number and the line within the file where the string appears recursively from the current directory, we -provide the command below.
   
```  
@mpooni23 ➜ /workspaces/docsearch (main) $  find . -type f -exec grep -nH "Tuesday, September 11, 2001" {} \;
./technical/911report/chapter-1.txt:6:    Tuesday, September 11, 2001, dawned temperate and nearly cloudless in the eastern United States. Millions of men and women readied themselves for work. Some made their way to the Twin Towers, the signature structures of the World Trade Center complex in New York City. Others went to Arlington, Virginia, to the Pentagon. Across the Potomac River, the United States Congress was back in session. At the other end of Pennsylvania Avenue, people began to line up for a White House tour. In Sarasota, Florida, President George W. Bush went for an early morning run.
```   

# 8. If we want to find directories with the name "origin" and do a long listing of the directory recursively from the current directory we issue the command below.

```
@mpooni23 ➜ /workspaces/docsearch (main) $ find . -name "origin" -type d -exec ls -ld {} \;
drwxrwxrwx+ 2 codespace codespace 4096 May  9 03:47 ./.git/refs/remotes/origin
drwxrwxrwx+ 2 codespace codespace 4096 May  9 03:47 ./.git/logs/refs/remotes/origin
```

# Sources:

https://unix.stackexchange.com/questions/638335/find-command-size-behavior
https://stackoverflow.com/questions/16956810/find-all-files-containing-a-specific-text-string-on-linux
https://www.geeksforgeeks.org/how-to-recursively-find-all-files-in-current-and-subfolders-based-on-wildcard-matching-in-linux/
https://www.geeksforgeeks.org/find-command-in-linux-with-examples/
