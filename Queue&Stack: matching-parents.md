# Question

I like parentheticals (a lot).

"Sometimes (when I nest them (my parentheticals) too much (like this (and this))) they get confusing."

Write a method that, given a sentence like the one above, along with the position of an opening parenthesis, finds the corresponding closing parenthesis.

Example: if the example string above is input with the number 10 (position of the first parenthesis), the output should be 79 (position of the last parenthesis).


# Solution 1
```java
    public static int getClosingParen(String sentence, int openingParenIndex) {

        // find the position of the matching closing parenthesis
        if(sentence.length() > openingParenIndex 
            && sentence.charAt(openingParenIndex) == '(' ){
            Stack<Character> stack = new Stack<>();
            stack.push('(');
            for(int idx=openingParenIndex+1; idx<sentence.length(); ++idx ){
                char c = sentence.charAt(idx);
                if(c=='('){
                    stack.push(c);
                    continue;
                }
                if(c==')'){
                    stack.pop();
                }
                
                if(stack.isEmpty()){
                    return idx;
                }
            }
        }else{
            throw new RuntimeException();
        }
        
        throw new RuntimeException();
    }
```

# Solutiomn 2 O(1) space
```java 
    public static int getClosingParen(String sentence, int openingParenIndex) {

        // find the position of the matching closing parenthesis
        if(sentence.length() > openingParenIndex 
            && sentence.charAt(openingParenIndex) == '(' ){
            int stack=1;
            for(int idx=openingParenIndex+1; idx<sentence.length(); ++idx ){
                char c = sentence.charAt(idx);
                if(c=='('){
                    stack++;
                    continue;
                }
                if(c==')'){
                    stack--;
                }
                
                if(stack==0){
                    return idx;
                }
            }
        }else{
            throw new RuntimeException();
        }
        
        throw new RuntimeException();
    }

```
