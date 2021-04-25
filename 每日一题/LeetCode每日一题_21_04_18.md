### LeetCode每日一题——删除有序数组中的重复项

> https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/

```
class Solution{
public:
	int removeDuplicates(vector<int> &nums){
		int len = nums.size();
		if(len == 0) return {};//特判，当输入为空数组的时候返回null
		if(len == 1) return 1;//特判，当输入的数组中只有一个数的时候，不用去重，直接返回。
		int index = 0;//作为无重复数组的下标
		for(int i = 0; i < len; i++){
			if(nums[i] != nums[index]){//如果碰到nums[i]不等于nums[index]，也就是没有重复的情况，那就让index的下一个等于nums[i]，因为是有序的，所以递增检查即可。
				nums[++index] = nums[i];
			}
		}
		return index + 1;//index从0开始，按长度算，需要 + 1
	}
};
```

