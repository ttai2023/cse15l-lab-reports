# Part 1: Debugging Scenario
### The original post from a student with a screenshot showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is.

**Post:**

![](/Screenshots/bash_script.png)

![](/Screenshots/command_line.png)

![](/Screenshots/compile_output.png)

![](/Screenshots/compile_error.png)

I was working on my grading script and I wanted to store the compilation output to a file, then extract only the compile errors, if there are any, to another file from the first file. I tried using the ```2>&1``` command to redirect all the output from compiling the file into the ```compile-output.txt``` file, and then used ```2>``` to redirect only the error from ```compile-output.txt``` into the ```compile-error.txt``` file. This is shown in the first screenshot. I then ran the bash script with one of the example repositories given, ```https://github.com/ucsd-cse15l-f22/list-methods-compile-error``` to test my code out. All the output was in the ```compile-output.txt``` file, but the ```compile-error.txt``` file was empty, even though there was an error. Does anyone know what the issue is?

**Description:**
A guess at the bug would be in the two lines where I redirected the outputs. I think there was a syntax error in the redirection of ```compile-error.txt``` file, as it does not seem to have the correct output.


### A response from a TA asking a leading question or suggesting a command to try

**TA Response**

Hi. I suggest that you review what the ```2>``` redirection command really does with command before it, and what ```cat``` does as well. 

### Another screenshot/terminal output showing what information the student got from trying that, and a clear description of what the bug is
![](/Screenshots/script_corrected.png)

![](/Screenshots/corrected_file.png)

**Description:**
After reviewing the ```2>``` command, I realised that it redirects the errors of the command before the redirection. In this case, it was ```cat```. Since there was no error concatenating the file, the ```compile-error.txt``` file will be empty. What I did to fix the error was ran the ```javac``` command again and redirected the errors directly using ```javac -cp $CPATH *.java 2> compile-error.txt ```. After fixing that, the```compile-error.txt``` file contained the compilation error. Thank you for your help!

# Part 2: Reflection

In the Week 7 lab, we had to time ourselves doing a series of tasks. I learnt keyboard shortcuts that I didn't know before, such as ```Ctrl-U```, ```Ctrl-A```, and ```Ctrl-W```, which really sped up my process, as I can correct my mistakes and typos really quickly instead of trying to navigate in the terminal only using arrow keys. They were really helpful, and I have started using them in my own projects when I'm working with the command-line.

