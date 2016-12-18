#Remove Duplicates from Sorted Array II
###题目
Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = [1,1,1,2,2,3],Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.


接着Remove Duplicates的题目，如果允许每个元素最多重复一次，请输出去重后的数组，返回数组的长度。

比如，给定[1,1,1,2,2,3]，应当返回新数组的长度5，原数组的前5位应当是[1, 1, 2, 2, 3]

###思路1
计数：遍历数组，统计当前的数出现的次数，如果超过2次，则不计入新数组；否则计入新数组

```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size() == 0)
            return 0;
        int k = 1, cnt = 1;
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] == nums[i - 1]) cnt++;
            else cnt = 1;
            if (cnt <= 2) nums[k++] = nums[i];
        }
        return k;
    }
};
```


###思路2
遍历数组，比较数组当前的数nums[i]，和新数组的倒数第二位是否相等：如果相等，则跳过当前的数，否则计入新数组

```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (k < 2 || nums[i] > nums[k - 2])
                nums[k++] = nums[i];
        }
        return k;
    }
};
```
注意每次都要和新数组的数比较也就是`nums[i] > nums[k - 2]`而不是`nums[i] > nums[i - 2]`。因为遍历到nums的第i位时，nums[i - 2]位可能已经被nums[i - 1]位覆盖了

比如[1, 1 ,1, 2, 2, 3]中，访问到第二个2时,我们应该把这个2加入到新数组中。但是i = 4，nums[2] = 2（其实是被nums[3]覆盖成了2），nums[i] > nums[i - 2]不成立。
