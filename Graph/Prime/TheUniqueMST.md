```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
using namespace std;

#define INF 100010

int t, n, m;
int len[110][110];
int d[110], vis[110], sum[110];
int res;

int main(){
	scanf("%d", &t);
	while(t--){
		res = 0;
		memset(vis, 0, sizeof(vis));
		memset(sum, 0, sizeof(sum));
		fill(len[0], len[0]+110*110, INF);
		fill(d, d+110, INF);
		scanf("%d %d", &n, &m);
		for (int i = 0; i < m; i++){
			int a, b;
			scanf("%d %d", &a, &b);
			scanf("%d", &len[a-1][b-1]);
			len[b-1][a-1] = len[a-1][b-1];
		}
		d[0] = 0;
		sum[0] = 1;
		int h = n;
		while(h--){
			int minnum = INF;
			int now = -1;
			for (int i = 0; i < n; i++){
				if (vis[i] == 0 && d[i] < INF){
					if (d[i] < minnum){
						minnum = d[i];
						now = i;
					}
				}
			}
			if (now == -1) break;
			vis[now] = 1;
			res += minnum;
			for (int i = 0; i < n; i++){
				if (vis[i] == 0 && len[now][i] != INF){
					if (len[now][i] < d[i]){
						d[i] = len[now][i];
						sum[i] = sum[now];
					}
					else if (len[now][i] == d[i]){
						sum[i] += sum[now];
					}
				}
			}
		}
		if (sum[n-1] > 1)
			printf("Not Unique!\n");
		else
			printf("%d\n", res);
	}
    return 0;
}
```
