# Lab report 3

I chose grep to research because it's the command that I've noticed has the most real-world use.

## Part 1

For part 1, I chose to use the -r option (or -d recurse) which lets grep recursively search all the files in a directory tree for a matching pattern. I found this option on the manpage.

### Example 1

In this first example, we'll replicate the skill demo task of searching for the string "Lucayans" in the folder written_2.

Command:
```bash
grep -r "Lucayans"
```
Output:
```
written_2/travel_guides/berlitz2/Bahamas-History.txt:Centuries before the arrival of Columbus, a peaceful Amerindian people who called themselves the Luccucairi had settled in the Bahamas. Originally from South America, they had traveled up through the Caribbean islands, surviving by cultivating modest crops and from what they caught from sea and shore. Nothing in the experience of these gentle people could have prepared them for the arrival of the Pinta, the Niña, and the Santa Maria at San Salvador on 12 October 1492. Columbus believed that he had reached the East Indies and mistakenly called these people Indians. We know them today as the Lucayans. Columbus claimed the island and others in the Bahamas for his royal Spanish patrons, but not finding the gold and other riches he was seeking, he stayed for only two weeks before sailing towards Cuba.
written_2/travel_guides/berlitz2/Bahamas-History.txt:The Spaniards never bothered to settle in the Bahamas, but the number of shipwrecks attest that their galleons frequently passed through the archipelago en route to and from the Caribbean, Florida, Bermuda, and their home ports. On Eleuthera the explorers dug a fresh-water well — at a spot now known as “Spanish Wells” — which was used to replenish the supplies of water on their ships before they began the long journey back to Europe with their cargoes of South American gold. As for the Lucayans, within 25 years all of them, perhaps some 30,000 people, were removed from the Bahamas to work — and die — in Spanish gold mines and on farms and pearl fisheries on Hispaniola (Haiti), Cuba, and elsewhere in the Caribbean.
```


### Example 2

Maybe I want to count the number of lines which mention Bahamas, possibly to see how much the Bahamas are represented in all the data. 

Command:
```bash
grep -d recurse "Bahamas" | wc -l
```
Output:
```
grep: .git/index: binary file matches
86
```

Here we can see an unfortunate consequence of the -r option: it includes stuff in .git. We can resolve this with the command line option `--exclude-dir=.git` (seen in part 4). 

## Part 2

The output for the first example got a little long, so for part 2, I chose to use the -o option which makes grep print only the parts of the file (or input) that match the pattern. I combine this with the -n option which prints the line number of a match, so I know where to look in the file. What's notable is this can be used with wc to count the number of times a pattern occurs in a given input or file. I found this option on the manpage.

### Example 1

Maybe I want to travel around the Bahamas, and I'm interested in gold, so I want to find all the files in travel_guides folder which mention gold in association with the Bahamas. But, I know the output might be large, so I'll use the command line options to shorten it.

Command:
```bash
grep "gold" written_2/travel_guides/*/*Bahamas* -o -n
```
Output:
```
written_2/travel_guides/berlitz2/Bahamas-History.txt:6:gold
written_2/travel_guides/berlitz2/Bahamas-History.txt:7:gold
written_2/travel_guides/berlitz2/Bahamas-History.txt:7:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:12:gold
```

### Example 2

But, you can use it for other fun things, like counting the number of occurences of a word in a file (or in our case, in all the files in written_2). `grep -r "word" | wc -l` doesn't work here because words might occur multiple times in a line; `grep -o` fixes that. Continuing the gold theme:

Command:
```bash
grep -r "gold" -o -n | wc -l
```
Output:
```
391
```

## Part 3

For part 3, I chose to use the `--color=auto` option which makes the grep inputs more colorful. I like this because in my terminal (unlike vscode or git bash), grep is not colored by default. I found this option on the manpage. Do note that for all the examples for this option, I'm going to ignore the instructions and use photos as the output instead of code blocks, as the code blocks do not render color properly. 

### Example 1

Just repeating the lucayans match, but with color (this makes the matches easier to distinguish by adding contrast):

Command:
```bash
grep -r "Lucayans" --color=auto
```

Output (after and before):

![image](https://user-images.githubusercontent.com/37094599/218294574-5fea4895-45cb-4004-aea0-87f8b44cfc8d.png)

### Example 2

I wonder what it does when you shorten the output, so let's run that:

Command:
```bash
grep "gold" written_2/travel_guides/*/*Bahamas* -o -n --color=auto
```
Output (before and after):

![image](https://user-images.githubusercontent.com/37094599/218294823-1b047ae2-6066-4fe1-bbdd-e58277cbb21e.png)

Apparently, it turns the line numbers green. Because all the different parts of the output are different colors, it does make it quite a bit easier to read. 

In the future, I've added `alias grep=grep --color=auto` to my ~/.zshrc so it does this by default.

## Part 4

For part 4, I chose to use the -E option which has grep do matches using extended regular expressions. This allows more flexibility with pattern matching. I found this option on the manpage.

### Example 1

Although my search for Bahamas gold appears to have been going well, I've made an error, which is not searching for "Gold" (capital g), instead limiting my search for lowercase. I also want to search for silver. So, now that I'm using extended regex, I can do so:

Command:
```bash
grep -E "([gG]old|[sS]ilver)" written_2/travel_guides/*/*Bahamas* -o -n --color=auto
```
Output:
```
written_2/travel_guides/berlitz2/Bahamas-History.txt:6:gold
written_2/travel_guides/berlitz2/Bahamas-History.txt:7:gold
written_2/travel_guides/berlitz2/Bahamas-History.txt:7:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:silver
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:Gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:silver
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:14:gold
written_2/travel_guides/berlitz2/Bahamas-WhatToDo.txt:21:Gold
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:12:gold
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:34:Silver
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:57:Gold
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:57:Gold
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:74:Gold
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:108:silver
```

The way the regex works is it matches either `[gG]old` or `[sS]ilver`, and the brackets just mean that it matches either g or G (likewise for `[sS]`. 

### Example 2

I'm interested in the total number of sentences contained in written_2. So, I've designed the following regex to find a sentence: `[A-Z][^.]+\.`. `[A-Z]` matches a capital letter, `[^.]+` matches one or more non period characters, and `\.` matches a period (. is a wildcard in regex). Do note that I've used the --exclude-dir=.git argument just to ensure that grep doesn't search the .git folder for sentences,

Command:
```bash
grep -E -r --exclude-dir=.git "[A-Z][^.]+\." -o -n --color=auto | wc -l
```
Output:
```
49319
```

So, it appears that there are 49319 sentences in the repository. This is probably more of an upper bound, as I did notice some false positive matching, but it's a reasonable estimate. 
