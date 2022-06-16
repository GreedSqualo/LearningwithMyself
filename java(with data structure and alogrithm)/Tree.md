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
public void Preorder1(TreeNode root){
     if(root == null) return;
     System.out.println(root.val+" ");
     Preorder(root.left);
     Preorder(root.right);
}
```
#### Non-recursive Solution

```
public void Preorder2(TreeNode root){
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
public void Inorder1(TreeNode root){
    if(root==null) return;
    Inorder(root.left);
    System.out.println(root.val+" ");
    Inorder(root.right);
}
```
#### Non-recursive Solution
```
public void Inorder2(TreeNode root){
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
public void Postorder1(TreeNode root){
    if(root==null) return;
    Postorder1(root.left);
    Postorder1(root.right);
    System.out.println(root.val+" ");
}
```
#### Non-recursive Solution
```
public void Postorder2(TreeNode root){
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
public void LevelOrder(TreeNode root){
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
## Maximum Depth
### Top-down Solution
```
private int answer; // don't forget to initialize answer before call maximum_depth
private void maximum_depth(TreeNode root, int depth) {
    if (root == null) {
        return;
    }
    if (root.left == null && root.right == null) {
        answer = Math.max(answer, depth);
    }
    maximum_depth(root.left, depth + 1);
    maximum_depth(root.right, depth + 1);
}
```
### Bottom-up Solution
```
public int maximum_depth(TreeNode root) {
    if (root == null) {
        return 0;                                   // return 0 for null node
    }
    int left_depth = maximum_depth(root.left);
    int right_depth = maximum_depth(root.right);
    return Math.max(left_depth, right_depth) + 1;   // return depth of the subtree rooted at root
}
```

## Symmetric Tree
### Recursive Solution
```
public boolean check(TreeNode root1, TreeNode root2){
    if(root1==null && root2 == null ) return true;
    if(root1==null || root2 == null) return false;
    if(root1.val != root2.val) return false;
    return check(root1.left, root2.right) && check(root1.right, root2.left);
}

public boolean isSymmetric(TreeNode root){
    if(root==null) return false;
    return check(root.left, root.right);
}
```
### Non-recursive Solution
```
public boolean isSymmetric(TreeNode root){
    Queue<TreeNode> q1 = new LinkedList<TreeNode>();
    Queue<TreeNode> q2 = new LinkedList<TreeNode>();
    TreeNode n1 = root;
    TreeNode n2 = root;
    q1.add(n1);
    q2.add(n2);
    while(!q1.isEmpty()||!q2.isEmpty()){
        n1 = q1.poll();
        n2 = q2.poll();
        if(n1==null && n2==null) continue;
        if(n1==null || n2 == null) return false;
        if(n1.val != n2.val ) return false;
        q1.add(n1.left);
        q1.add(n1.right);
        q2.add(n2.right);
        q2.add(n2.left);
    }
    return true;
}
```
