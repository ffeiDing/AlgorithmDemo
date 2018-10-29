// 最小生成树 prim算法

```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
using namespace std;

struct Edge{
	int x;
	int y;
	int len;
};

struct cmp{
	bool operator()(Edge a, Edge b){
		return a.len > b.len;
	}
};

int n, map[110][110], vis[110], sum;
priority_queue<Edge, vector<Edge>, cmp> waiting_q;


bool vis_map(){
	for (int i = 0; i < n; i++){
		if (vis[i] == 0)
			return false;
	}
	return true;
}

void prim(){
	vis[0] = 1;
	for (int i = 1; i < n; i++){
		Edge e;
		e.x = 0;
		e.y = i;
		e.len = map[0][i];
		waiting_q.push(e);
	}
	while(vis_map() != true){
		Edge e = waiting_q.top();
		while(vis[e.y] == 1){
			waiting_q.pop();
			e = waiting_q.top();
		}
		//cout << e.len << endl;
		sum += e.len;
		vis[e.y] = 1;
		for (int i = 0; i < n; i++){
			if (vis[i] == 1)
				continue;
			else{
				Edge temp;
				temp.x = e.y;
				temp.y = i;
				temp.len = map[temp.x][temp.y];
				waiting_q.push(temp);
			}
		}
	}
	return;	
}

int main(){
	while(cin >> n){
		sum = 0;
		memset(map, 0, sizeof(map));
		memset(vis, 0, sizeof(vis));
		while(!waiting_q.empty())
			waiting_q.pop();
		for (int i = 0; i < n; i++){
			for (int j = 0; j < n; j++){
				cin >> map[i][j];
			}
		}
		prim();
		cout << sum << endl;
	}
    return 0;
}
```
