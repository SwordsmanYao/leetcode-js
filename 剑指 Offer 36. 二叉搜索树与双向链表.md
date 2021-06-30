https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/

## 递归

```js
/**
 * // Definition for a Node.
 * function Node(val,left,right) {
 *    this.val = val;
 *    this.left = left;
 *    this.right = right;
 * };
 */
/**
 * @param {Node} root
 * @return {Node}
 */
var treeToDoublyList = function(root) {
  if (!root) {
    return;
  }

  const lastNodeRef = {
    current: null,
  };
  convert(root, lastNodeRef);

  let firstNode = lastNodeRef.current;

  while(firstNode.left) {
    firstNode = firstNode.left;
  }

  firstNode.left = lastNodeRef.current;
  lastNodeRef.current.right = firstNode;

  return firstNode;
};

function convert(root, lastNodeRef) {
  if (!root) {
    return;
  }

  convert(root.left, lastNodeRef);

  if (lastNodeRef.current) {
    lastNodeRef.current.right = root;
    root.left = lastNodeRef.current;
  }
  lastNodeRef.current = root;

  convert(root.right, lastNodeRef);
}
```

遍历

```js
/**
 * // Definition for a Node.
 * function Node(val,left,right) {
 *    this.val = val;
 *    this.left = left;
 *    this.right = right;
 * };
 */
/**
 * @param {Node} root
 * @return {Node}
 */
var treeToDoublyList = function(root) {
  if (!root) {
    return;
  }

  const lastNode = convert(root);

  let firstNode = lastNode;

  while (firstNode.left) {
    firstNode = firstNode.left;
  }

  firstNode.left = lastNode;
  lastNode.right = firstNode;

  return firstNode;
};

function convert(root) {
  if (!root) {
    return;
  }

  let current = root;
  const stack = [];
  let lastNode = null;

  while (current || stack.length > 0) {
    while (current) {
      stack.push(current);
      current = current.left;
    }

    current = stack.pop();

    if (lastNode) {
      lastNode.right = current;
      current.left = lastNode;
    }

    lastNode = current;

    current = current.right;
  }

  return lastNode;
}
```
