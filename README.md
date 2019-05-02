# fast-rock-paper-scissors
Plays rock paper scissors against itself really quick. Old and full of spelling errors from my highschool self.

```
Here is how this code runs:
-1 A random number is generated by the Xorshift RNG (wikipedia here: https://en.wikipedia.org/wiki/Xorshift)
- That number is handled in its binary form.
- That number is a 64 bit integer. Meaing it is made of 64 1s and 0s
-2 We take the last four bits of the number (0000, 0001, 0010, 0011 ... 1111)
- Those bits are converted to a base 10 number (ranging from 0 -> 15)
- An array that stores the frequencies of those numbers is incremented at the index of the base 10 number
- The number is shifted four bits to the right (1010 0101 -> 1010)
- The process is repeated 16 times
- At that point the 64 bit number is now 0 bits
-3 All of the above is repeated for 10 seconds.
Before we discuss how scores are calculated:
-4 Consider Rock Paper and Scissors to be numbers:
- 0 == Rock
- 1 == Paper
- 2 == Scissors
-5 Consider the base 2 versions of the indexes of our array.
- index 0 -> 0000
- index 1 -> 0001
- index 2 -> 0010
- ...
- index 15 -> 1111
-6 Break up the base 2 versions into two smaller segments.
- index 0 -> 00 00
- index 1 -> 00 01
- index 2 -> 00 10
- ...
- index 15 -> 11 11
-7 The numerical versions of those are...
- index 0 -> 0 0
- index 1 -> 0 1
- index 2 -> 0 2
- ...
- index 15 -> 3 3
-8 Ignore the indexes that have a three in the broken up base 2 version.
-9 Replace the numbers with Rock Paper Scissors per our earlier convention.
- index 0 -> Rock Rock
- index 1 -> Rock Paper
- index 2 -> Rock Scissors
- ...
- index 15 -> NULL NULL
-10 Those look like games...
- index 0 -> Rock Rock -> Tie
- index 1 -> Rock Paper -> Player 2 Wins
- index 2 -> Rock Scissors -> Player 1 Wins
- ...
- index 15 -> NULL NULL -> Not important
If we accept that the numbers that are generated are random,
we can use the frequency of a given index to assign a player a win or count a tie.
Here is a sampling of the table:
0 | 00 00 | Tie
1 | 00 01 | Player 2
2 | 00 10 | Player 1
3 | 00 11 | NULL
4 | 01 00 | Player 1
...
14| 11 01 | NULL
15| 11 11 | NULL
By these conventions:
-The sum of the frequencies of the indexes that give player 1 a win is the his/her score.
-The sum of the frequencies of the indexes that give player 2 a win is the his/her score.
-The sum of the player's scores and the indexes that return a tie is the total games played.
```
