# House Robber I
```c
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        int sum[len+3];
        memset(sum, 0, sizeof(sum));
        sum[0] = 0;
        sum[1] = 0;
        for (int i = 2; i <= len+1; i++){
            sum[i] = sum[i-1];
            if (sum[i-1] < sum[i-2]+nums[i-2])
                sum[i] = sum[i-2]+nums[i-2];
        }
        return sum[len+1];
    }
};
```

# House Robber II
```c
// 环形
class Solution {
public:
    int rob(vector<int>& nums) {
        int len = nums.size();
        if (len == 0)
            return 0;
        if (len == 1)
            return nums[0];
        int b = nums[len-1];
        nums[len-1] = 0;
        int sum[len];
        sum[0] = nums[0];
        sum[1] = max(nums[0], nums[1]);
        for (int i = 2; i < len; i++){
            sum[i] = max(sum[i-1], sum[i-2]+nums[i]);
        }
        int res = max(sum[len-1], sum[len-2]);
        nums[len-1] = b;
        nums[0] = 0;
        sum[0] = nums[0];
        sum[1] = max(nums[0], nums[1]);
        for (int i = 2; i < len; i++){
            sum[i] = max(sum[i-1], sum[i-2]+nums[i]);
        }
        int res1 = max(sum[len-1], sum[len-2]);
        return max(res1, res);
    }
};
```
