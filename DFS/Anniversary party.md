```c
#include <iostream>
#include <iomanip>
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <string.h>
#include <assert.h>
#include <queue>
#include <vector>
#include <math.h>
#include <algorithm>
#include <set>
using namespace std;

int n, vis[6010];

struct Node{
	int rate;
	vector<int> child;
};

Node node[6010];

int cal_sum(int idx){
	if (vis[idx] != -1)
		return vis[idx];
	if (node[idx].child.size() == 0){
		return node[idx].rate;
	}
	int temp = 0;
	for (int i = 0; i < node[idx].child.size(); i++){
		temp += cal_sum(node[idx].child[i]);
	}
	int temp2 = node[idx].rate;
	for (int i = 0; i < node[idx].child.size(); i++){
		int k = node[idx].child[i];
		for (int j = 0; j < node[k].child.size(); j++){
			int m = node[k].child[j];
			temp2 += cal_sum(m);
		}
	}
	vis[idx] = max(temp, temp2);
	return vis[idx];
}

int main() {
	cin >> n;
	memset(vis, 0, sizeof(vis));
	for (int i = 1; i <= n; i++)
		cin >> node[i].rate;
	for (int i = 0; i < n-1; i++){
		int a, b;
		cin >> a >> b;
		vis[a] = 1;
		node[b].child.push_back(a);
	}
	int root = -1;
	for (int i = 1; i <= n; i++){
		if (vis[i] == 0){
			root = i;
			break;
		}
	}
	memset(vis, -1, sizeof(vis));
	cout << cal_sum(root) << endl;
	return 0;
}
```
