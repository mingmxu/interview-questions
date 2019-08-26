# Question:
 You have an array of integers, and for each index you want to find the product of every integer except the integer at that index.

Write a method getProductsOfAllIntsExceptAtIndex() that takes an array of integers and returns an array of the products.

For example, given:

  [1, 7, 3, 4]

your method would return:

  [84, 12, 28, 21]

by calculating:

  [7 * 3 * 4,  1 * 3 * 4,  1 * 7 * 4,  1 * 7 * 3]

Here's the catch: You can't use division in your solution! 

# Solution:
```java
    public static int[] getProductsOfAllIntsExceptAtIndex(int[] intArray) {
        // make an array of the products
        if(intArray.length <=1 ) throw new RuntimeException();
        
        int len=intArray.length;
        int[] results = new int[len];
        results[0]=intArray[0];
        //left to right
        for(int idx=1; idx<len; ++idx){
            results[idx]=intArray[idx]*results[idx-1];
        }
        
        //righ to left;
        int tempRight=1;
        for(int idx=len-1; idx>0; --idx){
            results[idx]=results[idx-1]*tempRight;
            tempRight *= intArray[idx];
        }
        results[0]=tempRight;

        return results;
    }
```
