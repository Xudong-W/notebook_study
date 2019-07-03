1. noncoupyable类 和 copyable类
2. __thread  定义线程局部变量
3. static_cast, dynamic_cast
4. __builtin_expect(long exp,long e)     分支预测优化 ，返回值等于 第一个参数 exp
	与关键字if一起使用.首先要明确一点就是 if (value) 等价于 if (__builtin_expect(value, x)), 与x的值无关.
	e=1  if(LIKELY()) /表示大多数情况下if里面是真，程序大多数直接执行if里面的程序
	e=0  if(UNLIKELY()) /表示大多数情况if里面为假，程序大多数直接执行else里面的程序
5. static_assert(常量表达式，提示字符串)。做编译期间的断言，因此叫做静态断言
	如果第一个参数常量表达式的值为真(true或者非零值)，那么static_assert不做任何事情，否则会产生一条编译错误，错误位置就是该static_assert语句所在行，错误提示就是第二个参数提示字符串。
	assert是运行期断言，它用来发现运行期间的错误，不能提前到编译期发现错误，也不具有强制性，也谈不上改善编译信息的可读性，既然是运行期检查，对性能当然是有影响的，所以经常在发行版本中，assert都会被关掉；
	#error可看做预编译期断言，甚至都算不上断言，仅仅能在预编译时显示一个错误信息，它能做的不多，可以参与预编译的条件检查，由于它无法获得编译信息，当然就做不了更进一步分析了。
6. int backtrace(void **buffer, int size);
   char **backtrace_symbols(void *const *buffer, int size);	
   void backtrace_symbols_fd (void *const *buffer, int size, int fd)
   abi::__cxa_demangle：
	 该函数用与获取当前线程的调用堆栈,获取的信息将会被存放在buffer中,它是一个指针数组。参数 size 用来指定buffer中可以保存多少个void* 元素。函数返回值是实际获取的指针个数,

	 backtrace_symbols将从backtrace函数获取的信息转化为一个字符串数组. 参数buffer应该是从backtrace函数获取的数组指针,size是该数组中的元素个数(backtrace的返回值)，函数返回值是一个指向字符串数组的指针,它的大小同buffer相同.每个字符串包含了一个相对于buffer中对应元素的可打印信息.它包括函数名，函数的偏移地址,和实际的返回地址

     backtrace_symbols_fd与backtrace_symbols 函数具有相同的功能,不同的是它不会给调用者返回字符串数组,而是将结果写入文件描述符为fd的文件中,每个函数对应一行.它不需要调用malloc函数,因此适用于有可能调用该函数会失败的情况。
	 
	 backtrace可以在程序运行的任何地方被调用，返回各个调用函数的返回地址，可以限制最大调用栈返回层数。
	 在backtrace拿到函数返回地址之后，backtrace_symbols可以将其转换为编译符号，这些符号是编译期间就确定的
	 根据backtrace_symbols返回的编译符号，abi::__cxa_demangle可以找到具体地函数方法

7. std::is_same<int, pid_t>::value    判断类型是否一致,一致返回true
	std::decay