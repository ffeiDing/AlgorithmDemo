```c
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int len = nums.size();
        int sum[len], minsum[len];
        sum[0] = nums[0];
        minsum[0] = nums[0];
        for (int i = 1; i < len; i++){
            sum[i] = max(nums[i], sum[i-1]*nums[i]);
            sum[i] = max(sum[i], minsum[i-1]*nums[i]);
            minsum[i] = min(nums[i], sum[i-1]*nums[i]);
            minsum[i] = min(minsum[i], minsum[i-1]*nums[i]);
        }
        int maxres = -1000010;
        for (int i = 0; i < len; i++){
            maxres = max(maxres, sum[i]);
        }
        return maxres;
    }
};
```
