# Lab Report 1

# cd

## No Arguments
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ cd 
[user@sahara ~]$ 
```

**Working Directory:**
```
/home/lecture1/
```

**Explanation:**

The cd command is used change the current working directory to a new directory within that directory. Since there were no arguments, the working directory returned to the home directory.

**Error?**

It isn't an error, as no error message has been returned and the code did what it was intended to do. 

## A Path to a Directory as an Argument
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$
```

**Working Directory:**
```
/home
```

**Explanation:**

Since the argument is lecture1, the working directory is changed to /home/lecture1, as displayed by the prompt and if pwd is run.

**Error?**

It isn't an error, as having a valid argument of a relative path allowed the code to enter the given directory. 

## A Path to a File as an Argument
```
[user@sahara ~]$ cd lecture1/messages/en-us.txt
bash: cd: lecture1/messages/en-us.txt: Not a directory
```

**Working Directory:**
```
/home
```

**Explanation:**

The cd command only works to change the current directory given the relative path of a directory. An error is returned as the relative path of a file, en-us.txt was given, and it is not a directory.

**Error?**

It is an error, as the error message ```lecture1/messages/en-us.txt: Not a directory``` is returned and the current directory was not changed.


# ls

## No Arguments
```
[user@sahara ~]$ ls
lecture1
```

**Working Directory:**
```
/home
```

**Explanation:**

Since there was no argument, the ls command just displayed the files in the current working directory home, which only contains lecture1.

**Error?**

It isn't an error, as the contents in the current working directory was displayed, which means it was a valid command.


## A Path to a Directory as an Argument
```
[user@sahara ~]$ ls lecture1/
Hello.class  Hello.java  messages  README
```

**Working Directory:**
```
/home
```

**Explanation:**

Since the argument was the relative directory to lecture1 folder, ls displayed the files in lecture1, which includes the 4 directory contents shown above.

**Error?**

It isn't an error, as having a valid argument of a relative path allowed the code to enter the given directory. 

## A Path to a File as an Argument
```
[user@sahara ~]$ ls lecture1/messages/en-us.txt
lecture1/messages/en-us.txt
```

**Working Directory:**
```
/home
```

**Explanation:**

The ls command works to display the contents in a directory. Since en-us.txt is a file, there is no directory content within it, so it returned the relative path of the given file, which is its own content. 

**Error?**

It is not an error, as directory content of the file was returned, which is the path of the file.

# cat

## No Arguments
```
[user@sahara ~]$ cat
hi
hi

^C
```

**Working Directory:**
```
/home
```

**Explanation:**

The cat command prints out the contents of a given file. Since there were no argument file was given, it prints out whatever is typed into the terminal, in this case, "hi". It receives input until the program is exited out of.

**Error?**

It isn't an error, as no file is given, it prints out the content of the current home directory, which is whatever was entered into the terminal.


## A Path to a Directory as an Argument
```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```

**Working Directory:**
```
/home
```

**Explanation:**

Since the cat command prints out contents of a file given as the argument, if a directory is given like above, it will not be able to concatanate and an error is returned. 

**Error?**

It is an error, because a cat command expects a relative directory to a file as the argument. Since a directory is given, an error is returned, telling the user that lecture1 is a directory and is unable to be concatanated. 


## A Path to a File as an Argument
```
[user@sahara ~]$ cat lecture1/messages/en-us.txt
Hello World!
```

**Working Directory:**
```
/home
```

**Explanation:**

Since en-us.txt is a file, and the relative directory to it is given, the contents of the file is printed. 

**Error?**

It is not an error, as the content of the file was printed, as the cat command was intended to do. 








