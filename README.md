# LeetCode

### 461. Hamming Distance
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.


### Note:
0 ≤ x, y < 231.

### Example:


```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```
### 问题
求两个数的二进制表示中，不同位数的个数。
### 思路
1. 将两个数进行异或
2. 统计异或后的数字中1的个数
### C++

```
class Solution {
public:
    int hammingDistance(int x, int y) {
        int dist = 0; int n = x^y;  //异或
        while(n)
        {
            ++dist;
            n = n&(n-1);
        }
        return dist;
    }
};
```

### 476. Number Complement
Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

The above arrows point to positions where the corresponding bits are different.
#### Note:
The given integer is guaranteed to fit within the range of a 32-bit signed integer.
You could assume no leading zero bit in the integer’s binary representation.
#### Example 1:

```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2
```

#### Example 2:

```
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```
### 问题
取一个正整数的二进制表达的反
### 思路
1. 制作一个mask 将正整数的二进制位数对应的位数 置为0；
2. 将正整数取反 与 ~mask(00000000111)作与运算

### C++

```
class Solution {
public:
    int findComplement(int num) {
      unsigned mask = ~0;             //制作mask
        while (num & mask) mask <<= 1;//根据正整数的二进制位数 将mask对应的位数置为0；
        return ~mask & ~num;          //将正整数取反，与mask作与运算
    }
};
```
