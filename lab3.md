# Part 1 - Bugs
### A failure-inducing input for the buggy program as a JUnit test
```
@Test 
public void testReverseInPlace() {
    int[] input2 = {1, 2, 3};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[]{3, 2, 1}, input2);
}
```
### An input that doesn't induce a failure as a JUnit test 
```
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
}
```
### The symptom as the output of running the tests
  ![](/Screenshots/jUnit_test.png)

### The bug, as the before-and-after code change required to fix it
**before**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
**after**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```

# Part 2 - Researching Commands: ```grep```
- Online, find 4 interesting command-line options or alternate ways to use the command you chose. 
- To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. 
- There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. 
- Also consider asking ChatGPT!

- For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. 
- Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

- That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. 
- Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

- Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. 
- See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.

### grep -r

**Example 1**

Command: ```grep -r "base pair"  technical/```
Output:
```
technical//plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
technical//plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
technical//plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
technical//biomed/1471-2156-2-3.txt:          three exons. The first exon contains 279 base pairs (bp)
technical//biomed/1471-2121-3-10.txt:        both encode a 10-base pair sequence that is identical to
technical//biomed/1471-2121-3-10.txt:        the P3 sequence with an insertion of 3 base pairs at
technical//biomed/gb-2001-2-4-research0010.txt:          necessarily true because of Watson-Crick base pairing.
technical//biomed/gb-2003-4-4-r24.txt:        important considering that within a few hundred base pairs,
technical//biomed/gb-2001-2-4-research0011.txt:          sequenced to completion, yielding a 1,036 base pair (bp)
technical//biomed/1471-2229-2-3.txt:        stringency with a 300 base pair homologous 
etc.
```
Description: It is outputting every line in the directory "technical" that contains the given string "base pair." This is useful when the user wants to know the specific lines in which a certain word in a directory show up, working similarly to a Command-F function on Mac.

**Example 2**

Command: ```grep -r "base pair" technical/plos/*.txt```
Output:
```
technical/plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
technical/plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
technical/plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
```
Description: It is outputting every line in a .txt file in the directory "technical/plos" that contains the given string "base pair." This is useful when the user wants to know the specific lines in a specific type of file in which a certain word in a directory show up.

