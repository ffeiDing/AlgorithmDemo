AC:
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
using namespace std;

int n, h, num[30], d[30], sum, t[30];
int temp[30], max_sum, fish[30], fish_temp[30];

int main() {
	while(cin >> n){
		if (n==0) break;
		cin >> h;
		h = h*60;
		for (int i = 0; i < n; i++){
			cin >> num[i];
			temp[i] = num[i];
		}
		memset(fish, 0, sizeof(fish));
		memset(fish_temp, 0, sizeof(fish_temp));
		max_sum = -1;
		for (int i = 0; i < n; i++)
			cin >> d[i];
		for (int i = 0; i < n-1; i++)
			cin >> t[i];
		for (int i = 0; i < n; i++){
			int cost = 0;
			sum = 0;
			for (int j = 0; j < i; j++)
				cost += t[j];
			int fish_time = h/5-cost;
			for (int k = 0; k < fish_time; k++){
				int max_num = -1;
				int idx = -1;
				for (int j = 0; j <= i; j++){
					if (temp[j] > max_num){
						max_num = temp[j];
						idx = j;
					}
				}
				sum += temp[idx];
				temp[idx] -= d[idx];
				fish_temp[idx]++;
				if (temp[idx] < 0)
					temp[idx] = 0;
			}
			if (sum > max_sum){
				max_sum = sum;
				for (int j = 0; j < n; j++){
					fish[j] = fish_temp[j];
				}
			}
			for (int l = 0; l < n; l++){
				temp[l] = num[l];
			}
			memset(fish_temp, 0, sizeof(fish_temp));
		}

		cout << fish[0]*5;
		for (int i = 1; i < n; i++){
			cout << ", " << fish[i]*5;
		}
		cout << endl;
		cout << "Number of fish expected: " << max_sum << endl;
		cout << endl;
	}
	return 0;
}
```

TLE:
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
using namespace std;

int n, h, num[30], d[30], sum, t[30];
int temp[30], max_sum, fish[30], fish_temp[30];

int main() {
	while(cin >> n){
		if (n==0) break;
		cin >> h;
		h = h*60;
		for (int i = 0; i < n; i++){
			cin >> num[i];
			temp[i] = num[i];
		}
		memset(fish, 0, sizeof(fish));
		memset(fish_temp, 0, sizeof(fish_temp));
		max_sum = -1;
		for (int i = 0; i < n; i++)
			cin >> d[i];
		for (int i = 0; i < n-1; i++)
			cin >> t[i];
		for (int i = 0; i < n; i++){
			int cost = 0;
			sum = 0;
			for (int j = 0; j < i; j++)
				cost += t[j];
			int fish_time = h/5-cost;
			while (fish_time--){
				int max_num = -1;
				int idx = -1;
				for (int j = 0; j <= i; j++){
					if (temp[j] > max_num){
						max_num = temp[j];
						idx = j;
					}
				}
				sum += temp[idx];
				temp[idx] -= d[idx];
				fish_temp[idx]++;
				if (temp[idx] < 0)
					temp[idx] = 0;
			}
			if (sum > max_sum){
				max_sum = sum;
				for (int j = 0; j < n; j++){
					fish[j] = fish_temp[j];
				}
			}
			for (int l = 0; l < n; l++)
				temp[l] = num[l];
			memset(fish_temp, 0, sizeof(fish_temp));
		}

		cout << fish[0]*5;
		for (int i = 1; i < n; i++){
			cout << ", " << fish[i]*5;
		}
		cout << endl;
		cout << "Number of fish expected: " << max_sum << endl;
		cout << endl;
	}
	return 0;
}
```
