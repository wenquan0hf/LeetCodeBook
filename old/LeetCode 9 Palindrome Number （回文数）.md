翻译

```
确定一个整数是否是回文数。不能使用额外的空间。

一些提示：

负数能不能是回文数呢？（比如，-1）

如果你想将整数转换成字符串，但要注意限制使用额外的空间。

你也可以考虑翻转一个整数。
然而，如果你已经解决了问题“翻转整数（译者注：LeetCode 第七题），
那么你应该知道翻转的整数可能会造成溢出。
你将如何处理这种情况？

这是一个解决该问题更通用的方法。
```

原文

```
Determine whether an integer is a palindrome. Do this without extra space.

Some hints:

Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. 
However, if you have solved the problem "Reverse Integer", 
you know that the reversed integer might overflow. 
How would you handle such case?

There is a more generic way of solving this problem.
```

一开始的想法，大不了不新建一个字符串，直接在循环里用就好了，结果居然也可以accept。

```
public class Solution
{
    public bool IsPalindrome(int x)
    {       
        for (int i = 0; i < x.ToString().Length / 2; i++)
        {
            if ((x.ToString())[i] != x.ToString()[x.ToString().Length - i - 1])
            {
                return false;
            }        
        }
        return true;           
    }
}
```

可是叻：

```
11506 / 11506 test cases passed.
Status: Accepted
Runtime: 244 ms
Your runtime beats 0.97% of csharp submissions.
```

然后修改了一下：

```
public class Solution
{
    public bool IsPalindrome(int x)
    {       
        if (x < 0)
            return false;       
        // 判断x的长度，比如x=232，div就等于100
        int div = 1;
        while (x / div >= 10)
            div *= 10;      
        while (x != 0)
        {
            // 左边开始计数
            int left = x / div;
            // 右边开始计数
            int right = x % 10;      
            if (left != right)
                return false;    
            x = (x % div) / 10;
            div /= 100;
        }
        return true;   
    }
}
```
性能还是不尽如人意呀，不过同样的代码放在Java上，貌似C#要快一些。
```

11506 / 11506 test cases passed.
Status: Accepted
Runtime: 196 ms
Your runtime beats 21.36% of csharp submissions.
```

下面这份代码是网上找到的，性能和上面的一模一样：

```
public class Solution
{
    public bool IsPalindrome(int x)
    {
        if (x < 0)
            return false;
        else if (x == 0)
            return true;
        else
        {
            int tmp = x;
            int y = 0;
            while (x != 0)
            {
                y = y * 10 + x % 10;
                x = x / 10;
            }
            if (y == tmp)
                return true;
            else
                return false;
        }
    }
}
```