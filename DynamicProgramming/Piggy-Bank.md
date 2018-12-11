```c
// 完全背包 不同的是求最小值，注意初始化条件
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
#include <map>
using namespace std;

#define INF 0x3f3f3f3f

int t, empty, full, n, weight;
int w[510], v[510], sum[10010];

int main(){
	scanf("%d", &t);
	while(t--){
		scanf("%d%d", &empty, &full);
		weight = full - empty;
		scanf("%d", &n);
		for (int i = 0; i < n; i++)
			scanf("%d%d", &v[i], &w[i]);
		fill(sum, sum+10010, INF);
		sum[0] = 0;
		for (int i = 0; i < n; i++){
			for (int j = w[i]; j <= weight; j++){
				sum[j] = min(sum[j], sum[j-w[i]]+v[i]);
			}
		}
		if (sum[weight] != INF)
			printf("The minimum amount of money in the piggy-bank is %d.\n", sum[weight]);
		else
			printf("This is impossible.\n");
	}
    return 0;
}
```
