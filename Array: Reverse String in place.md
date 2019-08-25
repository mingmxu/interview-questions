**Question**:


Write a method that takes an array of characters and reverses the letters in place. ↴

> Why an array of characters instead of a string?
>
> The goal of this question is to practice manipulating strings in place. Since we're modifying the input, we need a mutable ↴ type like an array, instead of Java's immutable strings.

## Solution: two-pointer swap
```java
    public static void reverse(char[] arrayOfChars) {
        // reverse input array of characters in place
        for(int s=0, e=arrayOfChars.length-1; s<e; s++, e--){
            swap(arrayOfChars, s, e);
        }

    }
    
    private static void swap(char[] arrayOfChars, int s, int e){
        char temp = arrayOfChars[s];
        arrayOfChars[s]=arrayOfChars[e];
        arrayOfChars[e]=temp;
    }

```
