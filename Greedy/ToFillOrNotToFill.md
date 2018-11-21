```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <algorithm>
#include <set>
using namespace std;

double c, d, d_avg;
int n;
double sum = 0;
double left_oil = 0;

struct Node{
	double price;
	double dis;
	bool operator < (Node n) const{
		if (dis == n.dis)
			return price < n.price;
		return dis < n.dis;
	}
};

Node station[510];
Node s[510];

int main(){
	cin >> c >> d >> d_avg >> n;
	for (int i = 0; i < n; i++){
		cin >> s[i].price >> s[i].dis;
	}
	s[n].dis = d;
	s[n].price = 0;
	sort(s, s+n+1);
	int count = 1;
	double now = s[0].dis;
	station[0] = s[0];
	for (int i = 1; i < n+1; i++){
		if (s[i].dis != now){
			station[count++] = s[i];
			now = s[i].dis;
		}
	}
	if (station[0].dis != 0){
		cout << "The maximum travel distance = 0.00" << endl;
	}
	else{
		int i = 0;
		int possible = 0;
		while (i < count){
			if (i == count - 1){
				if (possible == 0)
					cout << fixed << setprecision(2) << sum << endl;
				break;
			}
			if (station[i].price >= station[i+1].price){
				double temp = station[i+1].dis - station[i].dis;
				if (temp/d_avg <= left_oil)
					left_oil -= temp/d_avg;
				else if (temp/d_avg > c){
					possible = 1;
					cout << fixed << setprecision(2) << "The maximum travel distance = " << station[i].dis+c*d_avg << endl;
					break;
				}
				else{
					sum += (temp/d_avg-left_oil)*station[i].price;
					left_oil = 0;
				}
				i++;
			}
			else{
				double temp = station[i+1].dis - station[i].dis;
				if (temp/d_avg > c){
					possible = 1;
					cout << fixed << setprecision(2) << "The maximum travel distance = " << station[i].dis+c*d_avg << endl;
					break;
				}
				else{
					double max_dis = station[i].dis + c*d_avg;
					int flag = 0;
					for (int j = i+1; j < count; j++){
						if (station[j].dis < max_dis && station[j].price < station[i].price){
							flag = 1;
							if ((station[j].dis-station[i].dis)/d_avg > left_oil){
								sum += ((station[j].dis-station[i].dis)/d_avg-left_oil)*station[i].price;
								left_oil = 0;
							}
							else
								left_oil -= (station[j].dis-station[i].dis)/d_avg;
							i = j;
							break;
						}
					}
					if (flag == 0){
						sum += (c-left_oil)*station[i].price;
						left_oil = c-temp/d_avg;
						i++;
					}
				}
			}
		}
	}
    return 0;
}

```
