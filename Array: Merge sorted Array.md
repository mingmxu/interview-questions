## Question
 In order to win the prize for most cookies sold, my friend Alice and I are going to merge our Girl Scout Cookies orders and enter as one unit.

Each order is represented by an "order id" (an integer).

We have our lists of orders sorted numerically already, in arrays. Write a method to merge our arrays of orders into one sorted array.

For example:
```java
int[] myArray = new int[]{3, 4, 6, 10, 11, 15};
int[] alicesArray = new int[]{1, 5, 8, 12, 14, 19};

System.out.println(Arrays.toString(mergeArrays(myArray, alicesArray)));
// prints [1, 3, 4, 5, 6, 8, 10, 11, 12, 14, 15, 19]
```


## Solution 1: two-pointer as inputs are sorted

```java
    public static int[] mergeArrays(int[] myArray, int[] alicesArray) {

        // combine the sorted arrays into one large sorted array
        int[] merged = new int[myArray.length + alicesArray.length];
        for(int i=0, j=0, idx=0; i<myArray.length || j<alicesArray.length;idx++){
            if(get(myArray,i) <= get(alicesArray,j) ){
                merged[idx]=get(myArray, i);
                i++;
            }else{
                merged[idx]=get(alicesArray,j);
                j++;
            }
        }

        return merged;
    }
    
    private static int get(int[] array, int idx){
        if(idx>=array.length) return Integer.MAX_VALUE;
        else return array[idx];
    }
```
