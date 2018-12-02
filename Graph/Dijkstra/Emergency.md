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

#define INF 1000010

int n, m, c1, c2;
int len[510][510];
int num[510];
int d[510], sum[510], diff[510];
int vis[510];

int main(){
	scanf("%d %d %d %d\n", &n, &m, &c1, &c2);
	memset(vis, 0, sizeof(vis));
	memset(sum, 0, sizeof(sum));
	memset(diff, 0, sizeof(diff));
	fill(len[0], len[0]+510*510, INF);
	fill(d, d+510, INF);
	for (int i = 0; i < n; i++)
		scanf("%d", &num[i]);
	for (int i = 0; i < m; i++){
		int a, b;
		scanf("%d %d", &a, &b);
		scanf("%d", &len[a][b]);
		len[b][a] = len[a][b];
	}
	getchar();
	d[c1] = 0;
	sum[c1] = num[c1];
	diff[c1] = 1;
	int h = n;
	while(h--){
		int minnum = INF;
		int now = -1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && d[i] != INF){
				if (d[i] < minnum){
					now = i;
					minnum = d[i];
				}
			}
		}
		if (now == -1) break;
		vis[now] = 1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && len[now][i] != INF){
				if (d[now] + len[now][i] < d[i]){
					d[i] = d[now] + len[now][i];
					sum[i] = sum[now] + num[i];
					diff[i] = diff[now];
				}
				else if (d[now] + len[now][i] == d[i]){
					sum[i] = max(sum[now] + num[i], sum[i]);
					diff[i] += diff[now];
				}
			}
		}
	}
	printf("%d %d\n", diff[c2], sum[c2]);
    return 0;
}
```
