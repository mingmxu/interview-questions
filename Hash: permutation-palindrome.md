# Question:

Write an efficient method that checks whether any permutation ↴ of an input string is a palindrome. ↴

You can assume the input string only contains lowercase letters.

Examples:

    "civic" should return true
    "ivicc" should return true
    "civil" should return false
    "livci" should return false

"But 'ivicc' isn't a palindrome!"

If you had this thought, read the question again carefully. We're asking if any permutation of the string is a palindrome. Spend some extra time ensuring you fully understand the question before starting. Jumping in with a flawed understanding of the problem doesn't look good in an interview.


# Solution:

```java
    public static boolean hasPalindromePermutation(String theString) {

        // check if any permutation of the input is a palindrome
        Set<Character> restChars = new HashSet<>();
        for(char c : theString.toCharArray()){
            if(restChars.contains(c) ){
                restChars.remove(c);
            }else{
                restChars.add(c);
            }
        }

        return restChars.size()<=1;
    }
```    
