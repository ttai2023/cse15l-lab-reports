# Part 1: Debugging Scenario
### The original post from a student with a screenshot showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is.

**Post:**

```grade.sh file```

![](/Screenshots/bash_script.png)

```command line ran```

![](/Screenshots/command_line.png)

```compile-output.txt file```

![](/Screenshots/compile_output.png)

```compile-error.txt file```

![](/Screenshots/compile_error.png)

I was working on my grading script and I wanted to store the compilation output to a file, then extract only the compile errors, if there are any, to another file from the first file. I tried using the ```2>&1``` command to redirect all the output from compiling the file into the ```compile-output.txt``` file, and then used ```2>``` to redirect only the error from ```compile-output.txt``` into the ```compile-error.txt``` file. This is shown in the first screenshot. I then ran the bash script with one of the example repositories given, ```https://github.com/ucsd-cse15l-f22/list-methods-compile-error``` to test my code out. All the output was in the ```compile-output.txt``` file, but the ```compile-error.txt``` file was empty, even though there was an error. Does anyone know what the issue is?

**Description:**
A guess at the bug would be in the two lines where I redirected the outputs. I think there was a syntax error in the redirection of ```compile-error.txt``` file, as it does not seem to have the correct output.


### A response from a TA asking a leading question or suggesting a command to try

**TA Response**

Hi. I suggest that you review what the ```2>``` redirection command really does with command before it, and what ```cat``` does as well. 

### Another screenshot/terminal output showing what information the student got from trying that, and a clear description of what the bug is

```grade.sh file after correction```

![](/Screenshots/script_corrected.png)

```compile-error.txt file after correction```

![](/Screenshots/corrected_file.png)

**Description:**
After reviewing the ```2>``` command, I realised that it redirects the errors of the command before the redirection. In this case, it was ```cat```. Since there was no error concatenating the file, the ```compile-error.txt``` file will be empty. What I did to fix the error was ran the ```javac``` command again and redirected the errors directly using ```javac -cp $CPATH *.java 2> compile-error.txt ```. After fixing that, the```compile-error.txt``` file contained the compilation error. Thank you for your help!

### All the information needed about the setup

**Files Needed:**
```grade.sh``` and ```TestListExamples.java```

**Directory Structure Needed**
![](/Screenshots/directory_structure.png)

**Contents of each file before fixing the bug**

```grade.sh```

```
CPATH='.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission 2> git-output.txt
# echo 'Finished cloning'


# Draw a picture/take notes on the directory structure that's set up after
if [[ -f student-submission/ListExamples.java ]]
then 
    cp student-submission/ListExamples.java grading-area
    cp TestListExamples.java grading-area
else 
    echo "There should be one file titled ListExamples.java in your repository, nothing else."
    exit 1
fi
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
cd grading-area

javac -cp $CPATH *.java > compile-output.txt 2>&1
cat compile-output.txt 2> compile-error.txt 

if [[ $? -ne 0 ]]
then    
    echo "Compilation error: see above."
    exit 1
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt 

if [[ $(head -n 2 junit-output.txt | tail -n 1 | grep "E") != "" ]]
then
    lastline=$(cat junit-output.txt | tail -n 2 | head -n 1)
    tests=$(echo $lastline | awk -F '[, ]' '{print $3}')
    failures=$(echo $lastline | awk -F '[, ]' '{print $6}')
    successes=$((tests-failures))
    echo "Failed tests: "
    grep ".) test" junit-output.txt
    echo "Number of tests passed: $successes / $tests"
else
    lastline=$(cat junit-output.txt | tail -n 2 | head -n 1)
    numtests=$(echo $lastline | grep -o '[0-9]*' | head -1)
    echo "All tests passed"
    echo "Number of tests passed: $numtests / $numtests"
fi
```

**The full command line (or lines) you ran to trigger the bug**

![](/Screenshots/command_line.png)

**A description of what to edit to fix the bug**

To fix the bug, you will have to edit the ```cat compile-output.txt 2> compile-error.txt``` line to ```javac -cp $CPATH *.java 2> compile-error.txt ``` so that the redirection command ```2>``` redirects the errors of the ```javac``` command instead of the ```cat``` command. Initially, since the ```cat``` command will not result in any errors, ```compile-error.txt``` would be empty. After the edit, since there is a compilation error in the file chosen, the errors will be redirected into the ```compile-error.txt``` file.


# Part 2: Reflection

In the Week 7 lab, we had to time ourselves doing a series of tasks. I learnt keyboard shortcuts that I didn't know before, such as ```Ctrl-U```, ```Ctrl-A```, and ```Ctrl-W```, which really sped up my process, as I can correct my mistakes and typos really quickly instead of trying to navigate in the terminal only using arrow keys. They were really helpful, and I have started using them in my own projects when I'm working with the command-line.

