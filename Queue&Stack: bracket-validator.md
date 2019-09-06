# Question

You're working with an intern that keeps coming to you with JavaScript code that won't run because the braces, brackets, and parentheses are off. To save you both some time, you decide to write a braces/brackets/parentheses validator.

Let's say:

    '(', '{', '[' are called "openers."
    ')', '}', ']' are called "closers."

Write an efficient method that tells us whether or not an input string's openers and closers are properly nested.

Examples:

    "{ [ ] ( ) }" should return true
    "{ [ ( ] ) }" should return false
    "{ [ }" should return false

# Solution
```java
    public static boolean isValid(String code) {
        if(code == null) throw new RuntimeException();
        // determine if the input code is valid
        Stack<Character> stack = new Stack<>();

        for(char c : code.toCharArray()){
            switch (c) {
                case '{':
                case '[':
                case '(':
                    stack.push(c);
                    break;
                case ']':
                case '}':
                case ')':
                    if(stack.isEmpty()) return false;
                    char prec = stack.pop();
                    if(
                        (prec=='[' && c!=']')
                        || (prec=='{' && c!='}')
                        || (prec=='(' && c!=')')
                    ){
                        return false;
                    }
                    break;
                default:
                    throw new RuntimeException();
            }
        }
        return stack.isEmpty();
    }
```
