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

int n, m, k, a[110][110], vis[110][110], num[110][110];

bool is_valid(int x, int y){
	if (x < 0 || x >= n) return false;
	if (y < 0 || y >= m) return false;
	return true;
}

int bfs(int x, int y){
	int temp = 0;
	vis[x][y] = 1;
	if (a[x][y] == 1)
		temp++;
	else
		return temp;
	if (is_valid(x-1, y) && vis[x-1][y] == 0){
		if (num[x-1][y] != -1){
			temp = num[x-1][y];
			return temp;
		}
		else
			temp += bfs(x-1, y);
	}
	if (is_valid(x+1, y) && vis[x+1][y] == 0){
		if (num[x+1][y] != -1){
			temp = num[x+1][y];
			return temp;
		}
		else
			temp += bfs(x+1, y);
	}
	if (is_valid(x, y+1) && vis[x][y+1] == 0){
		if (num[x][y+1] != -1){
			temp = num[x][y+1];
			return temp;
		}
		else
			temp += bfs(x, y+1);
	}
	if (is_valid(x, y-1) && vis[x][y-1] == 0){
		if (num[x][y-1] != -1){
			temp += num[x][y-1];
			return temp;
		}
		else
			temp += bfs(x, y-1);
	}
	num[x][y] = temp;
	return temp;
}

int main(){
	cin >> n >> m >> k;
	memset(vis, 0, sizeof(vis));
	memset(a, 0, sizeof(a));
	memset(num, -1, sizeof(num));
	for (int i = 0; i < k; i++){
		int x, y;
		cin >> x >> y;
		a[x-1][y-1] = 1;
	}
	int max_num = -1;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			if (a[i][j] == 1 && vis[i][j] == 0){
				num[i][j] = bfs(i, j);
				max_num = max(max_num, num[i][j]);
			}
		}
	}
	cout << max_num << endl;
	return 0;
}
```
