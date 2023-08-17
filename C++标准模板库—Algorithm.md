# ***C++标准模板库—Algorithm***

```c++
//通用容器操作方法：
---------
//构造函数
ContType<T> C;            		//创建一个空容器
ContType<T> C(nSIze);        	//创建一个含有 nSize 个默认元素的容器
ContType<T> C(nSize, Value);    //创建一个含有 nSize 个值为 Value 的元素的容器
ContType<T> C1(C2);  			//复制一个同类型容器
ContType<T> C(first, last);      //复制[first,last)范围内的元素到新容器中
//判断函数
C.empty();            			//判断容器是否为空
C1==C2;           				//判断c1是否等于c2
C1=C2;							//将c2的值赋给c1
//访问函数
C.begin();        				//正向迭代器，指向第一个元素
C.end();         				//正向迭代器，指向最后一个元素的下一位置
C.size();      					//返回容器当value前存储的元素数量
C.max_size();  					//返回容器能容纳的最大元素数量
//操作函数
C.clear();						//清空容器value
C.insert(it, value);			//在it指向的位置插入值为 Value的元素
C.insert(it,num,value);			//在it指向的位置插入num个值为value的元素
C.insert(it,fisrt,last);		//在it指向的位置插入地址为[first,end)区间内的所有元素

C.erase(it,nSize);				//删除从地址it开始的 nSize 个元素
C.erase(it);					//删除该迭代器指向的元
C.erase(first,last);			//删除迭代器[first,last)区间的元素
```

## 一、vector(向量)					py-list数组

### · 作为元素个数不确定时节省空间的数组使用

### · 不用指针，实现邻接表

```c++
//初始化
#include<vector>
vector<typename> vi;			//创建向量
vector<vector<int>> vi;			//创建元素为向量的向量
vector<typename> vi[maxn];		//创建元素为向量的数组
vector<typename>::iterator it;	//创建该向量的迭代器
【 允许使用 it+整数 的写法，不支持it<vi.end()写法，应用it!=vi.end() 】
```

```c++
vi.push_back(i);				//结尾加入元素i
vi.pop_back();					//删去结尾元素
【结尾进行增删操作，迭代器进行访问、插入操作】
```

## 二、string(字符类)				py-string字符串

```c++
//初始化
#include<string>
string str;						//创建字符类，只能用cin/cout进行输入输出
string str=" ";					//创建时可直接初始化
string::iterator it;			//创建该字符类的迭代器
【 允许使用 it+整数 的写法，不支持it<str.end()写法，应用it!=str.end() 】
```

```c++
operator+=						//直接使用+进行两个string类的连接【strcat】
compare operator				//直接使用比较运算符进行比较大小【strcmp】
str.size();						//得到长度【strlen】
str.substr(it,len);				//得到it位置长度为len的子串
string::npos					//string类中的常数，值为-1
str.find(str2);					//返回str2第一次出现的位置,若无则返回string::npos
str.find(first,end,value);		//返回[first,end)中value第一次出现的位置【map，set，multimap，multiset】
```

## 三、list(双向循环链表)

### · 同链表一样，不支持下标访问，访问效率低，但插入效率高

```c++
//初始化
#include<list>
list<typename> li;
list<typename>::iteratoe it;
【 允许使用 it++ 的写法，不支持it<li.end()写法，应用it!=li.end() 】
```

```c++
li.push_back(x);			//表尾插入x元素
li.push_front(x);			//表头插入x元素
li.pop_back();				//删除表尾元素
li.pop_front();				//删除表头元素
li.sort();					//只能使用list类中的排序，速度慢，涉及排序尽量使用vector
```

## 四、set(集合)						py-set集合

### · 内部以红黑树实现，自动去除重复元素，并进行哈希排序

### · [C++11]：unordered_set以散列代替红黑树，只去重不排序，速度更快

```c++
//初始化
#include<set>
set<typename> st;				//创建一个集合
set<typename>::iterator it;		//创建一个集合的迭代器
【 允许使用 it++ 的写法，不支持it<st.end()写法，应用it!=st.end() 】
```

```c++
st.insert(x);					//插入元素x，并自动进行排序
```

## 五、queue(队列)	

### · 先进先出，用于实现广度优先搜索(bfs)

### · 双端队列(deque)，优先队列(priority_queue)

### · deque(双端队列)：两端皆可以进行插入/删除操作，有迭代器

### · 不可从中间插入

```c++
//初始化
#include<queue>
queue<typename> qe;				//创建一个先进先出的队列
【 无迭代器，只能通过队首队尾进行访问和操作 】
```

```c++
qe.front()/back();				//查询队首/队尾元素
qe.pop()/push(x);				//首元素出队/元素x入队【无法从中间插入元素】
【 使用front和pop之前一定要先用empty判定是否为空队 】
```

## 六、priority_queue(优先队列)

### · 队尾插入元素后，自动由堆实现优先级排序，队首为优先级最高

### · 常用解决贪心问题，或以堆的本质对算法进行优化

```c++
//初始化
#include<queue>
priority_queue<typename> pq;									//创建一个优先队列
priority_queue<typename,vector<typename>,less<typename>> pq;	//等价上一个
【 第二个参数为承载底层实现堆的容器，第三个参数为优先级参数，可结构体里面对"<"进行"友元重载运算符"，进行优先排序（与cmp相反） 】
```

```c++
无front()/back(),只有top()访问队首
pq.top();						//查询队首元素（相当于front）
pq.pop()/push(x);				//首元素出队/元素x入队
【 使用top之前一定要先用empty判定是否为空队 】
```

## 七、stack(栈)

### · 先进后出，用于实现深度优先搜索(dfs)

### · 模拟递归，防止递归爆栈出错

```c++
//初始化
#include<stack>
stack<typename> sc;
【 无迭代器，只能通过栈顶进行访问和操作 】
```

```c++
sc.top();						//查询栈顶元素
sc.push(x);						//将元素x入栈
sc.pop();						//删除栈顶元素
【 使用top和pop之前一定要先用empty判定是否为空栈 】
```

## 八、map(映射)						py-dic字典

### · multimap：允许一个键对应多个值，即允许多个相同键同时存在 

### · [C++11]：unordered_set以散列代替红黑树，只去重不排序，速度更快

```c++
//初始化
#include<map>
map<typename1,typename2> mp;				//创建一个typename1-typename2的键值对的线性结构
map<typename1,typename2>::iterator it;		//创建一个映射的迭代器
【 map与set一样由红黑树实现，以键进行哈希排序自动排序，map中键必须是唯一的 】
```

```c++
it->first;						//通过迭代器访问键
it->second;						//通过迭代器访问值
mp[key]=value;					//已有该键则修改value，无该键则插入该键值对，也可insert插入pair
```

## 九、pair(键值)

### · 底层由结构体实现，作为底层实现map

```c++
//初始化
#include<utility> / #include<map>				//map中包含pair
pair<typename1,typename2> p(data1,data2);		//直接进行初始化
pair<typename1,typename2> p;
make_pair(data1,data2);							//同上
```

```c++
p->first;						//访问键
p->second;						//访问值
p1>p2;							//同类型pair比较，先比较键，键相同再比较值
```



# Algorithm		#include<algorithm>

## 一、max()、min()、abs()、max_element()、min_element()

```c++
max/min(a,b);	max/min({a,b,c});	//返回最大/最小值
abs(a)								//返回整数a的绝对值
【浮点数需要用fabs()，并导入cmath库】
max/min_element(arr,arr+n);			//返回地址[arr,arr+n)的最大/最小值的地址【加*进行访问】
```

## 二、swap()、reverse()、sort()

```c++
swap(a,b);							//将任意相同的结构、容器a和b进行交换
reverse(arr,arr+n);					//将地址[arr,arr+n)的结构、容器进行反转
sort(arr,arr+n,cmp);				//将地址[arr,arr+n)的结构、容器进行cmp排序
【 cmp无时默认为降序，升序为greater<typename>()，降序为less<typename>() 】
【 cmp为自定义bool函数时，bool cmp(typename data1,typename data2),若判定为false则data1与data2进行交换，data2排在data1之前，cmp常有二级排序】
```

## 三、fill()、count()、__gcd()

```c++
fill(arr,arr+n,value);				//将地址[arr,arr+n)的结构、容器进行填充为value
count(arr,arr+n,value);				//将地址[arr,arr+n)的结构、容器进行查询value的次数
__gcd(a,b);							//返回a和b的最大公因数
```

## 四、find()、lower_bound()、upper_bound()

```c++
find(arr,arr+n,value);		//将地址[arr,arr+n)的结构、容器进行查询value位置，若无则返回n+1的地址
lower_bound(arr,arr+n,value);	//将地址[arr,arr+n)的结构、容器进行查找第一个大于value的位置
upper_bound(arr,arr+n,value);	//将地址[arr,arr+n)的结构、容器进行查找第一个大于等于value的位置
```

## 五、next_permutation()、pre_permutation()

```c++
next_permutation(arr,arr+n);//将地址[arr,arr+n)的结构、容器进行下一次全排列【有序】，若无返回NULL
pre_permutation(arr,arr+n); //将地址[arr,arr+n)的结构、容器进行上一次全排列【有序】，若无返回NULL
```

## 六、set_intersection()、set_union()、set_difference()

```c++
交集：set_intersection(a,a+n,b,b+m,inserter(vi,vi.begin())); //将两个数组交集赋给容器vi
	set_intersection(v1.begin(),v1.end(),v2.begin(),v2.end(),inserter(vi,vi.begin()));
															//将两个容器交集赋给容器vi
并集：set_union(a,a+n,b,b+m,inserter(vi,vi.begin())); //将两个数组并集赋给容器vi
	set_union(v1.begin(),v1.end(),v2.begin(),v2.end(),inserter(vi,vi.begin()));
															//将两个容器并集赋给容器vi
差集：set_difference(a,a+n,b,b+m,inserter(vi,vi.begin())); //将两个数组差集赋给容器vi
	set_difference(v1.begin(),v1.end(),v2.begin(),v2.end(),inserter(vi,vi.begin()));
															//将两个容器差集赋给容器vi
inserter(c,c.begin()）为插入迭代器
【此函数接受第二个参数，这个参数必须是一个指向给定容器的迭代器。元素将被插入到给定迭代器所表示的元素之前】
```

