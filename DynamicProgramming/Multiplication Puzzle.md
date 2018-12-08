```c
// WA的原因是INF设置的太小了
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
#include <map>
using namespace std;

int n;
int num[110], dp[110][110];

int main(){
	scanf("%d", &n);
	num[0] = 1;
	num[n+1] = 1;
	fill(dp[0], dp[0]+110*110, 0x3f3f3f3f);
	for (int i = 1; i <= n; i++){
		scanf("%d", &num[i]);
	}
	for (int h = 0; h <= n; h++){
		for (int i = 1; i <= n; i++){
			int j = i+h;
			if (j > n) break;
			for (int k = i; k <= j; k++){
				int temp = 0;
				if (i-1 >= 1 && j+1 <= n){
					temp += num[i-1]*num[k]*num[j+1];
					if (k-1 >= i)
						temp+=dp[i][k-1];
					if (k+1 <= j)
						temp+=dp[k+1][j];
					dp[i][j] = min(dp[i][j], temp);
				}
			}
		}
	}
	printf("%d\n", dp[2][n-1]);
    return 0;
}
```
```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
#include <map>
using namespace std;

#define INF 0x3f3f3f3f

int n;
long long num[110];
long long dp[110][110];


int main(){
	scanf("%d", &n);
	num[0] = 1;
	num[n+1] = 1;
	fill(dp[0], dp[0]+110*110, INF);
	for (int i = 1; i <= n; i++)
		dp[i][i+1] = 0;
	for (int i = 1; i <= n; i++)
		scanf("%lld", &num[i]);
	for (int h = 2; h < n; h++){
		for (int i = 1; i + h <= n; i++){
			int j = i + h;
			for (int k = i+1; k < j; k++)
				dp[i][j] = min(dp[i][j], num[i]*num[k]*num[j]+dp[i][k]+dp[k][j]);
		}
	}
	printf("%lld\n", dp[1][n]);
    return 0;
}
```
