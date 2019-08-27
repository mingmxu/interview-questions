# Question


Write a method for doing an in-place ↴ shuffle of an array.

The shuffle must be "uniform," meaning each item in the original array must have the same probability of ending up in each spot in the final array.

Assume that you have a method getRandom(floor, ceiling) for getting a random integer that is >= floor and <= ceiling.

# Solution 
```java
    public static void shuffle(int[] array) {

        // shuffle the input in place
        for(int idx=0; idx<array.length-1; ++idx){
            //int rest = array.length-idx;
            //int replaceIdx = idx+(int)(Math.random()*rest);
            int replaceIdx = getRandom(idx+1, array.length-1);
            
            int temp=array[idx];
            array[idx]=array[replaceIdx];
            array[replaceIdx]=temp;
        }

    }
```    
