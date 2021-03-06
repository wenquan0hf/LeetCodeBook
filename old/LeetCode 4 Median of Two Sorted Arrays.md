翻译

```
有两个给定的排好序的数组nums1和nums2，其大小分别为m和n。
找出这两个已排序数组的中位数。
总运行时间的复杂度应该是O(log(m+n))。
```

原文

```
There are two sorted arrays nums1 and nums2 of size m and n respectively.
Find the median of the two sorted arrays. 
The overall run time complexity should be O(log (m+n)).
```

C#

```
public class Solution {
    public double FindMedianSortedArrays(int[] nums1, int[] nums2) {
		int len1=nums1.Length;
		int len2=nums2.Length;
		bool isEven=(nums1.Length+nums2.Length)%2==0;
		
		int left=(len1+len2+1)/2;
		int right=(len1+len2+2)/2;
		
		if (isEven)
        {
            var leftValue = findKth(nums1, 0, len1 - 1, nums2, 0, len2 - 1, left);
            var rightValue = findKth(nums1, 0, len1 - 1, nums2, 0, len2 - 1, right);
            return (leftValue + rightValue) / 2.0;
        }
        else
        {
            return findKth(nums1, 0, len1 - 1, nums2, 0, len2 - 1, right);
        }
    }
	public double findKth(int[] A,int lowA,int highA,int[] B,int lowB,int highB,int k)
	{
		if(lowA>highA)
		{
			return B[lowB+k-1];
		}
		if(lowB>highB)
		{
			return A[lowA+k-1];
		}
		int midA=(lowA+highA)/2;
		int midB=(lowB+highB)/2;
		if (A[midA] <= B[midB])
        {
            return k <= midA - lowA + midB - lowB + 1 ?
		        this.findKth(A, lowA, highA, B, lowB, midB - 1, k) :
				this.findKth(A, midA + 1, highA, B, lowB, highB, k - (midA - lowA + 1));
        }
        else
        {
            return k <= midA - lowA + midB - lowB + 1 ?
				this.findKth(A, lowA, midA - 1, B, lowB, highB, k) : 
				this.findKth(A, lowA, highA, B, midB + 1, highB, k - (midB - lowB + 1));
		}
	}
}
```