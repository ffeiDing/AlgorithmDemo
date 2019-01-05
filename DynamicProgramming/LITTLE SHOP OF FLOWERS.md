```c
#include <iostream>
#include <iomanip>
#include <queue>
#include <vector>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;

int n, m;
int sum[110][110];

int main(){
	cin >> n >> m;
	memset(sum, 0, sizeof(sum));
	for (int i = 1; i <= n; i++){
		for (int j = 1; j <= m; j++){
			int temp;
			cin >> temp;
			if (j < i) continue;
			int max_num = -10000;
			for (int k = i-1; k<j; k++){
				max_num = max(max_num, sum[i-1][k]);
			}
			//cout << max_num << endl;
			sum[i][j] = max_num + temp;
			//cout << sum[i][j] << endl;
		}
		//cout << endl;
	}
	int res = -10000;
	for (int i = n; i <= m; i++)
		res = max(res, sum[n][i]);
	cout << res << endl;
	return 0;
}
```
