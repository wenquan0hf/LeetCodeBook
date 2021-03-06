翻译

```
给定一个字符串S，找出它的最大回文子字符串。
你可以假定S的最大长度为1000，
并且这里存在唯一一个最大回文子字符串。
```

原文
```
Given a string S, find the longest palindromic substring in S. 
You may assume that the maximum length of S is 1000, 
and there exists one unique longest palindromic substring.
```

暴力搜索，$O(n^3)$

```
public static string LongestPalindrome(string s)
{
    int len = s.Length;
    for (int i = len; i > 0; i--)
        for (int j = 1; j <= len + 1 - i; j++)
            if (isPalindrome(s.Substring(j - 1, i)))
                return s.Substring(j - 1, i);
    return null;
}

public static bool isPalindrome(string s)
{
    for (int i = 0; i < s.Length / 2; i++)
        if (s.Substring(i, 1) != s.Substring(s.Length - 1 - i, 1))
            return false;

    return true;
}
```

动态规划，时间：$O(n^2)$，空间：$O(n^2)$

```
public class Solution
{
    public string LongestPalindrome(string s)
    {
        int sLen = s.Length;
        int lonBeg = 0; int maxLen = 1;
        bool[,] DP = new bool[1000, 1000];
        for (int i = 0; i < sLen; i++)
        {
            DP[i, i] = true;
        }
        for (int i = 0; i < sLen - 1; i++)
        {
            if (s[i] == s[i + 1])
            {
                DP[i, i + 1] = true;
                lonBeg = i;
                maxLen = 2;
            }
        }
        for (int len = 3; len <= sLen; len++)      // 字符串长度从3开始的所有子字符串
        {
            for (int i = 0; i < sLen + 1 - len; i++)
            {
                int j = len - 1 + i;       // j为数组尾部的索引
                if (s[i] == s[j] && DP[i + 1, j - 1])
                {
                    DP[i, j] = true;      // i到j为回文
                    lonBeg = i;           // lonBeg为起始索引，等于i
                    maxLen = len;      // maxLen为字符串长度
                }
            }
        }
        return s.Substring(lonBeg, maxLen);
    }
}
```

然而，继续悲剧……

```
Submission Result: Memory Limit Exceeded
```

```
public class Solution
{
    public string LongestPalindrome(string s)
    {
        int nLen = s.Length;
        if (nLen == 0) return "";
        string lonStr = s.Substring(0, 1);
        for (int i = 0; i < nLen - 1; i++)
        {
            string p1 = ExpandAroundCenter(s, i, i);
            if (p1.Length > lonStr.Length)
                lonStr = p1;
            string p2 = ExpandAroundCenter(s, i, i + 1);
            if (p2.Length > lonStr.Length)
                lonStr = p2;
        }
        return lonStr;
    }
    public static string ExpandAroundCenter(string s, int n, int m)
    {
        int l = n, r = m;
        int nLen = s.Length;
        while (l >= 0 && r <= nLen - 1 && s[l] == s[r])
        {
            l--;
            r++;
        }
        return s.Substring(l + 1, r - l - 1);
    }
}
```
好吧，这种方法来源于网络……据说要$O(n^2)$的时间，但仅要$O(1)$的空间！

哎，继续努力了！
