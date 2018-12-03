```c
//注意输入的处理，有可能是两位数、三位数，而不仅仅是一位数
//AC
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
using namespace std;

#define INF 100010

int n, m, k, dm;
int len[1100][1100];
int d[1100], vis[1100];

int main(){
	scanf("%d %d %d %d", &n, &m, &k, &dm);
	fill(len[0], len[0]+1100*1100, INF);
	for (int i = 0; i < k; i++){
		string s;
		char str[5];
		int a, b;
		scanf("%s", str);
		s = str;
		int leng = s.length();
		if (s[0] != 'G'){
			a = 0;
			for (int j = 0; j < leng; j++)
				a = a*10 + (s[j]-'0');
			a--;
		}
		else{
			a = 0;
			for (int j = 1; j < leng; j++)
				a = a*10 + (s[j]-'0');
			a = n + a - 1;
		}
		scanf("%s", str);
		s = str;
		leng = s.length();
		if (s[0] != 'G'){
			b = 0;
			for (int j = 0; j < leng; j++)
				b = b*10 + (s[j]-'0');
			b--;
		}
		else{
			b = 0;
			for (int j = 1; j < leng; j++)
				b = b*10 + (s[j]-'0');
			b = n + b - 1;
		}
		scanf("%d", &len[a][b]);
		len[b][a] = len[a][b];
	}
	int all = n + m;
	float maxdis = -1;
	float minavg = INF;
	int minindex = -1;
	for (int i = n; i < n + m; i++){
		//printf("%d\n", i);
		fill(d, d+1100, INF);
		memset(vis, 0, sizeof(vis));
		d[i] = 0;
		float mindis = INF;
		int h = all;
		int flag = 0;
		while(h--){
			int now = -1;
			int minum = INF;
			for (int j = 0; j < all; j++){
				if (vis[j] == 0 && d[j] < INF){
					if (d[j] < minum){
						minum = d[j];
						now = j;
					}
				}
			}
			if (now == -1) break;
			vis[now] = 1;
			if (minum > dm && now < n){
				flag = 1;
				break;
			}
			if (minum < mindis && now < n && minum != 0){
				mindis = minum;
			}
			//printf("%d %d %f\n", now, minum, mindis);
			for (int j = 0; j < all; j++){
				if (vis[j] == 0 && len[now][j] != INF){
					if (d[now] + len[now][j] < d[j]){
						d[j] = d[now] + len[now][j];
					}
				}
			}
		}
		if (mindis >= maxdis && flag == 0){
			//printf("%f %f\n", mindis, maxdis);
			float temp = 0;
			for (int j = 0; j < n; j++){
				temp += d[j];
			}
			temp = temp/float(n);
			if (mindis > maxdis){
				maxdis = mindis;
				minindex = i-n+1;
				minavg = temp;
			}
			else{
				if (temp < minavg){
					minavg = temp;
					minindex = i-n+1;
				}
			}
		}
	}
	if (minindex == -1)
		printf("No Solution\n");
	else{
		printf("G%d\n", minindex);
		printf("%.1f %.1f\n", maxdis+0.005, minavg+0.005);
	}
    return 0;
}


//AC
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
using namespace std;

#define INF 1e9

int n, m, k, dm;
int len[1100][1100];
int d[1100], vis[1100];

int main(){
	scanf("%d %d %d %d", &n, &m, &k, &dm);
	fill(len[0], len[0]+1100*1100, INF);
	for (int i = 0; i < k; i++){
		string s;
		char str[6];
		int a, b;
		scanf("%s", str);
		s = str;
		int leng = s.length();
		if (s[0] != 'G'){
			a = 0;
			for (int j = 0; j < leng; j++)
				a = a*10 + (s[j]-'0');
			a--;
		}
		else{
			a = 0;
			for (int j = 1; j < leng; j++)
				a = a*10 + (s[j]-'0');
			a = n + a - 1;
		}
		scanf("%s", str);
		s = str;
		leng = s.length();
		if (s[0] != 'G'){
			b = 0;
			for (int j = 0; j < leng; j++)
				b = b*10 + (s[j]-'0');
			b--;
		}
		else{
			b = 0;
			for (int j = 1; j < leng; j++)
				b = b*10 + (s[j]-'0');
			b = n + b - 1;
		}
		scanf("%d", &len[a][b]);
		len[b][a] = len[a][b];
	}
	int all = n + m;
	double maxdis = 0;
	double minavg = INF;
	int minindex = -1;
	for (int i = n; i < n + m; i++){
		fill(d, d+1100, INF);
		memset(vis, 0, sizeof(vis));
		d[i] = 0;
		int h = all;
		while(h--){
			int now = -1;
			int minum = INF;
			for (int j = 0; j < all; j++){
				if (vis[j] == 0 && d[j] < INF){
					if (d[j] < minum){
						minum = d[j];
						now = j;
					}
				}
			}
			if (now == -1) break;
			vis[now] = 1;
			for (int j = 0; j < all; j++){
				if (vis[j] == 0 && len[now][j] != INF){
					if (d[now] + len[now][j] < d[j])
						d[j] = d[now] + len[now][j];
				}
			}
		}
		double mindis = INF;
		int flag = 0;
		double avg = 0;
		for (int j = 0; j < n; j++){
			if (d[j] > dm){
				flag = 1;
				break;
			}
			if (d[j] < mindis)
				mindis = d[j];
			avg += d[j];
		}
		if (flag == 0){
			if (mindis > maxdis){
				maxdis = mindis;
				minindex = i-n+1;
				minavg = avg;
			}
			else if (mindis == maxdis && avg < minavg){
				minavg = avg;
				minindex = i-n+1;
			}
		}
	}
	if (minindex == -1)
		printf("No Solution\n");
	else{
		printf("G%d\n", minindex);
		printf("%.1f %.1f\n", maxdis, minavg/n);
	}
    return 0;
}





// WA版本
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
using namespace std;

#define INF 100010

int n, m, k, dm;
int len[1100][1100];
int d[1100], vis[1100];

int main(){
	scanf("%d %d %d %d", &n, &m, &k, &dm);
	fill(len[0], len[0]+1100*1100, INF);
	for (int i = 0; i < k; i++){
		string s;
		char str[5];
		int a, b;
		scanf("%s", str);
		s = str;
		if (s.length() == 1)
			a = s[0]-'1';
		else
			a = n + s[1]-'1';
		scanf("%s", str);
		s = str;
		if (s.length() == 1)
			b = s[0]-'1';
		else
			b = n + s[1]-'1';
		int temp;
		scanf("%d", &temp);
		if (temp < len[a][b]){
			len[a][b] = temp;
			len[b][a] = temp;
		}
	}
	int all = n + m;
	float maxdis = -1;
	float minavg = INF;
	int minindex = -1;
	for (int i = n; i < n + m; i++){
		//printf("%d\n", i);
		fill(d, d+1100, INF);
		memset(vis, 0, sizeof(vis));
		d[i] = 0;
		float mindis = INF;
		int h = all;
		int flag = 0;
		while(h--){
			int now = -1;
			int minum = INF;
			for (int j = 0; j < all; j++){
				if (vis[j] == 0 && d[j] < INF){
					if (d[j] < minum){
						minum = d[j];
						now = j;
					}
				}
			}
			if (now == -1) break;
			vis[now] = 1;
			if (minum > dm && now < n){
				flag = 1;
				break;
			}
			if (minum < mindis && now < n && minum != 0){
				mindis = minum;
			}
			//printf("%d %d %f\n", now, minum, mindis);
			for (int j = 0; j < all; j++){
				if (vis[j] == 0 && len[now][j] != INF){
					if (d[now] + len[now][j] < d[j]){
						d[j] = d[now] + len[now][j];
					}
				}
			}
		}
		if (mindis >= maxdis && flag == 0){
			//printf("%f %f\n", mindis, maxdis);
			float temp = 0;
			for (int j = 0; j < n; j++){
				temp += d[j];
			}
			temp = temp/float(n);
			if (mindis > maxdis){
				maxdis = mindis;
				minindex = i-n+1;
				minavg = temp;
			}
			else{
				if (temp < minavg){
					minavg = temp;
					minindex = i-n+1;
				}
			}
		}
	}
	if (minindex == -1)
		printf("No Solution\n");
	else{
		printf("G%d\n", minindex);
		printf("%.1f %.1f\n", maxdis+0.005, minavg+0.005);
	}
    return 0;
}
```
