//最大堆与最小堆

```c
#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
using namespace std;

priority_queue<int> max_queue;
priority_queue<int, vector<int>, greater<int> > min_queue;

int main(){
	int t, n, num;
	char op;
	scanf("%d", &t);
	while(t--){
		while(!max_queue.empty())
			max_queue.pop();
		while(!min_queue.empty())
			min_queue.pop();
		scanf("%d", &n);
		while(n--){
			scanf(" %c", &op);
			if (op == 'I'){
				scanf(" %d", &num);
				if (max_queue.empty() || num <= max_queue.top())
					max_queue.push(num);
				else
					min_queue.push(num);
				if (max_queue.size() < min_queue.size()){
					int temp = min_queue.top();
					min_queue.pop();
					max_queue.push(temp);
				}
				if (max_queue.size() > min_queue.size() + 1){
					int temp = max_queue.top();
					max_queue.pop();
					min_queue.push(temp);
				}
			}
			if (op == 'D'){
				if (!max_queue.empty()){
					max_queue.pop();
					if (max_queue.size() < min_queue.size()){
						int temp = min_queue.top();
						min_queue.pop();
						max_queue.push(temp);
					}
				}
			}
			if (op == 'Q')
				printf("%d\n", max_queue.top());
		}
	}
    return 0;
}
```
