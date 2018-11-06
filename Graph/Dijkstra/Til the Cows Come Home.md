```c
// 要注意有重边，因此需要对输入数据加以判断，保存较短的边
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <set>
using namespace std;

struct Node{
	int des;
	int len;
	Node(int _des, int _len){
		des = _des;
		len = _len;
	}
	Node(){
	}
	bool const operator < (Node n) const{
		return len > n.len;
	}
};


int t, n;
int dis[1010][1010];
int vis[1010];
priority_queue<Node> qu;

void dijkstra(){
	Node temp;
	while(!qu.empty()){
		temp = qu.top();
		int des = temp.des;
		qu.pop();
		if (vis[des] == 0){
			vis[des] = 1;
			for (int i = 0; i < n; i++){
				if (dis[des][i] != 1001000 && vis[i] == 0){
					if (dis[0][des] + dis[des][i] < dis[0][i]){
						dis[0][i] = dis[0][des] + dis[des][i];
						qu.push(Node(i, dis[0][i]));
					}
				}
			}
		}
	}
}


int main(){
	cin >> t >> n;
	memset(dis, 0, sizeof(dis));
	memset(vis, 0, sizeof(vis));
	for (int i = 0; i < n; i++){
		for (int j = 0; j < n; j++){
			if (i != j)
				dis[i][j] = 1001000;
		}
	}
	for (int i = 0; i < t; i++){
		int a, b, len;
		cin >> a >> b >> len;
		if (len < dis[a-1][b-1]){
			dis[a-1][b-1] = len;
			dis[b-1][a-1] = len;
		}
	}
	vis[0] = 1;
	for (int i = 1; i < n; i++){
		if (dis[0][i] != 1001000){
			qu.push(Node(i, dis[0][i]));
		}
	}
	dijkstra();
	cout << dis[0][n-1] << endl;
    return 0;
}
```
