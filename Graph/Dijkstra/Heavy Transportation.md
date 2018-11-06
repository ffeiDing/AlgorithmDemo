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
