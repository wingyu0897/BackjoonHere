# [문제](https://www.acmicpc.net/problem/1260 "#1260번")
  
> 그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.
<hr/>

# 풀이

```cpp
#include<iostream>
#include<vector>
#include<queue>
using namespace std;

vector<bool> visited;
vector<vector<bool>> linked;
int now;

void DFS(int n, int v)
{
	cout << v << " ";
	visited[v] = true;

	for (int i = 1; i <= n; i++)
	{
		if (i != v && visited[i] == false)
		{
			if (linked[v][i] == true)
			{
				DFS(n, i);
			}
		}
	}
}

void BFS(int n, int v)
{
	visited.clear();
	visited.resize(n + 1, false);

	visited[v] = true;

	queue<int> q;
	q.push(v);

	while (!q.empty())
	{
		now = q.front();
		q.pop();
		cout << now << " ";

		for (int i = 1; i <= n; i++)
		{
			if (i != v && visited[i] == false)
			{
				if (linked[now][i] == true)
				{
					q.push(i);
					visited[i] = true;
				}
			}
		}
	}
}

int main()
{
	int n, m, v, a, b;
	cin >> n >> m >> v;

	visited.resize(n + 1, false);
	linked.resize(n + 1, vector<bool>(n + 1, false));

	for (int i = 0; i < m; i++)
	{
		cin >> a >> b;
		linked[a][b] = true;
		linked[b][a] = true;
	}

	DFS(n, v);
	cout << '\n';
	BFS(n, v);

	return 0;
}
```

