https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/

## 前序遍历序列化
节点为null时用下划线(_)占位
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */

/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
 var serialize = function(root) {
   const result = [];
  serializeTree(root, result);

  return result.join(',');
};

function serializeTree(root, result) {
  if (!root) {
    result.push('_');
    return;
  }
  result.push(root.val);
  serializeTree(root.left, result);
  serializeTree(root.right, result);
}

/**
 * Decodes your encoded data to tree.
 *
 * @param {string} data
 * @return {TreeNode}
 */
var deserialize = function(data) {
  if (data === '_') {
    return null;
  }

  const dataArr = data.split(',');
  const rootVal = dataArr.shift();
  const root = new TreeNode(rootVal);
  deserializeTree(root, dataArr)
  return root;
};

function deserializeTree(parent, dataArr) {
  const left = dataArr.shift();
  if (left && left !== '_') {
    parent.left = new TreeNode(left);
    deserializeTree(parent.left, dataArr);
  }

  const right = dataArr.shift();
  if (right && right !== '_') {
    parent.right = new TreeNode(right);
    deserializeTree(parent.right, dataArr);
  }
}
/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */
```
