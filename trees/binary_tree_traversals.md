# Tree Traversals (fun)

## In-Order Traversal (Recursion)
```java
public List<Integer> inorderTraversal(TreeNode root) {
	List<Integer> rec = new ArrayList();
	if (root==null) return rec;
	rec.addAll(inorderTraversal(root.left));
	rec.add(root.val);
	rec.addAll(inorderTraversal(root.right));
	return rec;
}
```

## In-Order Traversal (Iterative)
```java
// code by yours truly (@caash22)
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        if (root == null) return new ArrayList<Integer>();
        List<Integer> inOrderTrav = new ArrayList<Integer>();
        Set<TreeNode> visited = new HashSet<TreeNode>();
        Stack<TreeNode> depth = new Stack<TreeNode>();
        depth.add(root);
        while (!depth.isEmpty()){
            TreeNode curr = depth.peek();
            if (curr.left == null || visited.contains(curr.left)){
                curr = depth.pop();
                visited.add(curr);
                inOrderTrav.add(curr.val);
                if (curr.right != null && !visited.contains(curr.right) && !depth.contains(curr.right)) depth.push(curr.right);
            } else if (curr.left != null && !visited.contains(curr.left) && !depth.contains(curr.left)) {
                depth.push(curr.left);
            }
        }
        return inOrderTrav;
    }
}
```

## Pre-Order Traversal (Recursion)
```java
public List<Integer> inorderTraversal(TreeNode root) {
	List<Integer> rec = new ArrayList();
	if (root==null) return rec;
	rec.add(root.val);
	rec.addAll(inorderTraversal(root.left));
	rec.addAll(inorderTraversal(root.right));
	return rec;
}
```

## Pre-Order Traversal (Iterative)
```java
// Code by yours truly (@caash22)
/**
* Definition for a binary tree node.
* public class TreeNode {
*     int val;
*     TreeNode left;
*     TreeNode right;
*     TreeNode(int x) { val = x; }
* }
*/
class Solution {
	public List<Integer> preorderTraversal(TreeNode root) {
		List<Integer> preOrderTrav = new ArrayList<Integer>();
		if (root == null) return preOrderTrav;
		Set<TreeNode> visited = new HashSet<TreeNode>();
		Stack<TreeNode> depth = new Stack<TreeNode>();
		depth.add(root);
		while (!depth.isEmpty()){
			TreeNode curr = depth.pop();
			visited.add(curr);
			preOrderTrav.add(curr.val);
			if (curr.right != null && !visited.contains(curr.right) && !depth.contains(curr.right)) depth.push(curr.right);
			if (curr.left != null && !visited.contains(curr.left) && !depth.contains(curr.left)) depth.push(curr.left);
		}
	return preOrderTrav;
	}
}
```


## Post-Order Traversal (Recursion)
```java
public List<Integer> inorderTraversal(TreeNode root) {
	List<Integer> rec = new ArrayList();
	if (root==null) return rec;
	rec.addAll(inorderTraversal(root.left));
	rec.addAll(inorderTraversal(root.right));
	rec.add(root.val);
	return rec;
}
```

## Post-Order Traversal (Iterative)
```java
// Code by your's truly @caash22
/**
* Definition for a binary tree node.
* public class TreeNode {
*     int val;
*     TreeNode left;
*     TreeNode right;
*     TreeNode(int x) { val = x; }
* }
*/
class Solution {
	public List<Integer> postOrderTraversal(TreeNode root) {
		List<Integer> postOrderTrav = new ArrayList<Integer>();
		if (root == null) return postOrderTrav;
		Set<TreeNode> visited = new HashSet<TreeNode>();
		Stack<TreeNode> depth = new Stack<TreeNode>();
		depth.add(root);
		while (!depth.isEmpty()){
			TreeNode curr = depth.peek();
			if ((curr.left == null || visited.contains(curr.left)) && 
			(curr.right == null || visited.contains(curr.right))){
			curr = depth.pop();
			visited.add(curr);
			postOrderTrav.add(curr.val);
			} else {
				if (curr.left != null && !visited.contains(curr.left) && !depth.contains(curr.left)) depth.push(curr.left);
				else if (curr.right != null && !visited.contains(curr.right) && !depth.contains(curr.right)) depth.push(curr.right);
			}
		}
		return postOrderTrav;
	}
}
```

## Level Traversal Over an N-ary tree
```java
//code by yours truly (@caash22)
/*
// Definition for a Node.
class Node {
	public int val;
	public List<Node> children;

	public Node() {}

	public Node(int _val,List<Node> _children) {
		val = _val;
		children = _children;
	}
};
*/
class Solution {
	public List<List<Integer>> levelOrder(Node root) {
		List<List<Integer>> answer = new ArrayList<List<Integer>>();
		if (root == null) return answer;
		Set<Node> visited = new HashSet<Node>();
		levelOrderHelper(root, visited, answer, 0);
		return answer;
	}
	private void levelOrderHelper(Node root, Set<Node> visited, List<List<Integer>> answer, int level){
		while (answer.size() <= level) answer.add(new ArrayList<Integer>());
		visited.add(root);
		answer.get(level).add(root.val);
		if (root.children != null){
			Iterator<Node> itr = root.children.iterator();
			while(itr.hasNext()){
				Node temp = itr.next();
				if (!visited.contains(temp)){
					levelOrderHelper(temp, visited, answer, level + 1);
				}
			}
		}
	}
}
```