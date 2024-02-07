# Part 1 - Bugs
- A failure-inducing input for the buggy program as a JUnit test
```
	@Test 
	public void testReverseInPlace() {
    int[] input2 = {1, 2, 3};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[]{3, 2, 1}, input2);
	}
```
- An input that doesn't induce a failure as a JUnit test 
```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
```
- The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
  ![](/Screenshots/jUnit_test.png)

- The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```

# Part 2 - Researching Commands: grep
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
