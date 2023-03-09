# Lab Report 5

For this lab, I chose to make my fast completion from lab report 4 into a bash script. Like from the past lab, I'm using this command: `git reset --hard f750e527ef14e6adef241b93245a828a2cdc04a9 && git push -f && cd .. && rm -rf lab7` to reset everything after I'm done, so I can have reproducibility (I can't go recreate the repository because I'm using github ssh deploy keys, so that ucsd doesn't have access to my whole github account). See sources at the end.

## Writing

My approach for the script was relatively simple. I chained all the commands together that I used in my lab4 (see here: https://15l.rooty.dev/lab4) with semicolons. For editing the file, I initially tried using vim to edit by passing my keystrokes (`vim +"execute 'normal! /x1\<CR>Nlr2' | x" ListExamples.java` was my best attempt), but eventually gave up and just used sed with some complicated regex to get it working: `sed -i -r -z "s/(2\)\);\n\s*index)1/\12/g" ListExamples.java`. -r is required to make the expression work, -z is required to make sed match newlines properly. What it does is match the buggy part, and replace index1 with index2 while using a capture group to ensure the other structure of the file remains intact. The other complication was making sure my backslash usage worked with all the string escaping, but I made it work in the end.

In the end, here's my full script:

![image](https://user-images.githubusercontent.com/37094599/223883077-226b6e9b-97c5-493d-850b-062068d49516.png)

As text:

```bash
#!/bin/bash

ssh cs15lwi23aje@ieng6.ucsd.edu "git clone git@github.com:otisdog8/lab7.git ; cd lab7 ; javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java ; java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests ; sed -i -r -z \"s/(2\)\);\n\s*index)1/\12/g\" ListExamples.java ; javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java ; java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests ; git add ListExamples.java ; git commit -m t ; git push"
```

I made it executable with `chmod +x task.sh`.

## Running

Here's the output of the final bash script:

![image](https://user-images.githubusercontent.com/37094599/223882404-b67de188-10d3-441a-8bd2-5ef4f180f296.png)

As a text block:

```
Cloning into 'lab7'...
JUnit version 4.13.2
..E
Time: 0.525
There was 1 failure:
1) testMerge2(ListExamplesTests)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
	at java.util.Arrays.copyOf(Arrays.java:3210)
	at java.util.Arrays.copyOf(Arrays.java:3181)
	at java.util.ArrayList.grow(ArrayList.java:267)
	at java.util.ArrayList.ensureExplicitCapacity(ArrayList.java:241)
	at java.util.ArrayList.ensureCapacityInternal(ArrayList.java:233)
	at java.util.ArrayList.add(ArrayList.java:464)
	at ListExamples.merge(ListExamples.java:42)
	at ListExamplesTests.testMerge2(ListExamplesTests.java:19)

FAILURES!!!
Tests run: 2,  Failures: 1

JUnit version 4.13.2
..
Time: 0.012

OK (2 tests)

[main e4f331d] t
 Committer: Jacob T Root <cs15lwi23aje@ieng6-202.ucsd.edu>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 1 insertion(+), 1 deletion(-)
warning: push.default is unset; its implicit value is changing in
Git 2.0 from 'matching' to 'simple'. To squelch this message
and maintain the current behavior after the default changes, use:

  git config --global push.default matching

To squelch this message and adopt the new behavior now, use:

  git config --global push.default simple

See 'git help config' and search for 'push.default' for further information.
(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
'current' instead of 'simple' if you sometimes use older versions of Git)

To git@github.com:otisdog8/lab7.git
   f750e52..e4f331d  main -> main
```

Based on the output, it clearly worked. Because I already had things like ssh keys setup, this was pretty easy.

Sources:
https://vi.stackexchange.com/questions/5989/is-it-possible-to-pipe-vim-commands-to-vim
https://unix.stackexchange.com/questions/26284/how-can-i-use-sed-to-replace-a-multi-line-string
