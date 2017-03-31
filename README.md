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

### 190. Reverse Bits
Reverse bits of a given 32 bits unsigned integer.

#### For example
given 
```
input 43261596 (represented in binary as 00000010100101000001111010011100)
```

```
, return 964176192 (represented in binary as 00111001011110000010100101000000).
```


#### Follow up:
If this function is called many times, how would you optimize it?

### 问题
反转比特
### 思路
1. 每次取最后一位加入result
2. 再将imput右移抛出已加入的数字

### C++

```
 uint32_t reverseBits(uint32_t input)
{
    uint32_t result = 0;
    const uint32_t BITS_OF_BYTES = 8 ;
    for (int i=0; i<sizeof(input)*BITS_OF_BYTES; i++) {
        result = (result << 1 )|(input & 1);            //result左移空出位置，将input最后一位加入
        input = input >> 1;                            //input右移
    }
    
    
    return result;
}
```

### 500. Keyboard Row

Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.
![image](https://leetcode.com/static/images/problemset/keyboard.png)
#### Example 1:

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```
#### Note:
You may use one character in the keyboard more than once.

You may assume the input string will only contain letters of alphabet.
#### 问题
给你一列表的单词，返回那些只包含美式键盘一行的单词
#### 思路
查每个单词的第一个字母，将其设为某行，随后遍历每个字母，看是否都在那一行
#### C++

```
std::vector<std::string> findWords(std::vector<std::string> &words)
{

    std::unordered_set<char> set1 = {'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'};
    std::unordered_set<char> set2 = {'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'};
    std::unordered_set<char> set3 = {'z', 'x', 'c', 'v', 'b', 'n', 'm'};
    std::vector<std::unordered_set<char>> sets = {set1, set2, set3};

    std::vector<std::string> result;

    for (int i = 0; i < words.size(); i++) {
        int index = 0, flag = 0;
        if (set1.find(tolower(words[i][0])) != set1.end()) {
            index = 0;
        } else if (set2.find(tolower(words[i][0])) != set2.end()) {
            index = 1;
        } else {
            index = 2;
        }

        std::unordered_set<char> tempset = sets[index];

        for (char a : words[i]) {
            if (tempset.find(tolower(a)) == tempset.end()) {
                flag = 1;
                break;
            }

        }
        
        if (flag == 0) {
            result.push_back(words[i]);
        }
    }

    return result;
}

```
#### 收获
==using namespace std; or using std::xxxxx；==
### 412. Fizz Buzz
Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.
#### Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
#### 问题
给一个N 从1到n中的数 放入数组，如果是三的倍数输出Fizz，五的倍数输出Buzz，三五的倍数输出FizzBuzz
#### 思路
分支判断
#### C++

```
using namespace std;

vector<string> fizzBuzz(int n)
{
    vector<string> a;
    for (int i = 1; i <= n; i++) {
        if (i%15==0) {
            a.push_back("FizzBuzz");
        }else if (i%5==0){
            a.push_back("Buzz");
        }else if (i%3==0){
            a.push_back("Fizz");
        }else{
            a.push_back(to_string(i));
        }
    }
    return a;
}

```
#### 收获
==to_string()== int=>string
#### 别人写法

```
vector<string> fizzBuzz(int n) {
        vector<string> ret_vec(n);
        for(int i=1; i<=n; ++i)
        {
            if(i%3 == 0)
            {
                ret_vec[i-1] += string("Fizz");
            }
            if(i%5 == 0)
            {
                ret_vec[i-1] += string("Buzz");
            }
            if(ret_vec[i-1] == "")
            {
                ret_vec[i-1] += to_string(i);
            }
        }
        return ret_vec;
    } 
```
### 344. Reverse String
Write a function that takes a string as input and returns the string reversed.
#### Example:

```
Given s = "hello", return "olleh".
```
### C++

```
string reverseString(string s) {
    
    if(s==""){
        return "";
    } ;
    string result = "";
    int length = (int)s.length();
    
    if(length != 0)
    {
        for (int i = length; i>0; i--) {
            char temp = s[i-1];
            result+=temp;       }
    }

    
    return result;
}

```
#### 别人写法

```
 string reverseString(string s) {
        int i = 0, j = s.size() - 1;
        while(i < j){
            swap(s[i++], s[j--]); 
        }
        
        return s;
    }
```
#### 收获

```
swap函数
```
### 496. Next Greater Element I
You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.
#### Example 1:

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```
#### Example 2:

```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```
#### Note:
All elements in nums1 and nums2 are unique.

The length of both nums1 and nums2 would not exceed 1000.
### C++

```
vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
    int n = findNums.size();
    int m = nums.size();
    vector<int> result(n);
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if (findNums[i] == nums[j]) {

                for (int k=j; k<m; k++) {
                    if (nums[k]>findNums[i]) {
                        result[i]=nums[k];
                        break;
                    }
                    
                }
                if (!result[i]) {
                    result[i]=-1;
                }
                
                break;
            }else{
                result[i] = -1;
            }
        }
        
    }
    return result;
}
```
### 别人写法

```

```
