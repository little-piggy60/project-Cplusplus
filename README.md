# Git-little-piggy

#include <iostream>
using namespace std;
const int MAXSIZE = 1000;
template<class T>
struct Node
{
	T data;
	int next;
};
template<class T>
class stalinklist
{
public:
	stalinklist();
	stalinklist(T a[], int n);
	void Delete(int i);
	void insert(int i, T a);
	T get(int k);
	int getlength();
	void printf();
	~stalinklist();
private:
	int front;
	int tail;
	int length;
	Node<T>sarry[MAXSIZE];
};
template<class T>
stalinklist<T>::stalinklist()
{
	for (int i = 0; i < MAXSIZE - 1; i++)
		sarry[i].next = i + 1;
	sarry[MAXSIZE - 1].next = -1;
	front = -1;
	tail = 0;
}
template<class T>
stalinklist<T>::stalinklist(T a[], int n)//头插法
{
	for (int i = n; i < MAXSIZE - 1; i++)
		sarry[i].next = i + 1;
	sarry[MAXSIZE - 1].next = -1;
	tail = n;
	front = 0;
	sarry[front].next = -1;
	length = 0;
	if (n > MAXSIZE)throw"空间不足";
	for (int i = n - 1; i > 0; i--)//模仿单链表进行头插法
	{
		
		sarry[i].data = a[i];
		sarry[i].next = sarry[front].next;
		sarry[front].next = i;
		length++;
	}
	sarry[front].data = a[0];
	length += 1;
}
//template<class T>
//stalinklist<T>::stalinklist(T a[], int n)//尾插法建立静态链表的数据链表
//{
//	if (n<=0||n >MAXSIZE)throw"空间不足或插入错误";
//	for (int i = n; i < MAXSIZE - 1; i++)
//	{
//		sarry[i].next = i + 1;
//	}
//		sarry[MAXSIZE - 1].next = -1;
//		tail = n;
//		length = 0;
//	front = 0;
//	int m = front;
//	for (int i = 0; i <n; i++)
//	{
//		sarry[i].data = a[i];
//		sarry[m].next = i;
//		m = i;
//		length += 1;
//	}
//	sarry[n - 1].next = -1;
//}

template<class T>
void stalinklist<T>::insert(int i, T a)
{
	if (tail == -1 || i > MAXSIZE || i < 0||i>length)throw"空间不足或插入错误";
	int m = tail;
	sarry[m].data = a;
	tail = sarry[m].next;

	if (front == -1)
	{
		if (i != 0)throw"空链表只能插入0位置";//确保插入位置准确
		sarry[tail].data = a;
		front = tail;
		tail = sarry[m].next;
		sarry[m].next = -1;
	}
	else if (i == 0)
	{
		sarry[m].next = front;
		front = m;
	}
	else
	{
		int prev = front;
		int j = 0;
	while (j != i-1)
	{
		j++;
		prev = sarry[prev].next;
	}
		sarry[m].next = sarry[prev].next;
		sarry[prev].next = m;
	}
}
template<class T>
void stalinklist<T>::Delete(int i)
{
	if (i<0 || i>(MAXSIZE - 1) || -1 == front)
		throw"释放空间错误";
	int p = sarry[i].next;
	if (p != -1)
	{
		sarry[i] = sarry[p];
	}
	else
	{
		p = i;
		int k = front;
		int prek = k;
		while (sarry[k].next != -1)
		{
			prek = k;
			k = sarry[k].next;
		}
		sarry[prek].next = -1;
	}
	sarry[p].next = tail;
	tail = p;
	if (front == i)
	{
		front = sarry[i].next;
	}
}
template<class T>
T stalinklist<T>::get(int k)
{
	int i = front;
	int n = 0;
	while (n != k)
	{
		if (sarry[i].next == -1)

		{
			cout << "链表中没有存储第k个元素" << " ";
			break;
		}
		n += 1;
		i = sarry[i].next;
	}
	return sarry[i].data;
}
template<class T>
int stalinklist<T>::getlength()
{
	int n = 1;
	int i = front;
	if (front == -1)
	{
		n = 0;
		return n;
	}
	else
	{
		while (sarry[i].next != -1)
		{
			n++;
			i = sarry[i].next;
		}
		return n;
	}
}
template<class T>
stalinklist<T>::~stalinklist()
{
	front = -1;
	tail = 0;
}
template <class T>
void stalinklist<T>::printf()
{
	int p = front;
	while (sarry[p].next != -1)
	{
		cout << sarry[p].data << " ";
		p = sarry[p].next;
	}
	cout << sarry[p].data << " ";
}
int main()
{
	int arr[] = { 1,2,3,4,5 };
	stalinklist<int>list(arr, 5);
	cout << "长度" << list.getlength ()<< endl;
	cout << "第3个元素：" << list.get(0) << endl;
	cout << "进行操作前的链表为：";
	list.printf();
	cout << endl;
	list.insert(4, 10);
	cout << "插入操作后的链表元素为：";
	list.printf();
	cout << endl;
	list.Delete(1);
	cout << "删除操作后的链表元素为：";
	list.printf();
	cout << endl;
	list.insert(4, 1);
	cout << "插入操作后的链表元素为：";
	list.printf();
	return 0;
}
