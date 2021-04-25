### LeetCode每日一题——删除有序数组中的重复项

> https://leetcode-cn.com/problems/remove-element/

```
class Solution
{
public:
    int removeElement(vector<int> &nums, int val)
    {
        int len = nums.size();
        if(len == 0) return 0;//特判，如果nums中没有元素，返回0
        if(len == 1) return nums[0] == val ? 0 : 1; //特判，如果nums中的元素只有一个，那就直接判断需不需去重
        int index = 0;//去重后数组的长度
        for(int i = 0; i < len; i++){
            if(nums[i] != val){
                nums[index++] = nums[i];//当不等于val的时候，让下标的数等于那个数并更新
                
            }
        }
        return index;
    }
};
```

