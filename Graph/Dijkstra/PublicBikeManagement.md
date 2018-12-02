```c
//Dijkstra + DFS
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

int c, n, sp, m;
int num[510];
int d[510], vis[510];
int len[510][510];
int min_front = INF;
int min_back = INF;
vector<int> pre[510];
vector<int> temppath, path;

void dfs(int node){
	temppath.push_back(node);
	if (node == 0){
		int front = 0;
		int back = 0;
		for (int i = temppath.size()-1; i >= 0; i--){
			int id = temppath[i];
			if (c/2 > num[id]){
				if (back > c/2 - num[id])
					back -= c/2 - num[id];
				else{
					front += c/2 - num[id] - back;
					back = 0;
				}
			}
			else{
				back += num[id]-c/2;
			}
		}
		if (front < min_front){
			path = temppath;
			min_front = front;
			min_back = back;
		}
		else if (front == min_front){
			if (back < min_back){
				path = temppath;
				min_back = back;
			}
		}
		temppath.pop_back();
		return;
	}
	for (int i = 0; i < pre[node].size(); i++)
		dfs(pre[node][i]);
	temppath.pop_back();
}

int main(){
	scanf("%d %d %d %d\n", &c, &n, &sp, &m);
	memset(vis, 0, sizeof(vis));
	fill(len[0], len[0]+510*510, INF);
	fill(d, d+510, INF);
	for (int i = 1; i <= n; i++)
		scanf("%d", &num[i]);
	for (int i = 0; i < m; i++){
		int a, b;
		scanf("%d %d", &a, &b);
		scanf("%d", &len[a][b]);
		len[b][a] = len[a][b];
	}
	n++;
	int h = n;
	d[0] = 0;
	num[0] = c/2;
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
		if (now == -1)
			break;
		vis[now] = 1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && len[now][i] != INF){
				if (d[now] + len[now][i] < d[i]){
					d[i] = d[now] + len[now][i];
					pre[i].clear();
					pre[i].push_back(now);
				}
				else if (d[now] + len[now][i] == d[i])
					pre[i].push_back(now);
			}
		}
	}
	dfs(sp);
	printf("%d ", min_front);
	for (int i = path.size()-1; i > 0; i--){
		printf("%d->", path[i]);
	}
	printf("%d ", path[0]);
	printf("%d\n", min_back);
    return 0;
}

```
