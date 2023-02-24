# Lab Report 4

## Step 1 and 2

Because I'm using a GitHub ssh deploy key instead of normal GitHub ssh (so ucsd doesn't get access to my whole github account), I don't remake and redeploy the repository. Instead, I just reset and push the github repository with this command:

```bash
git reset --hard f750e527ef14e6adef241b93245a828a2cdc04a9 $$ git push -f && cd .. && rm -rf lab7
```

## Step 3
Can't really screenshot this, just starting a timer.
## Step 4
![image](https://user-images.githubusercontent.com/37094599/221055258-66825675-6f7a-43b6-b8da-ebebe5398ecf.png)

Keyboard:

`<up><enter>`

My ssh command `kitty +kitten ssh cs15lwi23aje@ieng6.ucsd.edu` was up 1 in my zsh history.

## Step 5
![image](https://user-images.githubusercontent.com/37094599/221055612-fe991502-99eb-4adb-80e6-b9a47243ca58.png)

Keyboard:

`<ctrl>r,g8<enter>`

My github username Otisdog8 ends with g8 so this was a good way to quickly seek to the github clone command in the search history (`git clone git@github.com:otisdog8/lab7.git`)

## Step 6
![image](https://user-images.githubusercontent.com/37094599/221055976-ab83f4eb-a549-45aa-99f6-9507a28a2e36.png)

  
Keyboard:
  
`cd l<tab>,<ctrl>r,javac<enter>,<ctrl>r,java<space><enter>`

lab7 is the only folder that starts with l, so I can use tab to complete. I only use one javac command, so searching for javac in the search history returns the correct command: `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java`. I put a space after java so it doesn't match the previous javac command: `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests`.

## Step 7
![image](https://user-images.githubusercontent.com/37094599/221062774-82d7483b-790c-4053-a7f8-b6c673bde075.png)

Keyboard:

`<ctrl>r,nv<enter>,/x1<enter>Nlr2:wq<enter>`

I use nv to find the nvim command from my search history (`nvim ListExamples.java`). I use /x1 to search for the end of index1, N to go to the last search match, l to move the cursor one unit right, r2 to replace the 1 with a 2, and :wq to exit neovim.

## Step 8
![image](https://user-images.githubusercontent.com/37094599/221062966-4c616ad5-60f7-4f5a-9c5b-d73dca5878dd.png)


Keyboard:

`<ctrl>r,javac<enter>,<ctrl>r,java<space>-<enter>`

I used javac to find the compile command in the search history, and use java - to find the java command in the search history (- prevents the search from matching the end of the neovim command). 

## Step 9
![image](https://user-images.githubusercontent.com/37094599/221063071-e585e96c-b1e7-4422-a701-6449ac9514da.png)

Keyboard:

`<ctrl>r,add<enter>,<ctrl>r,comm<enter>,<ctrl>r,push<enter>`

I use add to find my git add command in the search history: `git add ListExamples.java`. I use my comm to match the commit command in the search history: `git commit -m t` , and I use push to match `git push` . 
