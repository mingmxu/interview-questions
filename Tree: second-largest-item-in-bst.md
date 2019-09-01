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

# Solution 1. recursive
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

# Solutiom 2. non-recursive
```java
    public static int findSecondLargest(BinaryTreeNode rootNode) {

        // find the second largest item in the binary search tree
        if(rootNode==null || (rootNode.left==null && rootNode.right==null)) 
            throw new RuntimeException();
            
        BinaryTreeNode parent=rootNode;
        BinaryTreeNode maxRight=parent;
        while(maxRight.right != null){
            parent=maxRight;
            maxRight=maxRight.right;
        }
        
        if(maxRight.right==null && maxRight.left!=null){
            BinaryTreeNode sndRoot=maxRight.left;
            while(sndRoot.right!=null){
                sndRoot=sndRoot.right;
            }
            return sndRoot.value;
        }
        
        return parent.value;
    }

```
