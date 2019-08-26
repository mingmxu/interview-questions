# question:


You've built an inflight entertainment system with on-demand movie streaming.

Users on longer flights like to start a second movie right when their first one ends, but they complain that the plane usually lands before they can see the ending. So you're building a feature for choosing two movies whose total runtimes will equal the exact flight length.

Write a method that takes an integer flightLength (in minutes) and an array of integers movieLengths (in minutes) and returns a boolean indicating whether there are two numbers in movieLengths whose sum equals flightLength.

When building your method:

    Assume your users will watch exactly two movies
    Don't make your users watch the same movie twice
    Optimize for runtime over memory


# Solution 1:

just compare each other, with time O(N^2) and space O(1)
```java
    public static boolean canTwoMoviesFillFlight(int[] movieLengths, int flightLength) {

        // determine if two movies add up to the flight length
        for(int i=0; i<movieLengths.length-1; ++i){
            for(int j=i+1; j<movieLengths.length; ++j){
                if(movieLengths[i] + movieLengths[j] == flightLength ){
                    return true;
                }
            }
        }

        return false;
    }
```

# Solution 2:

Use a HashSet to keep visited movies, for a coming movie check if the difference number is there.
```java
    public static boolean canTwoMoviesFillFlight(int[] movieLengths, int flightLength) {

        // determine if two movies add up to the flight length
        Set<Integer> checkedValue = new HashSet<>();
        for(int len : movieLengths){
            if(checkedValue.contains(flightLength-len) ){
                return true;
            }
            checkedValue.add(len);
        }

        return false;
    }
```


