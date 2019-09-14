# Question

Your quirky boss collects rare, old coins...

They found out you're a programmer and asked you to solve something they've been wondering for a long time.

Write a method that, given:

    an amount of money
    an array of coin denominations

computes the number of ways to make the amount of money with coins of the available denominations.

Example: for amount=444 (444¢) and denominations=[1,2,3][1,2,3][1,2,3] (111¢, 222¢ and 333¢), your program would output 444—the number of ways to make 444¢ with those denominations:

    1¢, 1¢, 1¢, 1¢
    1¢, 1¢, 2¢
    1¢, 3¢
    2¢, 2¢



# Solution 1: DP
```java
    public static int changePossibilities(int amount, int[] denominations) {
        if(amount < 0) throw new RuntimeException();
        // calculate the number of ways to make change
        int[] counts = new int[amount+1];
        counts[0]=1;
        for(int d : denominations){
            for(int amt=d; amt<=amount; ++amt){
                counts[amt] += counts[amt-d];
            }
        }

        return counts[amount];
    }

```

# Solution 2: backtracking - this may out-of-time for large numbers
```java
    public static int changePossibilities(int amount, int[] denominations) {
        // calculate the number of ways to make change
        int[] numbersOfEachCoin = new int[denominations.length];
        Set<String> validCombinations = new HashSet<>();
        tryACombination(amount, denominations, numbersOfEachCoin, validCombinations);

        return validCombinations.size();
    }
    
    public static void tryACombination(int amount, int[] denominations
        , int[] numbersOfEachCoin, Set<String> validCombinations){
        if(amount < 0) return;
        if(amount==0){
            //find one
            validCombinations.add(toString(numbersOfEachCoin));
            return;
        }
        
        for(int idx=0; idx<denominations.length; ++idx){
            numbersOfEachCoin[idx]++;
            tryACombination(amount-denominations[idx], denominations
                ,numbersOfEachCoin, validCombinations);
            numbersOfEachCoin[idx]--;
        }
    }
    
    public static String toString(int[] numbersOfEachCoin){
        StringBuilder sb = new StringBuilder();
        for(int n : numbersOfEachCoin){
            sb.append(n).append(":");
        }
        return sb.toString();
    }
```
