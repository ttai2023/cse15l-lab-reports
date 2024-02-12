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

### grep -A 

**Example 1**

Command: ```grep -A 2 "base pair" technical/plos/*.txt```
Output:
```
technical/plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
technical/plos/journal.pbio.0020190.txt-        chromosome that stimulate the action of proteins that bring about recombination (Eggleston
technical/plos/journal.pbio.0020190.txt-        and West 1997). Similarly, the immunoglobulin genes of mammals have recombination signal
--
technical/plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
technical/plos/journal.pbio.0020190.txt-        difficult to measure), in which recombination events tend to be concentrated. Often they
technical/plos/journal.pbio.0020190.txt-        are flanked by “coldspots,” regions of lower than average frequency of recombination
--
technical/plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
technical/plos/journal.pbio.0020223.txt-        effective molarity by several orders of magnitude, inducing a chemical reaction. Because
technical/plos/journal.pbio.0020223.txt-        reactions do not take place between reactants linked to mismatched (noncomplementary) DNA,
```
Description: It is outputting every line in the ".txt" files in the technical/plos/ directory that contains the given string "base pair" and the two lines after it. This is useful when the user wants to know the context in which a certain word in a file is used.

**Example 2**

Command: ```grep -A 3 "law" technical/government/Alcohol_Problems/*.txt```
Output:
```
technical/government/Alcohol_Problems/Session3-PDF.txt:rather than force or law enforcement should mark the interventions.
technical/government/Alcohol_Problems/Session3-PDF.txt-If there is a legal aspect to the case, it should be separated from
technical/government/Alcohol_Problems/Session3-PDF.txt-the clinical intervention as much as possible. Multiple, feasible
technical/government/Alcohol_Problems/Session3-PDF.txt-referral options that vary in intensity and scope should be
--
technical/government/Alcohol_Problems/Session3-PDF.txt:dissected, revealing flaws and problems. If we continue to do that,
technical/government/Alcohol_Problems/Session3-PDF.txt-we will never make any changes in services. He recommended a
technical/government/Alcohol_Problems/Session3-PDF.txt-balance between the rigor of research and the application process
technical/government/Alcohol_Problems/Session3-PDF.txt-that needs to happen.
--
technical/government/Alcohol_Problems/Session4-PDF.txt:(UPPL), a model law drafted by the National Association of
technical/government/Alcohol_Problems/Session4-PDF.txt-Insurance Commissioners (NAIC) in 1947, provides insurers with this
technical/government/Alcohol_Problems/Session4-PDF.txt-right. The NAIC is an organization of insurance regulators from the
technical/government/Alcohol_Problems/Session4-PDF.txt-50 states, the District of Columbia, and the 4 U.S. territories. It
--
etc.
```
It is outputting every line in the ".txt" files in the technical/government/Alcohol_Problems/ directory that contains the given string "law" and the three lines before it. This is useful when the user wants to find out not only which files contain a certain word but the context in which they are used.

### grep --colour=[when] 

**Example 1**

Command: ```grep --colour=always "police" chapter-13.5.txt```
Output:
```
                recorded calls to the Port Authority police desk from people in the towers on
                from police that morning.
                special approval by senior U.S. government officials. On September 13, Tampa police
                the airport so they could get on a plane to Lexington. Tampa police arranged for two
                Saudi nationals debarked from the plane and were met by local police. Their private
                security guards were paid, and the police then escorted the three Saudi passengers
                to Lexington by a local police officer in Lexington who did not have firsthand
                White House to kill the president. The man was shot by police and then killed
            8. For Pakistan's unpoliced areas, see Tasneem Noorani interview (Oct. 27, 2003).
```
Description: It is outputting every line in the "chapter-13.5.txt" file in the technical/911report/ directory that contains the given string "police," with every "police" being highlighted in red. This is useful when the user wants to know the context in which a certain word in a file is used.

**Example 2**

Command: ```grep -A 3 "law" technical/government/Alcohol_Problems/*.txt```
Output:
```
technical/government/Alcohol_Problems/Session3-PDF.txt:rather than force or law enforcement should mark the interventions.
technical/government/Alcohol_Problems/Session3-PDF.txt-If there is a legal aspect to the case, it should be separated from
technical/government/Alcohol_Problems/Session3-PDF.txt-the clinical intervention as much as possible. Multiple, feasible
technical/government/Alcohol_Problems/Session3-PDF.txt-referral options that vary in intensity and scope should be
--
technical/government/Alcohol_Problems/Session3-PDF.txt:dissected, revealing flaws and problems. If we continue to do that,
technical/government/Alcohol_Problems/Session3-PDF.txt-we will never make any changes in services. He recommended a
technical/government/Alcohol_Problems/Session3-PDF.txt-balance between the rigor of research and the application process
technical/government/Alcohol_Problems/Session3-PDF.txt-that needs to happen.
--
technical/government/Alcohol_Problems/Session4-PDF.txt:(UPPL), a model law drafted by the National Association of
technical/government/Alcohol_Problems/Session4-PDF.txt-Insurance Commissioners (NAIC) in 1947, provides insurers with this
technical/government/Alcohol_Problems/Session4-PDF.txt-right. The NAIC is an organization of insurance regulators from the
technical/government/Alcohol_Problems/Session4-PDF.txt-50 states, the District of Columbia, and the 4 U.S. territories. It
--
etc.
```
It is outputting every line in the ".txt" files in the technical/government/Alcohol_Problems/ directory that contains the given string "law" and the three lines before it. This is useful when the user wants to find out not only which files contain a certain word but the context in which they are used.




