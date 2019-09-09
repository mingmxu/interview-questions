# Question
You have a singly-linked list ↴ and want to check if it contains a cycle.

A singly-linked list is built with nodes, where each node has:

    node.next—the next node in the list.
    node.value—the data held in the node. For example, if our linked list stores people in line at the movies, node.value might be the person's name.

For example:
```java
  public class LinkedListNode {

    public int value;
    public LinkedListNode next;

    public LinkedListNode(int value) {
        this.value = value;
    }
}
```
A cycle occurs when a node’s next points back to a previous node in the list. The linked list is no longer linear with a beginning and end—instead, it cycles through a loop of nodes.

Write a method containsCycle() that takes the first node in a singly-linked list and returns a boolean indicating whether the list contains a cycle. 


# Solution 1. O(N) time + O(N) space
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static boolean containsCycle(LinkedListNode firstNode) {

        // check if the linked list contains a cycle
        Set<LinkedListNode> visitedNode = new HashSet<>();
        while(firstNode != null){
            if(visitedNode.contains(firstNode)){
                return true;
            }
            visitedNode.add(firstNode);
            firstNode = firstNode.next;
        }

        return false;
    }
```

# Solution 2. O(N) time + O(1) space
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static boolean containsCycle(LinkedListNode firstNode) {
        if(firstNode==null) return false;
        // check if the linked list contains a cycle
        LinkedListNode step1=firstNode;
        LinkedListNode step2=firstNode.next;
        while(step1!=null && step2 != null){
            if(step1==step2) return true;
            step1=step1.next;
            step2=step2.next;
            if(step2==null) return false;
            step2=step2.next;
        }

        return false;
    }
```
