```c
#include <iostream>
#include <iomanip>
#include <cstring>
#include <algorithm>
#include <vector>
#include <queue>
using namespace std;

int n, vis[10010];
long long sum;
struct Node{
	int val;
	int day;
};
Node node[10010];

bool cmp(Node a, Node b){
	if (a.val == b.val) return a.day < b.day;
	return a.val > b.val;
}

int main(){
	cin >> n;
	sum = 0;
	memset(vis, 0, sizeof(vis));
	for (int i = 0; i < n; i++)
		cin >> node[i].val >> node[i].day;
	sort(node, node+n, cmp);
	for (int i = 0; i < n; i++){
		for (int j = node[i].day; j >= 1; j--){
			if (vis[j] == 0){
				//cout << j << endl;
				vis[j] = 1;
				sum += node[i].val;
				break;
			}
		}
	}
	cout << sum << endl;
	return 0;
}
```
