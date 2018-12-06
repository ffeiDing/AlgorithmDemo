```c
//类似两次股票买卖，区别是一定要进行两次买卖
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

int t, n, num[50010], sum[50010];


int main(){
	scanf("%d", &t);
	while(t--){
		scanf("%d", &n);
		memset(num, 0, sizeof(num));
		memset(sum, 0, sizeof(sum));
		sum[0] = 0;
		int a = -100010;
		int b = -100010;
		for (int i = 1; i <= n; i++){
			scanf("%d", &num[i]);
			sum[i] = sum[i-1] + num[i];
			if (num[i] > a){
				b = a;
				a = num[i];
			}
			else{
				if (num[i] > b)
					b = num[i];
			}
		}
		int min_num = 0;
		int max_num = -100010;
		int fmax[50010];
		for (int i = 1; i <= n; i++){
			if (sum[i] < min_num)
				min_num = sum[i];
			max_num = max(max_num, sum[i] - min_num);
			fmax[i] = max_num;
		}
		min_num = sum[n];
		int bmax[50010];
		max_num = -100010;
		for (int i = n; i >= 1; i--){
			if (sum[i] > min_num)
				min_num = sum[i];
			max_num =  max(max_num, min_num - sum[i]);
			bmax[i] = max_num;
		}
		int maxsum = -100100;
		for (int i = 1; i <= n; i++){
			if (maxsum < fmax[i] + bmax[i])
				maxsum = fmax[i] + bmax[i];
		}
		if (maxsum == 0 && a < 0)
			maxsum = a+b;
		else if (maxsum == a)
			maxsum = a+b;
		printf("%d\n", maxsum);
	}
    return 0;
}
```
