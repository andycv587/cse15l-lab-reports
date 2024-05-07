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