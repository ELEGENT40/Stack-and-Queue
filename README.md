# Stack-and-Queue
栈，队列的练习
#include <iostream>
#include <malloc.h>
using namespace std;
#define Maxsize 50

typedef struct {
	int data[Maxsize];
	int top;
}Sqstack;

Sqstack gst = { {0},-1 };

void InitStack(Sqstack &s) {
	s.top = -1;
}

void Push(Sqstack&s, int c) {//进栈
	if (s.top == Maxsize - 1) {
		cout << "error" << endl;
	}
	else {
		s.top++;
		s.data[s.top] = c;
	}
}
void Pop(Sqstack& s, int& c) {
	if (s.top == -1) {
		cout << "error" << endl;
	}
	else {
		c = s.data[s.top];
		s.top--;
	}
}
void GetTop(Sqstack& s, int& c) {
	if (s.top == -1) {
		cout << "error" << endl;
	}
	else {
		c = s.data[s.top];
	}
}

int trans(char *postexp) {
	InitStack(gst);
		 int a = 0;
	while (*postexp != '\0') {
		int i = 0, j = 0;
		if (*postexp <= '9' && *postexp >= '0') {
			a = *postexp - '0';
			Push(gst, a);
		}
		else {
			if (*postexp == '+') {
				GetTop(gst, i), Pop(gst,i), GetTop(gst, j), Pop(gst, j), Push(gst, j + i);
			}
			if (*postexp == '-') {
				GetTop(gst, i), Pop(gst, i), GetTop(gst, j), Pop(gst, j), Push(gst, j - i);
			}
			if (*postexp == '*') {
				GetTop(gst, i), Pop(gst, i), GetTop(gst, j), Pop(gst, j), Push(gst, j * i);
			}
			if (*postexp == '/') {
				GetTop(gst, i), Pop(gst, i), GetTop(gst, j), Pop(gst, j), Push(gst, j / i);
			}
		}
		postexp++;
	}
	GetTop(gst, a);
	return a;
}

int main() {
	char postexp[] = "634+*7+";
	cin >> postexp;
	int num = -1;
	num = trans(postexp);
	cout << "The result is: " << num << endl;
	return 0;
}
