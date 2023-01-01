1. lambda函数
名称lambda来自lambda calculus——一种定义和应用函数的数学系统。这个系统让用户能够使用匿名函数——即无需给函数命名。
比如: [](int x) {return x % 3 == 0;}
对比：bool compare3(int x){return x % 3 == 0;}
差别有两个：1. 使用[]代替了函数名； 2. 没有声明返回类型。
返回类型相当于使用decltyp根据返回值推断得到的，如果lambda不包含返回语句，推断出来的返回类型将为void。
根据C++ primer plus书中第663页中的例子来看:
count3 = std::count_if(numbers.begin(),numbers.end(),[](int x){return x % 3 == 0;});
即用整个lambda表达式替换函数指针或者函数符构造函数。且仅当lambda表达式完全由一条返回语句组成时，自动类型推断才管用，否则，需要使用新增的返回类型后置语法:
[](double x)->double{int y = x; return x - y;} // return type is double

为何使用lambda：
即让定义位于使用的地方附近会很有用，这样则无需翻阅多页的源代码。另外，如果需要修改代码，涉及的内容都将在附近；而剪切并粘贴代码以便在其他地方使用时，涉及的内容也是在一起的。
从这种角度来看,lambda是理想的选择，因为其定义和使用是在同一个地方进行的，而函数是最糟糕的选择，因为不能在函数内部定义其他函数，因此函数的定义和使用可能离使用它的地方很远。
函数符是一个不错的选择，因为可以在函数内部定义类(包含函数符类)，因此定义离使用地点可以很近。
从简洁的角度看，函数符代码比函数和lambda代码更繁琐。
比如当需要使用同一个lambda两次：
count1 = std::count_if(n1.begin(), n1.end(), [](int x){return x % 3 == 0;});
count2 = std::count_if(n2.begin(), n2.end(), [](int x){return x % 3 == 0;});
但并非必须编写lambda两次，可以给lambda指定一个名称，并且使用该名称两次：

auto mod3 = [](int x){return x % 3 == 0;};
count1 = std::count_if(n1.begin(),n1.end(),mod3);
count2 = std::count_if(n2.begin(),n2.end(),mod3);

甚至可以像常规函数一样使用有名称的lambda:

bool result = mod3(z);

lambda还有一些额外的功能。具体地说，lambda可访问作用域内的任何动态变量;要捕获要使用的变量，可将其名称放在中括号内。
如果只指定了变量名，如[z]，将按值访问变量；如果在名称前面加上&，如[&count]，将按引用访问变量。[&]让用户能够按引用访问所有动态变量，而[=]则可以按值访问所有动态变量，也可以混合使用。


to do
函数符号，函数指针以及lambda之间的相对效率；
