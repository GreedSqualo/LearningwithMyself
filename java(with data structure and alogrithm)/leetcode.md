Tree
======

## Traverse a Tree
```
/*
  Definition for a binary tree node.
  public class TreeNode {
      int val;
      TreeNode left;
      TreeNode right;
      TreeNode() {}
      TreeNode(int val) { this.val = val; }
      TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
      }
  }
 */
 ```
### Preorder Traversal
#### Recursive Solution
```
public void static Preorder1(TreeNode root){
     if(root == null) return;
     System.out.println(root.val+" ");
     Preorder(root.left);
     Preorder(root.right);
}
```
#### Non-recursive Solution

```
public void static Preorder2(TreeNode root){
    Stack<TreeNode> q = new Stack<TreeNode>();
    q.add(root);
    while(!q.isEmpty()){
        TreeNode tn = q.pop();
        System.out.println(tn.val+" ");
        if(tn.right!=null) q.add(tn.right);
        if(tn.left!=null) q.add(tn.left);
    }
}
```

### Inorder Traversal
#### Recursive Solution
```
public void static Inorder1(TreeNode root){
    if(root==null) return;
    Inorder(root.left);
    System.out.println(root.val+" ");
    Inorder(root.right);
}
```
#### Non-recursive Solution
```
public void static Inorder2(TreeNode root){
    if(root==null) return;
    Stack<TreeNode> q = new Stack<TreeNode>();
    TreeNode current = root;
    while(current!=null || !q.isEmpty()) {
        while(current!=null) {
            q.add(current);
            current = current.left;
        }
        if(!q.isEmpty()){
            current = q.pop();
            System.out.println(current.val+" ");
            current = current.right;
        }
    }
}
```
### Postorder Traversal
#### Recursive Solution
```
public void static Postorder1(TreeNode root){
    if(root==null) return;
    Postorder1(root.left);
    Postorder1(root.right);
    System.out.println(root.val+" ");
}
```
#### Non-recursive Solution
```
public void static Postorder2(TreeNode root){
    if(root==null) return;
    TreeNode current = root;
    Stack<TreeNode> s1 = new Stack<TreeNode>();
    Stack<TreeNode> s2 = new Stack<TreeNode>();
    while(current!=null || !s1.isEmpty()){
        while(current!=null){
            s1.add(current);
            s2.add(current);
            current = current.left;
        }
        if(!s1.isEmpty()){
            current = s1.pop();
            current = current.right;
        }
    }
    while(!s2.isEmpty()){
        current = s2.pop();
        System.out.println(current.val+" ");
    }   
}
```

### Level Order Traversal
```
public void static LevelOrder(TreeNode root){
    if(root == null) return;
    Queue<TreeNode> q = new LinkedList<TreeNode>();
    TreeNode current = root;
    q.add(current);
    while(!q.isEmpty()){
        current = q.poll();
        System.out.println(current.val+" ");
        if(current.left!=null) q.add(current.left);
        if(current.right!=null) q.add(current.right);
    }
}
```
