# Question

Implement a queue ↴ with 2 stacks. ↴ Your queue should have an enqueue and a dequeue method and it should be "first in first out" (FIFO).

Optimize for the time cost of mmm calls on your queue. These can be any mix of enqueue and dequeue calls.

Assume you already have a stack implementation and it gives O(1)O(1)O(1) time push and pop.



# Solution
```java
    public static class QueueTwoStacks {

        private Deque<Integer> inStack = new ArrayDeque<>();
        private Deque<Integer> outStack = new ArrayDeque<>();

        public void enqueue(int item) {
            inStack.push(item);
        }

        public int dequeue() {
            if(outStack.isEmpty()){
                while(!inStack.isEmpty()){
                    outStack.push(inStack.pop());
                }
            }
            
            if(outStack.isEmpty()) throw new RuntimeException();
            return outStack.pop();
        }
    }

```
