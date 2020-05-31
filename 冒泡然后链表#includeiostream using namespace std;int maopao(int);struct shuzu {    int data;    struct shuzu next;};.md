```c++
//冒泡然后链表
#include<iostream> 
using namespace std;

int maopao(int*);

struct shuzu {
	int data;
	struct shuzu* next;
};

int main(void) {
	int n;
	cin >> n;
	int student[n];
	for (int i = 0; i < n; i++)
		cin >> student[i];
	maopao(&student);

	shuzu* head, * curr, * next;
	head = curr;
	next = curr;
	for (int i = 0; i < n; i++) {
		curr = new struct shuzu;
		cin >> curr->data;
		curr->next = NULL;
		next = next->next;
	}
	//检查插入时机(升序排序
	int text;
	int exchange;
	cin >> text;
	for (int i = 0; i < n; i++) {
		if (head->data > text) {
			curr = new struct shuzu;
			curr->data = text;
			curr->next = NULL;
			next = 
		}
	}
}


```

