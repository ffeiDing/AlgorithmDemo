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

int node[10010], vis[10010];

int find_root(int a){
	if (node[a] == 0) return a;
	int temp = find_root(node[a]);
	node[a] = temp;
	return temp;
}

int main(){
	int a, b;
	int cnt = 1;
	memset(node, 0, sizeof(node));
	memset(vis, 0, sizeof(vis));
	int flag = 0;
	while(cin >> a >> b){
		if (a == -1 && b == -1) break;
		if (a == 0 && b == 0){
			if (flag == 0){
				int sum = 0;
				for (int i = 0; i < 10010; i++){
					if (vis[i] == 1 && node[i] == 0)
						sum++;
				}
				if (sum == 0 || sum == 1)
					cout << "Case " << cnt << " is a tree." << endl;
				else
					cout << "Case " << cnt << " is not a tree." << endl;
			}
			else
				cout << "Case " << cnt << " is not a tree." << endl;
			flag = 0;
			cnt++;
			memset(node, 0, sizeof(node));
			memset(vis, 0, sizeof(vis));
			continue;
		}
		vis[a] = 1;
		vis[b] = 1;
		if (flag == 0){
			int root_a = find_root(a);
			int root_b = find_root(b);
			if (root_a == root_b || root_b != b){
				flag = 1;
			}
			else{
				node[root_b] = root_a;
			}
		}
	}
	return 0;
}
```
