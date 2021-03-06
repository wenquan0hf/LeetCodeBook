翻译

```
翻转一个整型数

例1：x = 123, 返回 321
例2：x = -123, 返回 -321
```

原文

```
Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321
```

Have you thought about this? （来自LeetCode官网）

```
Here are some good questions to ask before coding. 
Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? 
ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? 
Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. 
How should you handle such cases?

For the purpose of this problem, 
assume that your function returns 0 when the reversed integer overflows.

Update (2014-11-10):

Test cases had been added to test the overflow behavior.
```

C#

```
public class Solution
{
    public int Reverse(int x)
    {
        try
        {
            string str = Math.Abs(x).ToString();
            string newStr = (x < 0) ? "-" : "";
            for (int i = str.Length - 1; i >= 0; i--)
            {
                newStr += str[i];
            }
            return int.Parse(newStr);
        }
        catch (Exception e)
        {
            return 0;
        }
    }
}
```

C++（来源于网络）

```
class Solution {
public:
    int reverse(int x) {
        int res = 0;
        while(x!=0){
            if(res>INT_MAX/10||res<INT_MIN/10){
                return 0;
            }
            res = res*10 + x%10;
            x = x/10;
        }
        return res;
    }
};
```