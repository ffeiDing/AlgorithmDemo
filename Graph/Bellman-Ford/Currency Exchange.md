```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <map>
#include <cstring>
using namespace std;

struct Edge{
	int u, v;
	double w, c;
};

int n, m, start;
double sum, d[110];
Edge e[300];

int main(){
	cin >> n >> m >> start >> sum;
	memset(d, 0, sizeof(d));
	for (int i = 0; i < m; i++){
		int a, b;
		double r1, r2, c1, c2;
		cin >> a >> b >> r1 >> c1 >> r2 >> c2;
		e[i].u = a;
		e[i].v = b;
		e[i].w = r1;
		e[i].c = c1;
		e[i+m].u = b;
		e[i+m].v = a;
		e[i+m].w = r2;
		e[i+m].c = c2;
	}
	d[start] = sum;
	int flag = 0;
	for (int i = 0; i < n-1; i++){
		for (int j = 0; j < 2*m; j++){
			if ((d[e[j].u]-e[j].c)*e[j].w > d[e[j].v])
				d[e[j].v] = (d[e[j].u]-e[j].c)*e[j].w;
		}
	}
	for (int j = 0; j < 2*m; j++){
		if ((d[e[j].u]-e[j].c)*e[j].w > d[e[j].v]){
			flag = 1;
			break;
		}
	}
	if (flag == 1)
		cout << "YES" << endl;
	else
		cout << "NO" << endl;
	return 0;
}
```
