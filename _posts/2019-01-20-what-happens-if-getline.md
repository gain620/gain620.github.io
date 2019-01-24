---
published: true
layout: single
title: "What happens if the input exceeds the provided getline function's buffer size?"
date: 2019-01-20
category: post
tags: [c++, programming, iostream, getline, cin.clear(), failbit, goodbit]
comments: true
---


I was reviewing on **cin.getline()** and I got curious, what happens if the input exceeds the *provided buffer size*?

First, I assumed that the following getline function will read the remaining characters from the stream, but I was actually wrong. Yes, the stream will keep the rest parts, but when you exceed the specified count of characters, it will set a failbit. Therefore the next getline function just skips.

In order to solve this problem, you can simply add
```
cin.clear()
```

This will set the state bit to goodbit, and the next getline function will work fine.

```cpp
#include <iostream>

using namespace std;

int main()
{
    char nameA[5];
    char nameB[10];
    
    cout << "nameA : " ;
    cin.getline(nameA,5); // abcdefg => nameA(abcd\0) + buffer(efg\n)
    
    // if getline fills in the provided buffer without encountering the delimiter('\n')
    // it will set a failbit, so the following getline function won't just work.
    
    // therefore we need to clear the state of the stream and set the flag back to "goodbit"
    // clears failbit, so the next getline function works properly
    // cin.clear(); 
    
    // if you want to delete some characters from the buffer
    // cin.ignore(3, '\n');
    
    cout << "nameB : ";
    cin.getline(nameB,10);
    
    cout << endl << "Result : ";
    cout << nameA << ":" << nameB << endl;

    return 0;
}
```


Reference:
[https://en.cppreference.com/w/cpp/io/basic_istream/getline]