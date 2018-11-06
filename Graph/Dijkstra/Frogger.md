```c
// 队列清空！

#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <set>
using namespace std;

int n;

struct Node{
	double x;
	double y;
};
Node node[210];

struct Edge{
	int index;
	double len;
	Edge(int _index, double _len){
		index = _index;
		len = _len;
	}
	bool const operator < (Edge _edge) const{
		return len > _edge.len;
	}
};

double distance(int index1, int index2){
	return sqrt(pow(node[index2].x-node[index1].x, 2) + pow(node[index2].y-node[index1].y, 2));
}

double max_num (double a, double b){
	if (a > b)
		return a;
	return b;
}

int vis[210];
double dis[210];
double map[210][210];
priority_queue<Edge> qu;

void dijsktra(){
	vis[0] = 1;
	for (int i = 1; i < n; i++){
		dis[i] = map[0][i];
		qu.push(Edge(i, dis[i]));
	}
	while(!qu.empty()){
		Edge temp = qu.top();
		qu.pop();
		if (temp.index == 1)
			return;
		if (vis[temp.index] == 0){
			vis[temp.index] = 1; 
			for (int i = 0; i < n; i++){
				if (vis[i] == 0){
					double max_dis = max_num(map[i][temp.index], dis[temp.index]);
					if (dis[i] > max_dis)
						dis[i] = max_dis;
					//qu.push(Edge(i, map[i][temp.index]));
				    qu.push(Edge(i, dis[i]));
				}
			}
		}
	}
}

int main(){
	int sum = 0;
	while(cin >> n){
		if (n == 0)
			break;
		sum++;
		memset(vis, 0, sizeof(vis));
		while (!qu.empty())
			qu.pop();
		for (int i = 0; i < n; i++){
			cin >> node[i].x >> node[i].y;
			if (i == 0)
				dis[i] = 0;
			else
				dis[i] = 100010;
		}
		for (int i = 0; i < n; i++){
			for (int j = 0; j < n; j++){
				if (i == j)
					map[i][j] = 0;
				else{
					double temp = distance(i, j);
					map[i][j] = temp;
					map[j][i] = temp;
				}
			}
		}
		dijsktra();
		cout << "Scenario #" << sum << endl;
		cout << fixed;
		cout << "Frog Distance = " << setprecision(3) << dis[1] << endl;
		cout << endl;
	}
    return 0;
}
```
