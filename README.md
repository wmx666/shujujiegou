# shujujiegou

#include<iostream>
using namespace std;
template <class T>
class stack1
{
public:
	stack1(int x)
	{	
		    top[0] = -1;
			top[1] = size;
	}
	void push(T y,int x)
	{
		if(0==x)
		{
			if (top[x] +1 >= top[1])
			{
				throw "上溢";
			}
			top[x]++;
			data[top[x]] = y;
		}
		else
		{
			if (top[x] -1 <= top[0])
			{ 
				throw "上溢";
			}
			top[x]--;
			data[top[x]] = y;
		}
	
	}
	T pop(int x)
	{
		if (empty(x))
		{
			throw"下溢";
		}
		if(0==x)
		{
			top[x]--;
			return data[top[x]+1];
		}
		else
		{
			top[x]++;
			return data[top[x]-1];
		}
		
	}
	T gettop(int x)
	{
		if (empty(x))
		{
			cout << "下溢";
		}
		return data[top[x]];
	}
	bool empty(int x)
	{
		if(0==x)
		{ 
			if (-1 == top[x])
				return true;
			else
				return false;
		}
		if (1 == x)
		{
			if (size == top[x])
				return true;
			else
				return false;
		}
		
	}
	void sharestack(T a[],T b[],T x1,T x2)
	{
		top[0] = -1;
		top[1] = size;
		if (x1 + x2 <= size)
		{
			for (int i = 0; i < x1; i++)
			{
				top[0]++;
				data[top[0]] = a[i];
			}
			for (int i = 0; i < x2; i++)
			{
				top[1]--;
					data[top[1]] = b[i];
			}
		}
		else
			throw"上溢";
	}
	void print(int x)
	{
		if (empty(x))
		{
			throw"上溢";
		}
		else
		{
			if(0==x)
			{ 
				for (int y=0; y <= top[x]; y++)
					cout << data[y]<<" ";
				cout << endl;
			}
			if (1 == x)
			{
				for (int k = size-1; k >= top[x]; k--)
					cout << data[k] << " ";
				cout<<endl;
			}

		}

	}
	int top[2];
	const int size = 100;
	T *data=new T[size];

};
int main()
{
	stack1<int>t1(0);
	cout << t1.empty(0) << endl;
	t1.push(3,0);
	t1.push(5,0);
	cout << t1.empty(1) << endl;
	cout<<t1.gettop(0)<<endl;
	cout << t1.empty(0) << endl;
	cout << t1.pop(0) << endl;
	cout << t1.gettop(0)<<endl;

	stack1<int>t2(1);
	int a[7] = { 3,3,2,5,6,7,8 };
	int b[3] = { 6,4,3 };
	t2.sharestack(a, b, 7, 3);
	t2.print(0);
	t2.print(1);
	cout << t2.top[0]<<endl;
	cout<<t2.pop(0)<<endl;
	cout << t2.top[0] << endl;
	t2.print(0);
	t2.print(1);
	cout<<t2.gettop(0)<<endl;
	cout<<t2.gettop(1) << endl;
	try
	{
		for (int i = 0; i < 102; i++)
		{
			t1.push(i, 0);
		}
	}
	catch (const char* s)
	{
		cerr << s << endl; 
	}
	try
	{
		for (int i = 0; i < 100; i++)
		{
			t1.pop(1);
		}
	}
	catch (const char* s)
	{
		cerr << s << endl; 
	}
	system("pause");
}
