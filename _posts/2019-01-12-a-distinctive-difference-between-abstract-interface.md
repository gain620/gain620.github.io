---
published: true
layout: single
title: "A distinctive difference between Abstract class vs. Interface (Pure Abstract Classes in C++)"
category: post
tags: [c++, programming, abstract class, interface]
comments: true
---

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/man.jpg" alt="abstract class">

## Abstract class:
- can't be instantiated.
- is a special class which you can have some members without any implementations.
- usually used for framework library classes. (utilizes IoC, which it provides some default methods but enforces the programmer to implement the rest stuffs)
- All abstract methods have to be implemented, in order to be instantiated to an object.
- An abstract class contains at least one pure virtual function. You declare a pure virtual function by using a pure specifier (= 0)
- IS-A relationship.
- e.g. Porsche911 IS A Car, GameplayProgrammer IS A Programmer.

```cpp
// 'framework library' for a person
// a person can enrol and submit
// however, the class that consume this framework library
// need to provide 'where' the paperwork need to be sent
class Person
{
public:
	Person(){}

	void Enrol()
	{
		SendPaperWork("ENROL");
	}

	void Submit()
	{
		SendPaperWork("SUBMIT");
	}

private:
	virtual void SendPaperWork(string paperwork) = 0;
};

// by inheriting Person abstract class
// we are enabling student to enrol and submit
// however, SendPaperWork need to be implemented
// because we need to tell it explicitly 'where' 
// to send the enrolment/ submission
class Student : public Person
{
public:
	Student(){}
private:
	virtual void SendPaperWork(string paperwork) override
	{
		//School.Send(paperwork);
		cout << paperwork << endl;
	}
};

// an employee send the paperwork to a different 'place' than student
class Employee : public Person
{
public:
	Employee(){}
private:
	virtual void SendPaperWork(string paperwork) override
	{
		//Company.Send(paperwork);
		cout << paperwork << endl;	
	}
};
```

## Interface:
- can't be instantiated.
- is a special class which you have no members that have any implementations.
- A class that implements an Interface need to contain all the implementation, otherwise the compiler will throw an error.
- CAN-DO relationship.
e.g. Student CAN enrol, Student CAN submit assignment.

```cpp
class ICanEnrol
{
    virtual void Enrol() = 0;
};

class ICanSubmit
{
    virutal void Submit() = 0;
};

class Student : public ICanEnrol, ICanSubmit
{
    virtual void Enrol() override
    {
        School.Send("enrolment");
    }

    virtual void Submit() override
    {
        School.Send("report");
    }
};
```



Reference:
[http://blog.naver.com/PostView.nhn?blogId=psychoria&logNo=40184422694&proxyReferer=https%3A%2F%2Fwww.google.com%2F]
[http://ozt88.tistory.com/17]
[http://ronaldwidha.net/2008/06/16/a-good-example-of-abstract-class-vs-interface/]