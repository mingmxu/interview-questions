# Question
You have a linked list ↴ and want to find the kkkth to last node.

Write a method kthToLastNode() that takes an integer kkk and the headNode of a singly-linked list, and returns the kkkth to last node in the list.

For example:
```java
  public class LinkedListNode {

    public String value;
    public LinkedListNode next;

    public LinkedListNode(String value) {
        this.value = value;
    }
}

LinkedListNode a = new LinkedListNode("Angel Food");
LinkedListNode b = new LinkedListNode("Bundt");
LinkedListNode c = new LinkedListNode("Cheese");
LinkedListNode d = new LinkedListNode("Devil's Food");
LinkedListNode e = new LinkedListNode("Eccles");

a.next = b;
b.next = c;
c.next = d;
d.next = e;

kthToLastNode(2, a);
// returns the node with value "Devil's Food" (the 2nd to last node)
```

# Solution 1. O(N) time, O(k) space
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static LinkedListNode kthToLastNode(int k, LinkedListNode head) {
        if(k<=0) throw new RuntimeException();
        // return the kth to last node in the linked list
        Deque<LinkedListNode> queue = new LinkedList<>();
        int curSize=0;
        while(head!=null){
            queue.addLast(head);
            curSize++;
            head=head.next;
            if(curSize>k){
                queue.pollFirst();
                curSize--;
            }
        }
        
        if(curSize<k) throw new RuntimeException();
        return queue.pollFirst();
    }
```

# Solution 2: O(N) time, O(1) space
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static LinkedListNode kthToLastNode(int k, LinkedListNode head) {
        if(k<=0) throw new RuntimeException();
        // return the kth to last node in the linked list
        
        int size=0;
        LinkedListNode newHead = head;
        while(newHead!=null){
            size++;
            newHead=newHead.next;
        }
        
        if(size<k) throw new RuntimeException();
        while(head!=null){
            if(size==k) return head;
            size--;
            head=head.next;
        }
        
        return null;
    }
```
