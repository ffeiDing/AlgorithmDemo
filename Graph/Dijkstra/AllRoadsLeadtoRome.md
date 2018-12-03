```c
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

#define INF 1e9

int n, k, e;
int happy[210], vis[210], d[210], sum_happy[210], num[210];
int len[210][210];
vector<int> pre[210];
vector<int> path, temppath;
map<string, int> t1;
map<int, string> t2;
int sum = INF;

void dfs(int node){
	temppath.push_back(node);
	if (node == 0){
		if (temppath.size() < sum){
			sum = temppath.size();
			path = temppath;
		}
		temppath.pop_back();
		return;
	}
	for (int i = 0; i < pre[node].size(); i++)
		dfs(pre[node][i]);
	temppath.pop_back();
}

int main(){
	scanf("%d%d", &n, &k);
	char str[3];
	string s;
	scanf("%s", str);
	s = str;
	t1[s] = 0;
	t2[0] = s;
	fill(len[0], len[0]+210*210, INF);
	memset(happy, 0, sizeof(happy));
	memset(sum_happy, 0, sizeof(sum_happy));
	memset(num, 0, sizeof(num));
	for (int i = 1; i < n; i++){
		scanf("%s", str);
		s = str;
		if (s == "ROM")
			e = i;
		t1[s] = i;
		t2[i] = s;
		scanf("%d", &happy[i]);
	}
	for (int i = 0; i < k; i++){
		int a, b;
		cin >> s;
		a = t1[s];
		cin >> s;
		b = t1[s];
		cin >> len[a][b];
		len[b][a] = len[a][b];
	}
	memset(vis, 0, sizeof(vis));
	fill(d, d+210, INF);
	int h = n;
	d[0] = 0;
	num[0] = 1;
	while(h--){
		int now = -1;
		int minnum = INF;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && d[i] < minnum){
				minnum = d[i];
				now = i;
			}
		}
		if (now == -1) break;
		vis[now] = 1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 0 && len[now][i] != INF){
				if (d[now] + len[now][i] < d[i]){
					d[i] = d[now] + len[now][i];
					num[i] = num[now];
					sum_happy[i] = sum_happy[now] + happy[i];
					pre[i].clear();
					pre[i].push_back(now);
				}
				else if (d[now] + len[now][i] == d[i]){
					num[i] += num[now];
					if (sum_happy[i] < sum_happy[now] + happy[i]){
						sum_happy[i] = sum_happy[now] + happy[i];
						pre[i].clear();
						pre[i].push_back(now);
					}
					else if (sum_happy[i] == sum_happy[now] + happy[i]){
						pre[i].push_back(now);
					}
				}
			}
		}
	}
	printf("%d %d %d ", num[e], d[e], sum_happy[e]);
	dfs(e);
	printf("%d\n", sum_happy[e]/(sum-1));
	for (int i = path.size()-1; i > 0; i--)
		cout << t2[path[i]] << "->";
	cout << t2[path[0]] << endl;
    return 0;
}
```
