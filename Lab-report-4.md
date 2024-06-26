# Lab Report 4 - Vim (Week 7)

## Step 4: Log into ieng6
- **Keys Pressed:** `ssh<space>username@ieng6.ucsd.edu<enter>`
- **Summary:** This command logs us into the ieng6 server using SSH. Replace `username` with our school username.

![Screenshot of logging into ieng6](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-4/0.png?raw=true)

## Step 5: Clone the lab7 repository (using the SSH URL)
- **Keys Pressed:** `git<space>clone<space>https://github.com/ucsd-cse15l-s24/lab7:username/lab7.git<enter>`
- **Summary:** This command clones our lab 7 repository Replace `username` with our GitHub username.

![Screenshot of cloning repository](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-4/1.png?raw=true)

## Step 6: Run the tests, demonstrating that they fail
- **Keys Pressed:** `cd<space>lab7<enter>`, `javac<space>-cp<space>.:<space>lib/hamcrest-core-1.3.jar:<space>lib/junit-4.13.2.jar<space>*.java<enter>`, `java<space>-cp<space>.:<space>lib/hamcrest-core-1.3.jar:<space>lib/junit-4.13.2.jar<space>org.junit.runner.JUnitCore<space>ListExamplesTests<enter>`
- **Summary:** 
  1. `cd lab7` changes the directory to the cloned repository.
  2. `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` compiles the Java files.
  3. `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` runs the JUnit tests, showing the initial failing tests.

![Screenshot of running tests](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-4/3.png?raw=true)

## Step 7: Edit the code file to fix the failing test
- **Keys Pressed:** 
  - `vim<space>ListExamples.java<enter>`
  - `/index1<enter>`
  - `cwtemp<esc>`
  - `:%s/index1/index2/g<enter>`
  - `:%s/index2/index1/g<enter>`
  - `:%s/temp/index2/g<enter>`
  - `:wq<enter>`
- **Summary:** 
  1. `vim ListExamples.java` opens the file in vim.
  2. `/index1` searches for `index1`.
  3. `cwtemp<esc>` changes the first occurrence of `index1` to `temp`.
  4. `:%s/index1/index2/g<enter>` replaces all `index1` with `index2`.
  5. `:%s/index2/index1/g<enter>` replaces all `index2` with `index1`.
  6. `:%s/temp/index2/g<enter>` replaces all `temp` with `index2`.
  7. `<esc>:wq<enter>` saves and quits vim.

![Screenshot of editing the code](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-4/4.png?raw=true)


## Step 8: Run the tests, demonstrating that they now succeed
- **Keys Pressed:** `<up><up><up><up><enter>`, `<up><up><up><up><enter>`
- **Summary:** 
  1. `<up><up><up><up><enter>` accesses and reruns the `javac` command from the history to compile the files again.
  2. `<up><up><up><up><enter>` accesses and reruns the `java` command from the history to run the tests again, showing that they now succeed.

![Screenshot of running tests again](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-4/5.png?raw=true)

## Step 9: Commit and push the resulting change to your Github account
- **Keys Pressed:** `git<space>add<space>ListExamples.java<enter>`, `git<space>commit<space>-m<space>"Fixed<space>index<space>issue"<enter>`, `git<space>push<space>origin<space>main<enter>`
- **Summary:** 
  1. `git add ListExamples.java` stages the modified file for commit.
  2. `git commit -m "Fixed index issue"` commits the changes with a message.
  3. `git push origin main` pushes the changes to your GitHub repository.

![Screenshot of committing and pushing changes](https://github.com/andycv587/cse15l-lab-reports/blob/main/lab-report-4/6.png?raw=true)
