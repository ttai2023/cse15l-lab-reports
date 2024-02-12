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
The array is essentially just getting reflected as the values stored at the first half of the array is not being saved. The code change I made is to save the value at the first position found, then set the first position to the reflected value, and the reflected position to the saved value. I also just iterated through half the array so it would get reversed correctly. 


# Part 2 - Researching Commands: ```grep```

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

### grep -B

**Example 1**

Command: ```grep -B 2 "base pair" technical/plos/*.txt```
Output:
```
technical/plos/journal.pbio.0020190.txt-        So where does recombination (Box 1) fit in? Is recombination something that happens to
technical/plos/journal.pbio.0020190.txt-        DNA generally? Or does it happen to particular sequences? Bacteria have their chi (χ)
technical/plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
--
technical/plos/journal.pbio.0020190.txt-        chromosomes have local recombination hotspots where crossing over is much more likely to
technical/plos/journal.pbio.0020190.txt-        occur than in other places on the chromosome. Recombination hotspots are local regions of
technical/plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
--
technical/plos/journal.pbio.0020223.txt-        templates approximately 20–50 nucleotides in length are combined in very dilute solutions
technical/plos/journal.pbio.0020223.txt-        with reagents that are covalently linked to complementary DNA oligonucleotides. Upon
technical/plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
```
Description: It is outputting every line in the ".txt" files in the technical/plos/ directory that contains the given string "base pair" and the two lines after it. This is useful when the user wants to know what comes after a certain word in a file.

**Example 2**

Command: ```grep -B 3 "law"```
Output:
```
technical/government/Alcohol_Problems/Session3-PDF.txt-situations created by the injuries and the noisy and often chaotic
technical/government/Alcohol_Problems/Session3-PDF.txt-nature of emergency settings. Communication rather than
technical/government/Alcohol_Problems/Session3-PDF.txt-confrontation, concern rather than condemnation, and facilitation
technical/government/Alcohol_Problems/Session3-PDF.txt:rather than force or law enforcement should mark the interventions.
--
technical/government/Alcohol_Problems/Session3-PDF.txt-must be careful when evaluating social science and psycho-social
technical/government/Alcohol_Problems/Session3-PDF.txt-interventions. However, we are so sophisticated psychometrically
technical/government/Alcohol_Problems/Session3-PDF.txt-and methodologically that virtually every piece of research can be
technical/government/Alcohol_Problems/Session3-PDF.txt:dissected, revealing flaws and problems. If we continue to do that,
--
technical/government/Alcohol_Problems/Session4-PDF.txt-the potential denial of reimbursement for medical services provided
technical/government/Alcohol_Problems/Session4-PDF.txt-to patients if they have a positive blood alcohol or drug screen.
technical/government/Alcohol_Problems/Session4-PDF.txt-The Uniform Individual Accident and Sickness Policy Provision Law
technical/government/Alcohol_Problems/Session4-PDF.txt:(UPPL), a model law drafted by the National Association of
--
etc.
```
It is outputting every line in the ".txt" files in the technical/government/Alcohol_Problems/ directory that contains the given string "law" and the three lines after it. This is useful when the user wants to find the context following where certain words are used.

### grep -m

**Example 1** 

Command: ```grep -m 10 "police" technical/911report/chapter-9.txt```
Output: 
```
local public servants, especially the first responders: fire, police, emergency
            Most Port Authority police commands used ultra-high-frequency radios. Although all
            The 40,000-officer NYPD was headed by a police commissioner, whose duties were not
            The 11,000-member FDNY was headed by a fire commissioner who, unlike the police
                Authority police desk in 5 WTC, to be activated by members of the Port Authority
                police when the FDNY units responding to the WTC complex so requested. However, in
            Civilians who called the Port Authority police desk located at 5 WTC were advised to
            Several South Tower occupants called the Port Authority police desk in 5 WTC. Some
                working on upper floors. Chiefs also spoke with Port Authority police personnel and
                Authority police officer to evacuate the South Tower, because in their judgment the
```
It is outputting the first 10 lines it found in the file ```technical/911report/chapter-9.txt``` that has the word "police." This is useful if the user wants to see where a certain word is being used within a file but doesn't want that many outputs. 

**Example 2**

Command: ```grep -m 5 "law" technical/government/Alcohol_Problems/Session4-PDF.txt```
Output:
```
(UPPL), a model law drafted by the National Association of
The model law states, "The insurer shall not be liable for any
adopted the law, and four others have adopted it with provisional
law has not been to decrease insurance claims, but to discourage
are model laws and guidelines. Model legislation forms a uniform
```
It is outputting the first 10 lines it found in the file ```technical/government/Alcohol_Problems/Session4-PDF.txt``` that has the word "law." This is useful if the user wants only a certain number of lines that contains the corresponding input from a file. 
