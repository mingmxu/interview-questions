# Question
 Write a method to see if a binary tree ↴ is "superbalanced" (a new tree property we just made up).

A tree is "superbalanced" if the difference between the depths of any two leaf nodes ↴ is no greater than one.

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
    public static class NodeDepth{
        public NodeDepth(BinaryTreeNode node, int depth){
            this.node=node;
            this.depth=depth;
        }
        public BinaryTreeNode node;
        public int depth;
    }
    public static boolean isBalanced(BinaryTreeNode treeRoot) {
        if(treeRoot==null) return true;
        // determine if the tree is superbalanced
        List<Integer> uniqd = new ArrayList<>();
        Stack<NodeDepth> queue = new Stack<>();
        queue.add(new NodeDepth(treeRoot, 1));
        while(!queue.isEmpty()){
            NodeDepth node = queue.pop();
            if(node.node.left==null && node.node.right==null){
                int d = node.depth;
                if(!uniqd.contains(d)){
                    uniqd.add(d);
                }
                if(uniqd.size()>2) return false;
            }else{
                if(node.node.left!=null) queue.push(new NodeDepth(node.node.left, node.depth+1));
                if(node.node.right!=null) queue.push(new NodeDepth(node.node.right, node.depth+1));
            }
        }

        return uniqd.size()==1
            || (uniqd.size()==2 && Math.abs(uniqd.get(0)-uniqd.get(1))==1);
    }
```    
