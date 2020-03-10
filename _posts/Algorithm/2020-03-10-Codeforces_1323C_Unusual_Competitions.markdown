---
layout: post
title: "[Codeforces 1323C] Unusual Competitions"
description: "[Codeforces 1323C] Unusual Competitions"
date: 2020-03-10 17:42:00
categories: Algorithm
comments: true
---
[[Codeforces 1323C] Unusual Competitions](http://codeforces.com/contest/1323/problem/C)

## 문제 요약

문자열의 길이와 '(', ')'로 이루어진 괄호 문자열이 주어졌을 때, 어떤 부분 문자열들을 재배치해서 올바른 괄호 문자열로 고치기 위한 모든 부분 문자열들의 길이를 합하여 최소 길이를 구하는 문제

## 풀이

괄호 문자열과 관련된 문제들은 보통 스택을 이용해서 해결한다.  
이 문제 또한 마찬가지로 스택을 활용하는데, 부분 문자열들의 순서를 재배치해서 올바른 괄호 문자열로 고칠 수 있기 때문에 여는 괄호와 닫는 괄호의 수가 짝이 맞는지를 눈 여겨 봐야 한다.  
그래서 괄호의 짝은 맞지만, 순서가 다른 경우에 길이를 더 해주고 마지막에 스택에 남아있는 괄호가 있는지를 확인해 주면 된다.

## 코드

```C++
#include <iostream>
#include <vector>
using namespace std;
int n, ans;
vector<char> st;
char s[1000001];
int main() {
    scanf("%d", &n);
    scanf("%s", s);
    for (int i = 0; i < n; i++) {
        if (s[i] == '(') {
            if (st.empty() || st.back() == '(') st.push_back('(');
            else {
                ans++;
                st.pop_back();
            }
        }
        else {
            if (st.empty() || st.back() == ')') {
                ans++;
                st.push_back(')');
            }
            else st.pop_back();
        }
    }
    printf("%d", st.size() ? -1 : ans);
    return 0;
}
```
