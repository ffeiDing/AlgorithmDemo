```c
// 每个点对应的圆心位置按x轴从小到大排序
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
using namespace std;

double x[1010], y[1010];
int n;
double d;
int num;

void display_circle(){
	int flag = 0;
	int i = 0;
	double x0;
	while(i < n){
		if (flag == 0){
			flag = 1;
			x0 = x[i];
			num++;
			i++;
		}
		else{
			if (x[i]-x0 <= 2*y[i])
				i++;
			else
				flag = 0;
		}
	}
	return;
}

int main(){
	int sum = 0;
	while(cin >> n >> d){
		if (n == 0 && d == 0)
			break;
		sum++;
		num = 0;
		memset(x, 0, sizeof(x));
		memset(y, 0, sizeof(y));
		for (int i = 0; i < n; i++){
			double a, b;
			cin >> a >> b;
			if (b > d){
				num = -1;
			}
			y[i] = sqrt(d*d - b*b);
			x[i] = a + y[i];
		}
		if (num == 0){
			for(int i = 0; i < n; i++){
				for (int j = 0; j < i; j++){
					if (x[j] > x[i]){
						double temp1 = x[i];
						x[i] = x[j];
						x[j] = temp1;
						double temp2 = y[i];
						y[i] = y[j];
						y[j] = temp2;
					}
				}
			}
			display_circle();
		}
		cout << "Case " << sum << ": " << num << endl;
	}
    return 0;
}
```
