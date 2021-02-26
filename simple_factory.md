# 面向对象
要理解简单工厂模式，必须先引入了面向对象编程。雕版印刷术到活字印刷术的转变来类比传统的编程思想到面向对象编程思想的转变是再合适不过的例子了。面向对象编程就像活字印刷术一般，拥有可维护、可复用、可拓展属性，抽象出来，就是面向对象编程的三大核心思想：封装、继承、多态。

# 简单工程模式
用一个单独的类，即工厂类来负责实例的创建，以清晰的知道实例化的对象是谁，更方便增加实例化对象

```cpp
class Calculation
{
	public:
		virtual double GetResult()=0;
		double numberA;
		double numberB;
};

class Add:public Calculation
{
	virtual double GetResult()
	{
		return numberA+numberB;
	}
};

class Sub:public Calculation
{
	virtual double GetResult()
	{
		return numberA-numberB;
	}
};

class Div:public Calculation
{
	virtual double GetResult()
	{
		if (numberB==0)
		{
			throw new exception("除数不能为0")
		}
		return numberA/numberB;
	}
};


class Factory
{
	public:
		static Calculation* createCalculation(string str)
		{
			Calculation* cal=nullptr;
			switch(str)
			{
			case "+"
				cal=new Add();
				break;
			case "-"
				cal=new Sub();
				break;
			case "/"
				cal=new Div();
				break;
			default:
				cout<<"请输入正确的运算符："<<endl;
				break;
			}
			return cal;
		}
};

int main()
{
	Calculation* cal = Factory::createCalculation('/');
	cal->numberA = 12;
	cal->numberB = 4;
	double result=0;
	try
	{
		result = cal->GetResult();
	}
	catch (exception* ex)
	{
		cout<<ex->what()<<endl;
	}
	cout << result;
	return 0;
}
```
# UML类图
![简单工程模式](/picture/simple_factory.png)
