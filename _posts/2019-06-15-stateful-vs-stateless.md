---
published: true
layout: single
title: "Stateful vs. stateless"
date: 2019-06-15
category: post
tags: [programming, computer science]
comments: true
---
## Stateful - The program has a memory (state)
* 어떤 것이 "stateful"하다고 할때, 이것은 메모리에 앱/컴포넌트의 상태에 대한 정보들을 저장하는 중심 입니다. 이것은 또한 상태 값을 변경 할 수도 있습니다. 이것은 본질적으로 과거, 현재, 그리고 잠재적인 미래의 상태 변경에 대해 알고있는  "살아있는(living)" 것 입니다.

## Stateless - There's no memory (state) that's maintained by the program
* 어떤 것이 "stateless"하다고 할때, 이 것이 의미하는 것은 상태 값을 내부에서 계산을 하지만 절대 직접적으로 그 값을 변형시키지는 않는 것을 의미합니다. 이것은 완벽한 값의 투명성을 보장합니다. 이것이 의미하는 것은 입력값이 같을때, 결과값 역시 항상 같다는 것을 의미합니다. 

To illustrate the concept of state I'll define a function which is stateful and one which is stateless

Stateless
```c
//The state is derived by what is passed into the function

function int addOne(int number) { 
    return number + 1; 
}
```

Stateful
```c
//The state is maintained by the function 
private int _number = 0; //initially zero 
function int addOne() { 
    _number++; return _number; 
}
```

#### References
[Understanding differences in stateful vs. stateless
](https://jjeong.tistory.com/1127
)