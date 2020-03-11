---
layout: post
title: "[Codeforces 1316D] Nash Matrix"
description: "[Codeforces 1316D] Nash Matrix"
date: 2020-03-11 18:04:00
categories: Algorithm
comments: true
---
[[Codeforces 1316D] Nash Matrix](http://codeforces.com/contest/1316/problem/D)

## 문제 요약

게임 판의 가로와 세로 길이를 나타내는 양의 정수 n과 게임 판의 각 칸(x, y)별로 도달해야 할 칸의 위치(dx, dy)가 주어졌을 때, X가 도착지점, U,D,L,R은 각각 위,아래,왼쪽,오른쪽으로 이동을 나타내는 문자들로 게임 판을 구성할 수 있는지 여부를 구하고 게임판을 출력하는 문제

## 풀이

예를 들어 (1,1)에서 (1,1)로 도착해야 한다면, 해당 (1,1) 지점이 X가 되어야 한다는 것이고,  
(1,2)에서 (1,1)로 도착해야 한다면 (1,2) 지점에 U가 있어야 목적지에 도달할 수 있다는 것이다.  
이 문제는 뒤집어 생각해보면 해결할 수 있다.  
반복문을 통해 각 칸이 어느 칸을 향해야 하는지를 검사하고, (-1,-1)인 경우에는 끊임없이 게임판을 헤매면서 X 칸에 도달할 수 없게 만들고,
(-1,-1)이 아닌 경우에는 목표 지점으로 향하게 만들어야 한다.  
이를 뒤집어 생각해보면 목표 지점이 될 수 있는 칸((x,y) = (dx,dy))에서 dfs든 bfs를 활용하여 목표 지점으로 도달해야 하는 다른 칸들을 찾아서 탐색 방향과 반대 방향으로 게임판을 구성해주면 된다는 결론에 도달한다.  
목표 지점이 없는 칸의 경우에는 서로 (-1,-1)끼리만 이어질(순환될) 수 있도록 시작점과 끝점을 정하고 마찬가지로 순회를 통해 방향을 정해주면 된다.  
나머지 INVALID한 경우는 목표 지점이 없는 칸임에도 불구하고 순환될 수 없도록 시작점은 있지만 끝점은 없는 경우와 모든 게임판의 탐색이 끝났을 때 한 번도 방문되지 않은 칸이 경우 두 가지가 있다.

## 코드

```C++
#include <cstdio>
using namespace std;
int n, dx[] = { 0,-1,1,0 }, dy[] = { 1,0,0,-1 }, X[1001][1001], Y[1001][1001];
bool v[1001][1001];
char dir[] = "URLD", ans[1001][1001];
bool boardValidation(int x, int y) {
    return 0 < x && x <= n && 0 < y && y <= n && !v[y][x];
}
void dfs(int x, int y) {
    v[y][x] = 1;
    for (int i = 0; i < 4; i++) {
        int nx = x + dx[i], ny = y + dy[i];
        if (boardValidation(nx, ny) && X[y][x] == X[ny][nx] && Y[y][x] == Y[ny][nx]) {
            ans[ny][nx] = dir[i];
            dfs(nx, ny);
        }
    }
}
int main() {
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) for (int j = 1; j <= n; j++) scanf("%d %d", &Y[i][j], &X[i][j]);
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++) {
            if (v[i][j]) continue;
            if (X[i][j] == j && Y[i][j] == i) {
                ans[i][j] = 'X';
                dfs(j, i);
            }
            if (X[i][j] == -1) {
                bool b = 1;
                for (int k = 0; k < 4; k++) {
                    int x = j + dx[k], y = i + dy[k];
                    if (boardValidation(x, y) && X[y][x] == -1) {
                        ans[y][x] = dir[k];
                        ans[i][j] = dir[3 - k];
                        dfs(x, y);
                        dfs(j, i);
                        b = 0;
                        break;
                    }
                }
                if (b) {
                    puts("INVALID");
                    return 0;
                }
            }
        }
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            if (!v[i][j]) {
                puts("INVALID");
                return 0;
            }
    puts("VALID");
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) printf("%c", ans[i][j]);
        puts("");
    }
    return 0;
}
```
