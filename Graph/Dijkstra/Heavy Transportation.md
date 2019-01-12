```c
// 注意w[i]的初始化 为0 还是 为maxnum

#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <set>
using namespace std;

int sum;
int n, m;
int vis[1010];
int map[1010][1010];
int w[1010];

struct Node{
	int index;
	int weight;
	bool const operator < (Node _n) const{
		return weight < _n.weight;
	}
	Node(int _index, int _weight){
		index = _index;
		weight = _weight;
	}
};

priority_queue<Node> qu;

void dijkstra(){
	vis[0] = 1;
	for (int i = 1; i < n; i++){
		if (map[0][i] != 1000010){
			w[i] = map[0][i];
			qu.push(Node(i, w[i]));
		}
	}
	while(!qu.empty()){
		Node temp = qu.top();
		qu.pop();
		if (temp.index == n-1) return;
		if (vis[temp.index] == 0){
			vis[temp.index] = 1;
			for (int i = 0; i < n; i++){
				if (vis[i] == 0 && map[temp.index][i] != 1000010){
					int min_w = map[temp.index][i] < w[temp.index] ? map[temp.index][i] : w[temp.index];
					if (w[i] < min_w)
						w[i] = min_w;
					qu.push(Node(i, w[i]));
				}
			}
		}
	}
}

int main(){
	cin >> sum;
	for (int k = 1; k <= sum; k++){
		cin >> n >> m;
		while(!qu.empty())
			qu.pop();
		memset(vis, 0, sizeof(vis));
		memset(w, 0, sizeof(w));
		for (int i = 0; i < n; i++){
			for (int j = 0; j < n; j++){
				if (i == j) map[i][j] = 0;
				else{
					map[i][j] = 1000010;
					map[j][i] = 1000010;
				}
			}
		}
		for (int i = 0; i < m; i++){
			int a, b, weight;
			cin >> a >> b >> weight;
			if (weight < map[a-1][b-1]){
				map[a-1][b-1] = weight;
				map[b-1][a-1] = weight;
			}
		}
		dijkstra();
		cout << "Scenario #" << k << ":" << endl;
		cout << w[n-1] << endl;
		cout << endl;
	}
    return 0;
}
```

```c
#include <iostream>
#include <iomanip>
#include <string>
#include <algorithm>
#include <string.h>
#include <cmath>
#include <cstring>
#include <stack>
#include <map>
using namespace std;

#define INF 0x3f3f3f3f

int n, m, k, dis[1010][1010], vis[1010], d[1010];

int main(){
	cin >> k;
	for (int j = 1; j <= k; j++){
		memset(vis, 0, sizeof(vis));
		memset(dis, -1, sizeof(dis));
		memset(d, -1, sizeof(d));
		cin >> n >> m;
		while(m--){
			int a, b, c;
			cin >> a >> b >> c;
			dis[a-1][b-1] = c;
			dis[b-1][a-1] = dis[a-1][b-1];
		}
		d[0] = INF;
		int t = n;
		while(t--){
			int min_num = -1;
			int idx = -1;
			for (int i = 0; i < n; i++){
				if (d[i] > min_num && vis[i] == 0){
					min_num = d[i];
					idx = i;
				}
			}
			if (idx == -1) break;
			vis[idx] = 1;
			for (int i = 0; i < n; i++){
				if (dis[idx][i] != -1 && vis[i] == 0){
					d[i] = max(d[i], min(d[idx], dis[idx][i]));
				}
			}
		}
		cout << "Scenario #" << j << ":" << endl;
		cout << d[n-1] << endl;
		cout << endl;
	}
	return 0;
}
```
