# Question
You have a method rand5() that generates a random integer from 1 to 5. Use it to write a method rand7() that generates a random integer from 1 to 7.

rand5() returns each integer with equal probability. rand7() must also return each integer with equal probability.

# Solution
```java
    public static int rand7() {

        // implement rand7() using rand5()
        int[][] results = new int[][] {
        {1, 2, 3, 4, 5},
        {6, 7, 1, 2, 3},
        {4, 5, 6, 7, 1},
        {2, 3, 4, 5, 6},
        {7, 0, 0, 0, 0},
        };
        
        int row=rand5()-1;
        int col=rand5()-1;
        while(results[row][col]==0){
            row=rand5()-1;
            col=rand5()-1;
        }

        return results[row][col];
    }
```
