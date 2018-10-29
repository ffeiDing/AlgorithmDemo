```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
using namespace std;

int b[1010], re[1010];
int flag;

int root(int x){
	if (b[x] != 0){
		int temp = b[x];
		b[x] = root(b[x]);
		if (re[x] == re[temp])
			re[x] = 0;
		else
			re[x] = 1;
		return b[x];
	}
	else
		return x;
}


void combine(int x, int y, int k){
	int x_root = root(x);
	int y_root = root(y);
	if (x_root != y_root){
		b[x_root] = y_root;
		re[x_root] = re[x]==re[y]? k:(k+1)%2;
	}
	else{
		if ((re[x]-re[y]+2)%2 != k)
			flag = 1;
	}
	return;
}

int main(){
	int n, m;
	while(~scanf("%d%d", &n, &m)){
		memset(b, 0, sizeof(b));
		memset(re, 0, sizeof(re));
		flag = 0;
		while(m--){
			int x, y, k;
			scanf("%d%d%d", &x, &y, &k);
			if (flag == 0){
				combine(x+1, y+1, k);
				if (flag == 1)
					printf("NO\n");
			}
		}
		if (flag == 0)
			printf("YES\n");
	}
    return 0;
}
```
