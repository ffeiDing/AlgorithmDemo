```c
#include <iostream>
#include <iomanip>
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <string.h>
#include <assert.h>
#include <queue>
#include <vector>
#include <math.h>
#include <algorithm>
#include <set>
using namespace std;

int n;
priority_queue<double> qu;

int main() {
	cin >> n;
	for (int i = 0; i < n; i++){
		double temp;
		cin >> temp;
		qu.push(temp);
	}
	while(!qu.empty()){
		double temp1 = qu.top();
		qu.pop();
		if (qu.empty()){
			cout << fixed << setprecision(3) << temp1 << endl;
			break;
		}
		double temp2 = qu.top();
		qu.pop();
		temp1 = 2*sqrt(temp1*temp2);
		qu.push(temp1);
	}
	return 0;
}
```
