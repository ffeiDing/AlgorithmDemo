#include <iostream>
#include <iomanip>
#include <cmath>
#include <stdio.h>
#include <queue>
#include <cstring>
#include <set>
using namespace std;

struct Node{
	int x;
	int y;
	int sum;
	int kill;
	Node(int _x, int _y, int _sum, int _kill){
		x = _x;
		y = _y;
		sum = _sum;
		kill = _kill;
	}
	Node(){}
};

Node s;
Node e;

int m, n;
int num = 0;
char map[110][110];
int vis[110][110][256];
int x_index[4] = {-1, 1, 0, 0};
int y_index[4] = {0, 0, 1, -1};
int score[110][110];
queue<Node> qu;

bool is_valid(int x, int y){
	return x >= 0 && x < n && y >= 0 && y < m && map[x][y] == '.'; 
}

int bfs(){
	vis[s.x][s.y][score[s.x][s.y]] = 1;
	qu.push(s);
	while(!qu.empty()){
		Node node = qu.front();
		qu.pop();
		if (node.x == e.x && node.y == e.y && node.kill == (1<<num)-1)
			return node.sum;
		//cout << e.x <<" " <<  e.y  << " " << num << " " << node.x << " " << node.y << " " << node.kill << endl;
		for (int i = 0; i < 4; i++){
			int x = node.x + x_index[i];
			int y = node.y + y_index[i];
			if (is_valid(x, y)){
				int score_tmp = node.kill|score[x][y];
				if (vis[x][y][score_tmp] == 0){
					vis[x][y][score_tmp] = 1;
					qu.push(Node(x, y, node.sum+1, score_tmp));
				}
			}
		}
	}
	return -1;
}

int main(){
	cin >> n >> m;
	memset(vis, 0, sizeof(vis));
	memset(map, 0, sizeof(map));
	memset(score, 0, sizeof(score));
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			cin >> map[i][j];
			if (map[i][j] == 'I'){
				s.x = i;
				s.y = j;
				s.sum = 0;
				s.kill = 0;
				map[i][j] = '.';
			}
			else if (map[i][j] == 'O'){
				e.x = i;
				e.y = j;
				map[i][j] = '.';
			}
		}
	}
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			//cout << num << endl;
			if (map[i][j] == 'w'){
				int tmp = 1<<num;
				num++;
				for (int k = i-1; k >= 0 && map[k][j] == '.'; k--)
					score[k][j] += tmp;
			}
			else if (map[i][j] == 's'){
				int tmp = 1<<num;
				num++;
				for (int k = i+1; k < m && map[k][j] == '.'; k++)
					score[k][j] += tmp;
			}
			else if (map[i][j] == 'a'){
				int tmp = 1<<num;
				num++;
				for (int k = j-1; k >= 0 && map[i][k] == '.'; k--)
					score[i][k] += tmp;
			}
			else if (map[i][j] == 'd'){
				int tmp = 1<<num;
				num++;
				for (int k = j+1; k < n && map[i][k] == '.'; k++)
					score[i][k] += tmp;
			}
		}
	}
	s.kill = score[s.x][s.y];
	cout << bfs() << endl;
    return 0;
}
