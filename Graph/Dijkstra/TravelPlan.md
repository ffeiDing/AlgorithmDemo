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

int n, m, s, e;
int len[510][510], cost[510][510];
int vis[510], d[510], c[510];
int pre[510];
vector<int> path;

int main(){
	scanf("%d %d %d %d", &n, &m, &s, &e);
	memset(vis, 0, sizeof(vis));
	fill(d, d+510, INF);
	fill(c, c+510, INF);
	fill(len[0], len[0]+510*510, INF);
	for (int i = 0; i < m; i++){
		int a, b;
		scanf("%d %d", &a, &b);
		scanf("%d %d", &len[a][b], &cost[a][b]);
		len[b][a] = len[a][b];
		cost[b][a] = cost[a][b];
	}
	int h = n;
	d[s] = 0;
	c[s] = 0;
	while(h--){
		int minnum = INF;
		int now = -1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && d[i] != INF){
				if (d[i] < minnum){
					minnum = d[i];
					now = i;
				}
			}
		}
		if (now == -1) break;
		vis[now] = 1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && len[now][i] != INF){
				if (d[now] + len[now][i] < d[i]){
					d[i] = d[now] + len[now][i];
					c[i] = c[now] + cost[now][i];
					pre[i] = now;
				}
				else if (d[now] + len[now][i] == d[i]){
					if (c[now] + cost[now][i] < c[i]){
						c[i] = c[now] + cost[now][i];
						pre[i] = now;
					}
				}
			}
		}
	}
	int index = e;
	while(1){
		if (index == s){
			path.push_back(s);
			break;
		}
		path.push_back(index);
		index = pre[index];
	}
	for (int i = path.size()-1; i >= 0; i--)
		printf("%d ", path[i]);
	printf("%d %d\n", d[e], c[e]);
    return 0;
}
```
