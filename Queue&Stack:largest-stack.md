# Question

You want to be able to access the largest element in a stack. ↴

Use the built-in Stack class to implement a new class MaxStack with a method getMax() that returns the largest element in the stack. getMax() should not remove the item.

Your stacks will contain only integers.



# Solution
```java
    public static class MaxStack {
        private Stack<Integer> values = new Stack<>();
        private Stack<Integer> maxValues = new Stack<>();
        
        public void push(int item) {
            values.push(item);
            if(maxValues.isEmpty()){
                maxValues.push(item);
            }else{
                maxValues.push(Math.max(item, maxValues.peek()));
            }
        }

        public int pop() {
            if(values.isEmpty()) throw new RuntimeException();
            maxValues.pop();
            return values.pop();
        }

        public int getMax() {
            if(maxValues.isEmpty()) throw new RuntimeException();
            return maxValues.peek();
        }
    }
```
