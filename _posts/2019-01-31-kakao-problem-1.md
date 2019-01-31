---
published: true
layout: single
title: "Kakao algorithms problem #1"
date: 2019-01-31
category: post
tags: [c++, programming, problem solving]
comments: true
---

## 2019 Kakao coding interview problem #1

**https://www.welcomekakao.com/learn/courses/30/lessons/42888**

```cpp
#include <string>
#include <vector>
#include <unordered_map>
#include <sstream>

using namespace std;

vector<string> solution(vector<string> record) {
    vector<string> answer;
    unordered_map<string, string> users; // = {{"uid2424", "Sam"}};

    for(auto iter = record.begin(); iter != record.end(); iter++)
    {
        string temp = *iter;

        vector<string> tokens;
        string token;
        istringstream tokenStream(temp);
        while (getline(tokenStream, token, ' '))
        {
              tokens.push_back(token);
        }

        if(tokens[0] != "Leave")
        {
            users[tokens[1]] = tokens[2];
        }

        if(tokens[0] == "Enter")
        {
            answer.push_back(tokens[1]+"님이 들어왔습니다.");  
        }else if (tokens[0] == "Leave")
        {
            answer.push_back(tokens[1]+"님이 나갔습니다.");   
        }

    }

    for (auto iter = answer.begin(); iter != answer.end(); iter++)
    {
        size_t pos = (*iter).find("님");
        string userId = (*iter).substr(0, pos);

        (*iter).replace(0, pos, users[userId]);
    }

    return answer;
}
```