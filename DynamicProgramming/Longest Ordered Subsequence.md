```c
#include <iostream>
#include <iomanip>
#include <queue>
#include <vector>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;

int n, a[1010], sum[1010];

int main(){
	cin >> n;
	fill(sum, sum+n, 1);
	for (int i = 0; i < n; i++)
		cin >> a[i];
	int max_sum = -1;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < i; j++){
			if (a[i] > a[j]){
				sum[i] = max(sum[i], sum[j]+1);
			}
		}
		max_sum = max(max_sum, sum[i]);
	}
	cout << max_sum << endl;
	return 0;
}
```
