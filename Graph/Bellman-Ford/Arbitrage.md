```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <map>
#include <cstring>
using namespace std;

struct Edge{
	int a;
	int b;
	double w;
};

int n, m, start;
double d[40];
map<string, int> m1;
Edge e[1000];

int ford(int num){
	memset(d, 0, sizeof(d));
	d[num] = 1;
	for (int i = 0; i < n-1; i++){
		for (int j = 0; j < m; j++){
			if (d[e[j].a]*e[j].w > d[e[j].b]){
				d[e[j].b] = d[e[j].a]*e[j].w;
			}
		}
	}
	for (int j = 0; j < m; j++){
		if (d[e[j].a]*e[j].w > d[e[j].b])
			return 1;
	}
	return 0;
}

int main(){
	int sum = 0;
	while(cin >> n){
		sum++;
		if (n == 0) break;
		for (int i = 0; i < n; i++){
			string s;
			cin >> s;
			m1[s] = i;
		}
		cin >> m;
		for (int i = 0; i < m; i++){
			string s1, s2;
			double v;
			cin >> s1 >> v >> s2;
			e[i].a = m1[s1];
			e[i].b = m1[s2];
			e[i].w = v;
		}
		int flag = 0;
		for (int k = 0; k < n; k++){
			if (ford(k) == 1){
				flag = 1;
				break;
			}
		}
		if (flag == 0)
			cout << "Case " << sum << ": No" << endl;
		else
			cout << "Case " << sum << ": Yes" << endl;
	}
	return 0;
}
```


```c
\\一定要形成环
#include <iostream>
#include <iomanip>
#include <cmath>
#include <map>
#include <cstring>
using namespace std;

struct Edge{
	int a;
	int b;
	double w;
};

int n, m, start;
double d[40];
map<string, int> m1;
Edge e[1000];

int ford(int num){
	memset(d, 0, sizeof(d));
	d[num] = 1;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			if (d[e[j].a]*e[j].w > d[e[j].b]){
				d[e[j].b] = d[e[j].a]*e[j].w;
			}
		}
	}
	if (d[num] > 1)
		return 1;
	return 0;
}

int main(){
	int sum = 0;
	while(cin >> n){
		sum++;
		if (n == 0) break;
		for (int i = 0; i < n; i++){
			string s;
			cin >> s;
			m1[s] = i;
		}
		cin >> m;
		for (int i = 0; i < m; i++){
			string s1, s2;
			double v;
			cin >> s1 >> v >> s2;
			e[i].a = m1[s1];
			e[i].b = m1[s2];
			e[i].w = v;
		}
		int flag = 0;
		for (int k = 0; k < n; k++){
			if (ford(k) == 1){
				flag = 1;
				break;
			}
		}
		if (flag == 0)
			cout << "Case " << sum << ": No" << endl;
		else
			cout << "Case " << sum << ": Yes" << endl;
	}
	return 0;
}
```
