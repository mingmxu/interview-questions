# Question
 Write a method fib() that takes an integer nnn and returns the nnnth Fibonacci ↴ number.

Let's say our Fibonacci series is 0-indexed and starts with 0. So:
```java
fib(0);  // => 0
fib(1);  // => 1
fib(2);  // => 1
fib(3);  // => 2
fib(4);  // => 3
...
```

# Solution 1: simple recursive
```java
    public static int fib(int n) {
        if(n<0) throw new RuntimeException();
        // compute the nth Fibonacci number
        if(n==0) return 0;
        if(n==1) return 1;
        
        return fib(n-1)+fib(n-2);
    }

```

# Solution 2. recursive with memorized
```java
    public static Map<Integer, Integer> checkedValues = new HashMap<>();
    public static int fib(int n) {
        if(checkedValues.containsKey(n)) return checkedValues.get(n);
        
        if(n<0) throw new RuntimeException();
        // compute the nth Fibonacci number
        if(n==0) return 0;
        if(n==1) return 1;
        
        int res = fib(n-1)+fib(n-2);
        checkedValues.put(n, res);
        return res;
    }
```

# Solution 3. button-up DP
```java
    public static int fib(int n) {
        if(n==0) return 0;
        if(n==1) return 1;
        // compute the nth Fibonacci number
        int[] dp = new int[n+1];
        dp[0]=0;
        dp[1]=1;
        
        for(int i=2; i<=n; ++i){
            dp[i]=dp[i-1]+dp[i-2];
        }

        return dp[n];
    }
```    
