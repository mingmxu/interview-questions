# Question

Given an array of integers, find the highest product you can get from three of the integers.

The input arrayOfInts will always have at least three integers.

# Solution 1
```Java
    public static int highestProductOf3(int[] intArray) {
        
        // calculate the highest product of three numbers
        Arrays.sort(intArray);
        int len=intArray.length;
        return Math.max(
            intArray[len-1]*intArray[len-2]*intArray[len-3]
            , intArray[len-1]*intArray[0]*intArray[1]
            );
    }
```

# Solution 2
Since we use only several numbers, it's not neccessary to sort the entire array.
```java
    public static int highestProductOf3(int[] intArray) {
        //System.out.println(intArray);
        // calculate the highest product of three numbers
        PriorityQueue<Integer> largest = new PriorityQueue<>();
        PriorityQueue<Integer> smallest = new PriorityQueue<>((i,j)->j-i);

        for(int v : intArray){
            largest.add(v);
            smallest.add(v);
            if(largest.size() >3 ) largest.poll();
            if( smallest.size()>2 ) smallest.poll();
        }
        
        int max3=largest.poll();
        int max2=largest.poll();
        int max1=largest.poll();
        //int max4=largest.poll();
        
        int min1=smallest.poll();
        int min2=smallest.poll();
        //int min3=smallest.poll();
        
        //System.out.println(max1+","+max2+","+max3+" | "+min1+","+min2);
        
        return Math.max(max1*max2*max3, max1*min1*min2);
    }
```

# solution 3

Of course you can do it in a 3-loop way.
