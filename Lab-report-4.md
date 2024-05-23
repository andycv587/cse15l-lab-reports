# Lab Report 4 - Vim (Week 7)

## Step 4: Log into ieng6
- **Keys Pressed:** `ssh<space>username@ieng6.ucsd.edu<enter>`
- **Summary:** This command logs you into the ieng6 server using SSH. Replace `username` with our actual username.

![Screenshot of logging into ieng6](link-to-your-screenshot-1)

## Step 5: Clone your fork of the repository from your Github account (using the SSH URL)
- **Keys Pressed:** `git<space>clone<space>git@github.com:yourusername/lab7.git<enter>`
- **Summary:** This command clones your fork of the lab 7 repository to your local machine. Replace `yourusername` with your actual GitHub username.

![Screenshot of cloning repository](link-to-your-screenshot-2)

## Step 6: Run the tests, demonstrating that they fail
- **Keys Pressed:** `cd<space>lab7<enter>`, `javac<space>-cp<space>.:<space>lib/hamcrest-core-1.3.jar:<space>lib/junit-4.13.2.jar<space>*.java<enter>`, `java<space>-cp<space>.:<space>lib/hamcrest-core-1.3.jar:<space>lib/junit-4.13.2.jar<space>org.junit.runner.JUnitCore<space>ListExamplesTests<enter>`
- **Summary:** 
  1. `cd lab7` changes the directory to the cloned repository.
  2. `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` compiles the Java files.
  3. `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` runs the JUnit tests, showing the initial failing tests.

![Screenshot of running tests](link-to-your-screenshot-3)

## Step 7: Edit the code file to fix the failing test
- **Keys Pressed:** `vim<space>ListExamples.java<enter>`, `/index1<enter>cwwindex2<esc>:wq<enter>`
- **Summary:** 
  1. `vim ListExamples.java` opens the file in vim.
  2. `/index1` searches for `index1`.
  3. `cwwindex2` changes `index1` to `index2`.
  4. `<esc>:wq<enter>` saves and quits vim.

![Screenshot of editing the code](link-to-your-screenshot-4)

## Step 8: Run the tests, demonstrating that they now succeed
- **Keys Pressed:** `<up><up><up><up><enter>`, `<up><up><up><up><enter>`
- **Summary:** 
  1. `<up><up><up><up><enter>` accesses and reruns the `javac` command from the history to compile the files again.
  2. `<up><up><up><up><enter>` accesses and reruns the `java` command from the history to run the tests again, showing that they now succeed.

![Screenshot of running tests again](link-to-your-screenshot-5)

## Step 9: Commit and push the resulting change to your Github account
- **Keys Pressed:** `git<space>add<space>ListExamples.java<enter>`, `git<space>commit<space>-m<space>"Fixed<space>index<space>issue"<enter>`, `git<space>push<space>origin<space>main<enter>`
- **Summary:** 
  1. `git add ListExamples.java` stages the modified file for commit.
  2. `git commit -m "Fixed index issue"` commits the changes with a message.
  3. `git push origin main` pushes the changes to your GitHub repository.

![Screenshot of committing and pushing changes](link-to-your-screenshot-6)
