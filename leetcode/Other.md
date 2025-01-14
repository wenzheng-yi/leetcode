### 位1的个数

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为[汉明重量](https://baike.baidu.com/item/汉明重量)）。

````javascript
/**
 * @param {number} n - a positive integer
 * @return {number}
 */
var hammingWeight = function (n) {
  let times = 0
  while (n) {
    n &= n - 1
    ++times
  }
  return times
};
````

### 汉明距离

两个整数之间的 [汉明距离](https://baike.baidu.com/item/汉明距离) 指的是这两个数字对应二进制位不同的位置的数目。

给你两个整数 `x` 和 `y`，计算并返回它们之间的汉明距离。

````javascript
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
var hammingDistance = function(x, y) {
  let z = x ^ y
  let res = 0
  while(z){
    z &= z -1
    res++
  }
  return res
};
````

### 颠倒二进制位

颠倒给定的 32 位无符号整数的二进制位。

````javascript
/**
 * @param {number} n - a positive integer
 * @return {number} - a positive integer
 */
var reverseBits = function(n) {
  let rev = 0
  for (let i = 0; i < 32 && n > 0; ++ i) {
    rev |= (n & 1) << (31 - i)
    n >>>= 1
  }
  return rev >>> 0
};
````

### 杨辉三角

给定一个非负整数 *`numRows`，*生成「杨辉三角」的前 *`numRows`* 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

````javascript
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function (numRows) {
  let result = []
  for (let i = 0; i < numRows; ++i) {
    let nums = new Array(i + 1).fill(1)
    for (let k = 1; k < nums.length - 1; ++k) {
      nums[k] = result[i - 1][k - 1] + result[i - 1][k]
    }
    result.push(nums)
  }
  return result;
};
````

### 有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

1、左括号必须用相同类型的右括号闭合。
2、左括号必须以正确的顺序闭合。

````javascript
/**
 * @param {string} s
 * @return {boolean}
 */
const map = new Map([
  ['(', ')'],
  ['[', ']'],
  ['{', '}']
])
var isValid = function (s) {
  let brackets = []
  for (let i = 0; i < s.length; ++i) {
    if (s.charAt(i) == map.get(brackets[brackets.length - 1])) {
      brackets.pop()
    } else {
      brackets.push(s.charAt(i))
    }
  }
  return brackets.length == 0
};
````

### 缺失的数字

给定一个包含 `[0, n]` 中 `n` 个数的数组 `nums` ，找出 `[0, n]` 这个范围内没有出现在数组中的那个数。

````javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
   let missing = nums.length;
   for ( let i = 0; i < nums.length; ++i) {
     missing ^= i ^ nums[i]
   }
   return missing
};
````

### [用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

```javascript
var CQueue = function() {
  this.inStack = []
  this.outStack = []
};

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
  this.inStack.push(value)
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
  if (!this.outStack.length) {
      if (!this.inStack.length) {
          return -1
      }
      this.in2out()
  }
  return this.outStack.pop()
};

CQueue.prototype.in2out = function() {
    while (this.inStack.length) {
        this.outStack.push(this.inStack.pop())
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */
```

