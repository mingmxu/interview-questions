# Question

Find a duplicate, Space Edition™.

We have an array of integers, where:

    The integers are in the range 1..n1..n1..n
    The array has a length of n+1n+1n+1

It follows that our array has at least one integer which appears at least twice. But it may have several duplicates, and each duplicate may appear more than twice.

Write a method which finds an integer that appears more than once in our array. (If there are multiple duplicates, you only need to find one of them.)

We're going to run this method on our new, super-hip MacBook Pro With Retina Display™. Thing is, the damn thing came with the RAM soldered right to the motherboard, so we can't upgrade our RAM. So we need to optimize for space!



# Solution
```java
    public static int findRepeat(int[] numbers) {

        // find a number that appears more than once
        java.util.Arrays.sort(numbers);
        int from=0;
        int to=numbers.length-1;
        while(from<=to){
            int middle=(from+to)/2;
            if( (middle>0 && numbers[middle]==numbers[middle-1])
                || (middle<numbers.length-1 && numbers[middle]==numbers[middle+1])
                ){
                    return numbers[middle];
                }
            
            if(numbers[middle]-numbers[from]<numbers[to]-numbers[middle]){
                to=middle-1;
            }else{
                from=middle+1;
            }
        }

        return 0;
    }
```
  
Below is one example of merge sort
```java
    numbers=sort(numbers, 0, numbers.length-1);

    private static int[] sort(int[] array, int from, int to){
        if(from==to){
            return new int[]{array[from]};
        }
        if(from>to){
            return new int[]{};
        }
        
        int middle=(from+to)/2;
        
        int[] left=sort(array, from, middle);
        int[] right=sort(array, middle+1, to);
        
        int[] results = new int[left.length+right.length];
        for(int i=0,j=0,idx=0; idx<results.length; ++idx){
            if(i>=left.length){
                results[idx]=right[j++];
                continue;
            }
            if(j>=right.length){
                results[idx]=left[i++];
                continue;
            }
            
            if(left[i]>right[j]){
                results[idx]=right[j++];
            }else{
                results[idx]=left[i++];
            }
        }
        
        return results;
     }
 ```
