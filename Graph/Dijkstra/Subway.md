```c
// 需要四舍五入
// cout << int(d[1]+0.5) << endl; AC
// cout << int(d[1]) << endl; WA
#include <iostream>
#include <iomanip>
#include <math.h>
#include <algorithm>
#include <string.h>
using namespace std;

# define INF 0x3f3f3f3f
int s_x, s_y, e_x, e_y;
int node_x[210], node_y[210];
double cost[210][210], d[210], vis[210];

double distance_walk(int x1, int y1, int x2, int y2) {
	double temp = pow(x1 - x2, 2) + pow(y1 - y2, 2);
	temp = sqrt(temp);
	return temp / 10000.0 * 60.0;
}

double distance_subway(int x1, int y1, int x2, int y2) {
	double temp = pow(x1 - x2, 2) + pow(y1 - y2, 2);
	temp = sqrt(temp);
	return temp / 40000.0 * 60.0;
}

int main() {
	fill(cost[0], cost[0] + 210 * 210, INF);
	fill(d, d + 210, INF);
	memset(vis, 0, sizeof(vis));
	cin >> s_x >> s_y >> e_x >> e_y;
	int x, y;
	int pre = 0;
	int cnt = 1;
	node_x[0] = s_x;
	node_y[0] = s_y;
	node_x[1] = e_x;
	node_y[1] = e_y;
	cost[0][1] = min(cost[0][1], distance_walk(e_x, e_y, s_x, s_y));
	cost[1][0] = cost[0][1];
	int flag = 0;
	while (cin >> x >> y) {
		if (x == -1 && y == -1) {
			flag = 0;
			pre = 0;
			continue;
		}
		cnt++;
		node_x[cnt] = x;
		node_y[cnt] = y;
		for (int i = 0; i < cnt; i++) {
			cost[i][cnt] = min(cost[i][cnt], distance_walk(node_x[i], node_y[i], node_x[cnt], node_y[cnt]));
			cost[cnt][i] = cost[i][cnt];
		}
		if (flag == 1) {
			cost[pre][cnt] = min(cost[pre][cnt], distance_subway(x, y, node_x[pre], node_y[pre]));
			cost[cnt][pre] = cost[pre][cnt];
		}
		flag = 1;
		pre = cnt;
	}
	d[0] = 0;
	int n = cnt + 1;
	int h = n;
	while (h--) {
		int now = -1;
		double minnum = INF;
		for (int i = 0; i < n; i++) {
			if (vis[i] == 0 && d[i] != INF) {
				if (d[i] < minnum) {
					minnum = d[i];
					now = i;
				}
			}
		}
		if (now == -1) break;
		vis[now] = 1;
		for (int i = 0; i < n; i++) {
			if (vis[i] == 0 && cost[now][i] != INF) {
				d[i] = min(d[i], d[now] + cost[now][i]);
			}
		}
	}
	cout << int(d[1]+0.5) << endl;
	//while (1);
	return 0;
}
```
