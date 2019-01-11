```c
#include <iostream>
#include <iomanip>
#include <string>
#include <algorithm>
#include <string.h>
#include <cmath>
#include <cstring>
using namespace std;

int n, m, a[310], dis[310][310], sum[310][40];

int main(){
	cin >> n >> m;
	for (int i = 0; i < n; i++)
		cin >> a[i];
	memset(dis, 0, sizeof(dis));
	fill(sum[0], sum[0]+310*40, 0x3f3f3f3f);
	for (int i = 0; i < n; i++){
		for (int j = i; j < n; j++){
			int mid = a[(i+j)/2];
			for (int k = i; k <= j; k++){
				dis[i][j] += abs(a[k]-mid);
			}
		}
	}
	for (int i = 0; i < 310; i++)
		sum[i][0] = 0;
	for (int i = 0; i < 40; i++)
		sum[0][i] = 0;
	for (int i = 1; i <= n; i++){
		for (int j = 1; j <= m; j++){
			for (int k = 1; k <= i; k++){
				if (j == 1)
					sum[i][j] = min(sum[i][j], dis[0][i-1]);
				else
					sum[i][j] = min(sum[i][j], sum[k-1][j-1]+dis[k-1][i-1]);
				//cout << i << " " << j << " " <<k <<  " " << sum[i][j] << endl;
			}
		}
	}
	cout << sum[n][m] << endl;
}
```
