# Question
Hooray! It's opposite day. Linked lists go the opposite way today.

Write a method for reversing a linked list. ↴ Do it in place. ↴

Your method will have one input: the head of the list.

Your method should return the new head of the list.

Here's a sample linked list node class:
```java
  public class LinkedListNode {

    public int value;
    public LinkedListNode next;

    public LinkedListNode(int value) {
        this.value = value;
    }
}
```


# Solution 1: O(N) time, O(1) space
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static LinkedListNode reverse(LinkedListNode headOfList) {
        if(headOfList == null) return null;
        // reverse the linked list in place
        LinkedListNode pre=null;
        LinkedListNode cur=headOfList;
        LinkedListNode next = cur.next;
        while(next != null){
            cur.next=pre;
            pre=cur;
            LinkedListNode temp=next.next;
            next.next=cur;
            cur=next;
            next=temp;
        }

        return cur;
    }
```

# Solution 2: O(N) time, O(N) space
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static LinkedListNode reverse(LinkedListNode headOfList) {
        if(headOfList == null) return null;
        // reverse the linked list in place
        List<LinkedListNode> nodeList = new ArrayList<>();
        while(headOfList != null){
            nodeList.add(headOfList);
            headOfList = headOfList.next;
        }
        
        nodeList.get(0).next=null;
        for(int idx=1; idx<nodeList.size(); idx++){
            nodeList.get(idx).next=nodeList.get(idx-1);
        }
        
        return nodeList.get(nodeList.size()-1);
    }
```

# Solution 3. make a reversed deep copy
```java
    public static class LinkedListNode {

        public int value;
        public LinkedListNode next;

        public LinkedListNode(int value) {
            this.value = value;
        }
    }

    public static LinkedListNode reverse(LinkedListNode headOfList) {

        // reverse the linked list in place
        LinkedListNode preNode=null;
        while(headOfList != null){
            LinkedListNode newNode = new LinkedListNode(headOfList.value);
            newNode.next=preNode;
            preNode=newNode;
            headOfList = headOfList.next;
        }

        return preNode;
    }
```
