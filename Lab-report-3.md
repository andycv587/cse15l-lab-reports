# cse15l-lab-reports

## Lab Report 3

### Part 1 - Bugs

#### A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown).

```java
import static org.junit.Assert.assertArrayEquals;
import org.junit.Test;

public class ArrayTests {
    @Test
    public void testReverseInPlaceFailure() {
        int[] original = {1, 2, 3, 4};
        ArrayExamples.reverseInPlace(original);
        assertArrayEquals(new int[]{4, 3, 2, 1}, original);
    }
}
```

#### An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown).

```java
import static org.junit.Assert.assertArrayEquals;
import org.junit.Test;

public class ArrayTests {
    @Test
    public void testReverseInPlaceNoFailure() {
        int[] original = {};
        ArrayExamples.reverseInPlace(original);
        assertArrayEquals(new int[]{}, original);
    }
}

```

#### The symptom, as the output of running the two tests above (provide it as a screenshot -- one test should pass, one test should fail).

##### Test that is Not Working
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-3/BuggyNotWorking.png?raw=true)

##### Test that is working
<br>![Image](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-3/BuggyButWorking.png?raw=true)


#### The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown).
##### Buggy Code
```java
public class ArrayExamples {
    public static void reverseInPlace(int[] arr) {
        for(int i = 0; i < arr.length / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[arr.length - i];
            arr[arr.length - i] = temp;
        }
    }
}
```

##### Fixed Code
```java
public class ArrayExamples {
    public static void reverseInPlace(int[] arr) {
        for(int i = 0; i < arr.length / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[arr.length - i - 1];
            arr[arr.length - i - 1] = temp;
        }
    }
}
```

#### Briefly describe (2-3 sentences) why the fix addresses the issue.

In the original code, it incorrectly accesses `arr[arr.length - i]`, which would cause exception out of bounds when `i` is `0`. In order to fix this, we can subtract an additional `1` from the index, which ensures it always stay within bounds. This adjustment can target the element at the opposite end of the array segment being swapped, thus correctly reversing the array in place.


### Part 2: Researching Commands

For this task, I would choose the `grep` command, which is a powerful tool used for searching plain-text data sets for lines that match a regular expression. Here are four interesting command-line options for grep:

#### `-r` (or `--recursive`)

This option allows `grep` to search through all directories and subdirectories starting from the specified path, matching the specified pattern.

##### Example 1:

```
grep -r "function" ./technical
```

This command searches recursively for the word "function" within all files under the `./technical` directory. It's useful for finding occurrences of the term "function" in any code files, documents, or logs in the directory.


##### Example 2:

```
grep -r "^import" ./technical
```

This command recursively searches for lines that start with "import" in all files within the `./technical` directory. This is particularly useful for identifying all the import statements in programming files to understand dependencies.

#### `-i` (or `--ignore-case`)

This option makes `grep` perform case-insensitive matching, allowing it to match a pattern regardless of case.

##### Example 1:

```
grep -i "Network" ./technical/report.txt
```

This command searches for the word "network" in report.txt inside the `./technical directory`, ignoring the case of the letters. It's useful when the case of the text is unknown or varied.

##### Example 2:

```
grep -ir "error" ./technical/logs/
```
This command recursively searches for the word "error" in all files within the `./technical/logs` directory, ignoring case. This is useful for debugging, as errors can be logged in any case.

#### `-v` (or `--invert-match`)

This option inverts the matching process, returning only lines that do not match the given pattern.

##### Example 1:

```
grep -v "success" ./technical/process.log
```

This command searches `process.log` in the `./technical` directory for lines that do not contain the word "success". It's useful for quickly finding all lines that indicate failures or other statuses that are not "success".

##### Example 2:

```
grep -vr "todo" ./technical/projects/
```

This command recursively searches for lines that do not contain "todo" within the  `./technical/projects` directory. This can help identify files that are potentially completed and do not have any pending tasks marked as "todo".

#### `-l` (or `--files-with-matches`)

This option tells `grep` to only output the names of files containing the matching lines, instead of the lines themselves.

##### Example 1:

```
grep -l "configuration" ./technical/settings/
```

This command lists the files under the `./technical/settings` directory that contain the word "configuration". This is useful for quickly identifying all configuration files that might need review or updates.

##### Example 2:

```
grep -lr "deprecated" ./technical/src/
```

This command recursively lists all files in the `./technical/src` directory that contain the word "deprecated". This can be particularly useful in a software development context to identify old code that needs to be updated or replaced.