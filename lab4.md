# Step 4
### Screenshot
![](/Screenshots/step4.png)

### Keys Pressed
```
ssh<space>y2tai<shift>2ieng6.ucsd.edu<enter>
```

### Summary
I used the ```ssh``` command to login to my account in the ```ieng6``` remote server.

# Step 5
### Screenshot
![](/Screenshots/step5.png)

### Keys Pressed
```
git<space>clone<space><cmd>v<enter>
```

### Summary
I copied the ssh url from github from my forked repository. Then, I used the ```git clone``` command and pasted the ssh url to clone the repository.

# Step 6
### Screenshot
![](/Screenshots/step6.png)

### Keys Pressed
```
cd<space>l<tab><enter>bash<space>t<tab><enter>
```

### Summary
I used to ```cd``` command to change current directory to ```lab7```. For this, I typed in ```l```, then used ```<tab>``` to autocomplete the file name. Then, I ran the ```test.sh``` file using the ```bash``` command and ```<tab>``` after typing in ```t``` to autocomplete the ```test.sh``` file name.

# Step 7
### Screenshot
![](/Screenshots/step7.png)

### Keys Pressed
```
vim<space>L<tab>.<tab><Enter>/cha<Enter>jexi2<esc>:wq<enter>
```

### Summary
I first opened the ```ListExamples.java``` with the ```vim``` command. I used ```<tab>``` to autocomplete the file name after typing ```L``` in, then added the ```.``` and used ```<tab>``` again to complete the ```.java``` extension. To edit the file, I first searched for "cha" using the ```/``` built-in vim command to find the comment that indicated where we needed to edit to fix the file. Then, I used ```j``` to move one line down, reaching the actual line with code ```index1 += 1``` to be edited. After that, I used the e command to reach the end of the word of ```index1```, then x to delete the last letter, ```1```. To replace it, I typed in ```i``` to enter insert mode and typed 2, making the line of code ```index2 += 1```. Lastly, I used the ```<esc>``` key to escape insert mode, and ```:wq``` command to save changes and quit vim. 

# Step 8
### Screenshot
![](/Screenshots/step8.png)

### Keys Pressed
```
<up><up><enter>
```

### Summary
Since the ```<up>``` key gets the previous commands, and ```bash test.sh``` was two commands up, I pressed the up arrow twice to access and run it.

# Step 9
### Screenshot
![](/Screenshots/step9.png)

### Keys Pressed
```
git<space>add<space>.<enter>git<space>commit<enter>ifixederrors<esc><shift>;wq<enter>
```

### Summary
I added the changes I made using ```git add .``` command. Then, I used the ```git commit``` command to commit my changes. This takes me to vim, where it prompts me for a commit message. I typed in ```i``` to enter insert mode, then typed the message "fixed errors", and used ```<esc>``` to escape insert mode. Finally, I used the ```:wq``` command to save my changes and quit vim.
