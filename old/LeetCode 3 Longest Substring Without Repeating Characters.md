翻译
```
 给定一个字符串，找出其没有重复字符的最大子序列的长度。
 例如，“abcabcbb”的无重复字符的最大子序列是“abc”，它的长度是3。
 “bbbbb”的最大子序列是“b”，它的长度是1。
```

原文

```
Given a string, find the length of the longest substring without repeating characters. 
For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3.
For "bbbbb" the longest substring is "b", with the length of 1.
```

Code 1（C++）

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int len = s.Length;
        int head = 0, index = 0, maxLen = 0;
        bool[] exist = new bool[256];
        for (int i = 0; i < exist.Length; i++)  
            exist[i] = false;  
        while (index < len){
            if (exist[s[index]]){
                 maxLen = Math.Max(maxLen, index - head);
                 while (s[head] != s[index]){
                     exist[s[head]] = false;
                     head++;
                 }
                 head++; index++;
             }
             else{
                 exist[s[index]] = true;
                 index++;
             }
         }
         maxLen = Math.Max(maxLen, len - head);
         return maxLen; 
    }
};
```

Code 1 C#

```
public class Solution
{
    public int LengthOfLongestSubstring(string s)
    {
        int len = s.Length;
        int head = 0, index = 0, maxLen = 0;
        bool[] exist = new bool[256];
        for (int i = 0; i < exist.Length; i++)
            exist[i] = false;
        while (index < len)
        {
            if (exist[s[index]])
            {
                maxLen = Math.Max(maxLen, index - head);
                while (s[head] != s[index])
                {
                    exist[s[head]] = false;
                    head++;
                }
                head++; index++;
            }
            else
            {
                exist[s[index]] = true;
                index++;
            }
        }
        maxLen = Math.Max(maxLen, len - head);
        return maxLen;
    }
}
```

Code 1 Java

```
public class Solution {
    public int lengthOfLongestSubstring(String s) {
    	int len=s.length();
    	int head=0,index=0,maxLen=0;
    	boolean[] exist=new boolean[256];
    	for(boolean e : exist)
    		e=false;
    	while(index<len){
    		if(exist[s.charAt(index)]){
    			maxLen=Math.max(maxLen, index-head);
    			while(s.charAt(head)!=s.charAt(index)){
    				exist[s.charAt(head)]=false;
    				head++;
    			}
    			head++; index++;
    		}
    		else{
    			exist[s.charAt(index)]=true;
    			index++;
    		}
    	}
    	return maxLen= Math.max(maxLen,len-head);
    }
}
```

Code 2 C++
```
static  int lengthOfLongestSubstring(string s)
{
    int ascii[256];
    for(int i=0; i<256; i++) ascii[i] = -1;
    int start = 0, ans = 0;
    int i;
    for(i=0; i<s.size(); i++){
       if( -1 != ascii[ s[i] ] ){
            if(ans < i-start) ans = i-start;
            for(int j=start; j<ascii[ s[i] ]; j++)
                 ascii[j] = -1;
            if(ascii[s[i]] + 1 > start )
                 start = ascii[s[i]] +1;
       }
       ascii[s[i]] = i;
    }
    if(ans < i-start) ans = i-start;
    return ans;
}
```

