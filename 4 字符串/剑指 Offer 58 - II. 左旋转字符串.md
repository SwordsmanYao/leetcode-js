# 剑指 Offer 58 - II. 左旋转字符串

https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/


字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

示例 1：

输入: s = "abcdefg", k = 2
输出: "cdefgab"



讲解：
https://github.com/youngyangyang04/leetcode-master/blob/master/problems/%E5%89%91%E6%8C%87Offer58-II.%E5%B7%A6%E6%97%8B%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.md


```js
/**
 * @param {string} s
 * @param {number} n
 * @return {string}
 */
 var reverseLeftWords = function(s, n) {
  const strArr = Array.from(s);
  reverse(strArr, 0, n - 1);
  reverse(strArr, n, strArr.length - 1);
  reverse(strArr, 0, strArr.length - 1);
  return strArr.join('');
};

// 翻转从 start 到 end 的字符
function reverse(strArr, start, end) {
  let left = start;
  let right = end;

  while(left < right) {
    // 交换
    [strArr[left], strArr[right]] = [strArr[right], strArr[left]];
    left++;
    right--;
  }
}
```
