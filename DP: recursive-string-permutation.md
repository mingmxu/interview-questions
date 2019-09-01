# Question

Write a recursive method for generating all permutations of an input string. Return them as a set.

Don't worry about time or space complexity—if we wanted efficiency we'd write an iterative version.

To start, assume every character in the input string is unique.

Your method can have loops—it just needs to also be recursive.


# Solution 1: backtracking
```java
    public static Set<String> getPermutations(String inputString) {

        // generate all permutations of the input string
        List<Integer> charIndexes = new ArrayList<>();
        Set<String> results = new HashSet<>();
        
        char[] inputAsChars = inputString.toCharArray();
        
        combination(charIndexes, results, inputAsChars, 0);
        
        return results;
    }
    
    public static void combination(List<Integer> charIndexes, Set<String> results
        , char[] inputAsChars, int nextIndex){
        if(nextIndex==inputAsChars.length){
            results.add(toString(charIndexes, inputAsChars));
            return;
        }
        
        for(int idx=0; idx<inputAsChars.length; ++idx){
            if(charIndexes.contains(idx)){
                continue;
            }
            charIndexes.add(idx);
            combination(charIndexes, results, inputAsChars, nextIndex+1);
            charIndexes.remove(nextIndex);
        }
    }
    
    public static String toString(List<Integer> charIndexes, char[] inputAsChars){
        StringBuilder sb = new StringBuilder();
        for(int idx : charIndexes){
            sb.append(inputAsChars[idx]);
        }
        return sb.toString();
    }

```

# solution 2: simple recursive
```java
    public static Set<String> getPermutations(String inputString) {

        // generate all permutations of the input string
        Set<String> results = new HashSet<>();
        
        if(inputString.equals("")){
            results.add("");
            return results;
        }
        
        if(inputString.length()==1){
            results.add(inputString);
            return results;
        }
        
        Set<String> subSet = getPermutations(inputString.substring(1));
        char restChar=inputString.charAt(0);
        for(String ss : subSet){
            for(int ssidx=0; ssidx<=ss.length(); ++ssidx){
                results.add(new StringBuilder()
                    .append(ss.substring(0,ssidx))
                    .append(restChar)
                    .append(ss.substring(ssidx)).toString() );
            }
        }

        return results;
    }
```
