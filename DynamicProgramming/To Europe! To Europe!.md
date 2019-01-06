```c
#include <iostream>
#include <iomanip>
#include <algorithm>
#include <cmath>
#include <cstring>
using namespace std;

#define INF 0x3f3f3f3f
int b, n;
double l;

struct Node {
	int w;
	double v;
};
Node node[1100];
int load[1100], rate[1100];
double cost[1100];

int main() {
	while (cin >> b >> l >> n) {
		double sum = 0;
		if (b == 0 && l == 0 && n == 0) break;
		memset(cost, 0, sizeof(cost));
		for (int i = 1; i <= n; i++) {
			cin >> node[i].w >> node[i].v;
		}
		for (int i = 1; i <= n; i++) {
			load[i] = node[i].w;
			cost[i] = l / node[i].v + cost[i - 1];
			rate[i] = node[i].v;
			int load_temp = load[i];
			double cost_temp = cost[i];
			double rate_temp = rate[i];
			for (int j = i - 1; j >= 1; j--) {
				if (load[i] + node[j].w > b) break;
				double m;
				if (rate[i] < node[j].v)
					m = rate[i];
				else
					m = node[j].v;
				double temp = l /m + cost[j - 1];
				//cout << temp << endl;
				cost[i] = temp;
				rate[i] = m;
				load[i] += node[j].w;
				if (temp <= cost_temp) {
					cost_temp = temp;
					rate_temp = m;
					load_temp += node[j].w;
				}
			}
			load[i] = load_temp;
			rate[i] = rate_temp;
			cost[i] = cost_temp;
			//cout << i << " " << load[i] << " " << cost[i] << " " << rate[i] << endl;
		}
		cout << fixed << setprecision(1) << cost[n] * 60 << endl;
	}
	return 0;
}
```
