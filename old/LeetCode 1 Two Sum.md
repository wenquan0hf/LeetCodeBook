翻译：

```
给定一个整型数组，找出能相加起来等于一个特定目标数字的两个数。

函数twoSum返回这两个相加起来等于目标值的数字的索引，且index1必须小于index2。
请记住你返回的答案（包括index1和index2）都不是从0开始的。

你可以假定每个输入都有且仅有一个解决方案。

输入: numbers={2, 7, 11, 15}, target=9
输出: index1=1, index2=2
```
原文：

```
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target,
where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

C++

```
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		map<int, int> mapping;
		vector<int> result;
		for (int i = 0; i < nums.size(); i++)
		{
			mapping[nums[i]] = i;
		}
		for (int i = 0; i < nums.size(); i++)
		{
			int searched = target - nums[i];
			if (mapping.find(searched) != mapping.end()
				&& mapping.at(searched) != i)
			{
				result.push_back(i + 1);
				result.push_back(mapping[searched] + 1);
				break;
			}
		}
		return result;	   
	}
};
```

Java

```
public class Solution {
	public int[] twoSum(int[] nums, int target) {
		HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
		int[] result=new int[2];
		for(int i=0;i<nums.length;i++){
			map.put(nums[i], i);
		}		
		for(int i=0;i<nums.length;i++){
			int searched=target-nums[i];
			if(map.containsKey(searched)&&map.get(searched)!=i){
				int index=map.get(searched);
				if(index<i){
					result[0]=map.get(searched)+1;
					result[1]=i+1;
				}else{
					result[0]=i+1;
					result[1]=map.get(searched)+1;
				}			
			}
		}
		return result;                
    }
}
```

C#（超时）

```
public static int[] TwoSum(int[] nums, int target)
{
    Dictionary<int, int> map = new Dictionary<int, int>();
    int[] result = new int[2];
    for (int i = 0; i < nums.Length; i++)
    {
        map.Add(i, nums[i]);
    }
    for (int i = 0; i < nums.Length; i++)
    {
        if (nums[i] > target)
            continue;
        int searched = target - nums[i];
        if (map.ContainsValue(searched))
        {
            int index = map.Where(x => x.Value == searched).Select(x => x.Key).FirstOrDefault();
            if (index != i)
            {
                if (index < i)
                {
                    result[0] = index + 1;
                    result[1] = i + 1;
                }
                else
                {
                    result[0] = i + 1;
                    result[1] = index + 1;
                }
            }
        }
    }
    return result;
}
```