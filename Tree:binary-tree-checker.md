# Question:

 Write a method to check that a binary tree ↴ is a valid binary search tree. ↴

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

# Solution:
```java
    public static boolean isBinarySearchTree(BinaryTreeNode root) {

        // determine if the tree is a valid binary search tree
        Stack<Integer> valueList = new Stack<>();

        return isValid(root, valueList);
    }
    
    public static boolean isValid(BinaryTreeNode node, Stack<Integer> valueList){
        if(node==null){
            return true;
        }
        
        if(!isValid(node.left, valueList)){
            return false;
        }
        
        if(valueList.isEmpty() 
            || (valueList.peek()<node.value ) ){
                valueList.push(node.value);
            }else{
                return false;
            }
        
        if(!isValid(node.right, valueList)){
            return false;
        }
        
        return true;
    }
```    
