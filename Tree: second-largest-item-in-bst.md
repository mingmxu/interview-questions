# Question
 Write a method to find the 2nd largest element in a binary search tree. ↴

Here's a sample binary tree node class:
```java
  public class BinaryTreeNode {

    public int value;
    public BinaryTreeNode left;
    public BinaryTreeNode right;

    public BinaryTreeNode(int value) {
        this.value = value;
    }

    public BinaryTreeNode insertLeft(int leftValue) {
        this.left = new BinaryTreeNode(leftValue);
        return this.left;
    }

    public BinaryTreeNode insertRight(int rightValue) {
        this.right = new BinaryTreeNode(rightValue);
        return this.right;
    }
}
```

# Solution
```java
    public static int findSecondLargest(BinaryTreeNode rootNode) {

        // find the second largest item in the binary search tree
        List<Integer> values = new ArrayList<>();
        scan(rootNode, values);
        
        if(values.size()<2) throw new RuntimeException();
        return values.get(1);
    }
    
    public static void scan(BinaryTreeNode node, List<Integer> values){
        if(node==null) return;
        
        scan(node.right, values);
        
        values.add(node.value);
        if(values.size()>=2) return;
        
        scan(node.left, values);
    }
```
