# Lab_report_5

## Part 1 : Debugging Scenario

### Original Post from a Student

**Subject:** Unexpected Behavior in Java Program

**Content:**
Hi everyone,

I'm facing a strange issue with my Java program. I wrote a simple script to count the number of lines in a text file using a bash script to execute the Java file. However, when I run my bash script, it doesn't produce the expected output. I've attached a screenshot of my terminal and my bash script. Any ideas on what might be going wrong?

![Screenshot of Terminal Output](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-5/1.png?raw=true)

And My bash file looks like this:

```count_lines.sh
javac LineCounter.java
java LineCounter.txt
```

**Response from TA**
Hi Andy,
Thanks for sharing the details. It seems like there might be an issue with either the file location or the compilation command. Could you please check if the `LineCounter.java` file is in the same directory as your bash script? Also, try running the following command manually and share the output:

```bash
ls -l
```
**Student's Response with New Screenshot/Terminal Output**

![Screenshot of Terminal Output](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-5/2.png?raw=true)

Thank you for the suggestion. It looks like the files are all in the same directory. However, I noticed something odd in my Java file. Here's the content of Line Counter.java:

```java
//created by User: andys
import java.io.*;

public class LineCounter {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Usage: java LineCounter <filename>");
            System.exit(1);
        }

        String filename = args[0];
        try (BufferedReader br = new BufferedReader(new FileReader(filename))) {
            int lines = 0;
            while (br.readLine() != null) {
                lines++;
            }
            System.out.println("Number of lines: " + lines);
        } catch (IOException e) {
            System.out.println("An error occurred while reading the file.");
        }
    }
}
```

**Bug Description**

The initial issue seems to be a misunderstanding of the error message. The javac command wasn't finding the `LineCounter.java` file, which caused the subsequent java command to fail as well. This error could be due to a typo in the filename or an issue with the current working directory.

**Setup for Fixing Bugs**
Since our `line counter.java` file looks like this within my system:

![Screenshot of Terminal Output](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-5/3.png?raw=true)

it names differently compare than what listed in my bash file`count_lines.sh` 

```count_lines.shDescription of What to Edit to Fix the Bug:

Ensure that LineCounter.java is correctly named and located in the same directory as count_lines.sh.
Verify the bash script has the correct file permissions and the files are in the correct directory.
javac LineCounter.java
java LineCounter.txt
```

**Description of How to Fix the Bug:**

I need to ensure that LineCounter.java is correctly named and located in the same directory as count_lines.sh.
Verify the bash script has the correct file permissions and the files are in the correct directory.

So that I have change the filename of `Line Counter.java` to `LineCounter.java`, which is the same as what I had in the `count_lines.sh`

## Part 2: Reflection
In the second half of this quarter, I learned how to effectively use debugging tools and techniques to troubleshoot issues in both Java and bash scripts. One interesting thing I discovered was the power of using integrated development environments (IDEs) for debugging, which can significantly speed up the process by providing detailed insights into runtime errors and logic issues. This hands-on experience has greatly improved my debugging skills and overall understanding of software development.

I really enjoyed CSE 15L and learned a lot about using the bash terminal and how to utilize GitHub to upload my code. I appreciated how our group collaborated in the lab work and how we helped each other figure out the commands. This collaborative environment made the learning process much more enjoyable and effective.


