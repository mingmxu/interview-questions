# question

 You created a game that is more popular than Angry Birds.

Each round, players receive a score between 0 and 100, which you use to rank them from highest to lowest. So far you're using an algorithm that sorts in O(nlg⁡n)O(n\lg{n})O(nlgn) time, but players are complaining that their rankings aren't updated fast enough. You need a faster sorting algorithm.

Write a method that takes:

    an array of unsortedScores
    the highestPossibleScore in the game

and returns a sorted array of scores in less than O(nlg⁡n)O(n\lg{n})O(nlgn) time.

For example:

  int[] unsortedScores = {37, 89, 41, 65, 91, 53};
final int HIGHEST_POSSIBLE_SCORE = 100;

int[] sortedScores = sortScores(unsortedScores, HIGHEST_POSSIBLE_SCORE);
// sortedScores: [91, 89, 65, 53, 41, 37]

We’re defining nnn as the number of unsortedScores because we’re expecting the number of players to keep climbing.

And, we'll treat highestPossibleScore as a constant instead of factoring it into our big O time and space costs because the highest possible score isn’t going to change. Even if we do redesign the game a little, the scores will stay around the same order of magnitude. 

# Solution:
```java
    public static int[] sortScores(int[] unorderedScores, int highestPossibleScore) {

        // sort the scores in O(n) time
        int[] scoreArray = new int[highestPossibleScore+1];
        for(int s : unorderedScores){
            scoreArray[s]++;
        }
        
        int[] results = new int[unorderedScores.length];
        int rIdx=0;
        for(int idx=highestPossibleScore; idx>=0; --idx){
            for(int n=0; n<scoreArray[idx]; ++n){
                results[rIdx++]=idx;
            }
        }

        return results;
    }
```
