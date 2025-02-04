# Question
 You are a renowned thief who has recently switched from stealing precious metals to stealing cakes because of the insane profit margins. You end up hitting the jackpot, breaking into the world's largest privately owned stock of cakes—the vault of the Queen of England.

While Queen Elizabeth has a limited number of types of cake, she has an unlimited supply of each type.

Each type of cake has a weight and a value, stored in objects of a CakeType class:

  public class CakeType {

    final int weight;
    final int value;

    public CakeType(int weight, int value) {
        this.weight = weight;
        this.value  = value;
    }
}

Java

For example:

  // weighs 7 kilograms and has a value of 160 shillings
new CakeType(7, 160);

// weighs 3 kilograms and has a value of 90 shillings
new CakeType(3, 90);

You brought a duffel bag that can hold limited weight, and you want to make off with the most valuable haul possible.

Write a method maxDuffelBagValue() that takes an array of cake type objects and a weight capacity, and returns the maximum monetary value the duffel bag can hold.

For example:

  CakeType[] cakeTypes = new CakeType[] {
    new CakeType(7, 160),
    new CakeType(3, 90),
    new CakeType(2, 15),
};

int capacity = 20;

maxDuffelBagValue(cakeTypes, capacity);
// returns 555 (6 of the middle type of cake and 1 of the last type of cake)

Weights and values may be any non-negative integer. Yes, it's weird to think about cakes that weigh nothing or duffel bags that can't hold anything. But we're not just super mastermind criminals—we're also meticulous about keeping our algorithms flexible and comprehensive. 

# Solution 1: space O(M*N)
```java
    public static long maxDuffelBagValue(CakeType[] cakeTypes, int weightCapacity) {
        for(CakeType cake : cakeTypes){
            if(cake.weight<=0 && cake.value>0){
                throw new RuntimeException();
            }
        }
        
        // calculate the maximum value that we can carry
        int[][] matrix = new int[weightCapacity+1][cakeTypes.length];
        for(int idx=1; idx<=weightCapacity; ++idx){
            int max=0;
            for(int cIdx=0; cIdx<cakeTypes.length; ++cIdx){
                if(idx>=cakeTypes[cIdx].weight){
                    matrix[idx][cIdx] = cakeTypes[cIdx].value
                        +maxOfRow(matrix, idx-cakeTypes[cIdx].weight);
                }
                
            }
        }

        return maxOfRow(matrix, weightCapacity);
    }
    
    public static int maxOfRow(int[][] matrix, int row){
        int max=0;
        for(int k : matrix[row]){
            max=Math.max(max, k);
        }
        return max;
    }
```
# Solution 2. SPACE O(N)
```java
    public static long maxDuffelBagValue(CakeType[] cakeTypes, int weightCapacity) {
        for(CakeType cake : cakeTypes){
            if(cake.weight<=0 && cake.value>0){
                throw new RuntimeException();
            }
        }
        
        // calculate the maximum value that we can carry
        int[] matrix = new int[weightCapacity+1];
        for(int idx=1; idx<=weightCapacity; ++idx){
            for(int cIdx=0; cIdx<cakeTypes.length; ++cIdx){
                if(idx>=cakeTypes[cIdx].weight){
                    matrix[idx] = Math.max(matrix[idx],
                        cakeTypes[cIdx].value
                            +matrix[idx-cakeTypes[cIdx].weight]);
                }
                
            }
        }

        return matrix[weightCapacity];
    }
```
