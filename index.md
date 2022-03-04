# Welcome to myblogs
# 初识算法
## 排序算法
### 一、插入排序
插入排序（英语：Insertion Sort）是一种简单直观的排序算法。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，通常采用in-place排序（即只需用到 {\displaystyle O(1)} {\displaystyle O(1)}的额外空间的排序），因而在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。
过程演示：

![Insertion_sort_动图](D:\我的文件\Typora\Typora图片\Insertion_sort_动图.gif)	

```C
void insertion_sort(int arr[], int len){
    int i,j,temp;
    for (i=1;i<len;i++){
        temp = arr[i];
        for (j=i;j>0 && arr[j-1]>temp;j--){
            arr[j] = arr[j-1];
        }
        arr[j] = temp;
    }
}
```
### 二、选择排序
选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理如下。首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到所有元素均排序完毕。
过程演示：

![Selection_sort_动图](D:\我的文件\Typora\Typora图片\Selection_sort_动图.gif)	

![Selection-Sort-动图2](D:\我的文件\Typora\Typora图片\Selection-Sort-动图2.gif)	

```c
void selection_sort(int a[], int len) 
{
    int i,j,temp;
    for (i = 0 ; i < len - 1 ; i++) 
    {
        int min = i;                  // 记录最小值，第一个元素默认最小
        for (j = i + 1; j < len; j++)     // 访问未排序的元素
        {
            if (a[j] < a[min])    // 找到目前最小值
            {
                min = j;    // 记录最小值
            }
        }
        if(min != i)
        {
            temp=a[min];  // 交换两个变量
            a[min]=a[i];
            a[i]=temp;
        }
        /* swap(&a[min], &a[i]);  */   // 使用自定义函数交換,指针或者引用
    }
}
 
/*
void swap(int *a,int *b) // 交换两个变量
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
*/
```
### 三、冒泡排序
冒泡排序（英语：Bubble Sort）是一种简单的排序算法。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序（如从大到小、首字母从A到Z）错误就把他们交换过来。
过程演示：

![](D:\我的文件\Typora\Typora图片\Bubble_sort_动图.gif)		

```c
#include <stdio.h>
void bubble_sort(int arr[], int len) {
    int i, j, temp;
    for (i = 0; i < len - 1; i++)
        for (j = 0; j < len - 1 - i; j++)//len-1-i划重点
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
}
int main() {
    int arr[] = { 22, 34, 3, 32, 82, 55, 89, 50, 37, 5, 64, 35, 9, 70 };
    int len = (int) sizeof(arr) / sizeof(*arr);
    bubble_sort(arr, len);
    int i;
    for (i = 0; i < len; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
### 四、希尔排序
希尔排序，也称递减增量排序算法，是插入排序的一种更高效的改进版本。希尔排序是非稳定排序算法。
希尔排序是基于插入排序的以下两点性质而提出改进方法的：
+ 插入排序在对几乎已经排好序的数据操作时，效率高，即可以达到线性排序的效率

+ 但插入排序一般来说是低效的，因为插入排序每次只能将数据移动一位
  过程演示：

  ![Sorting_shellsort_anim](D:\我的文件\Typora\Typora图片\Sorting_shellsort_anim.gif)	
```c
void shell_sort(int arr[], int len) {
    int gap, i, j;
    int temp;
    for (gap = len >> 1; gap > 0; gap = gap >> 1)
        for (i = gap; i < len; i++) {
            temp = arr[i];
            for (j = i - gap; j >= 0 && arr[j] > temp; j -= gap)
                arr[j + gap] = arr[j];
            arr[j + gap] = temp;
        }
}
```
### 五、归并排序
把数据分为两段，从两段中逐个选最小的元素移入新数据段的末尾。
可从上到下或从下到上进行。
过程演示：

![Merge_sort_animation2](D:\我的文件\Typora\Typora图片\Merge_sort_animation2.gif)	

![Merge-sort-example-300px](D:\我的文件\Typora\Typora图片\Merge-sort-example-300px.gif)	

1. 迭代法
```c
int min(int x, int y) {
    return x < y ? x : y;
}
void merge_sort(int arr[], int len) {
    int* a = arr;
    int* b = (int*) malloc(len * sizeof(int));
    int seg, start;
    for (seg = 1; seg < len; seg += seg) {
        for (start = 0; start < len; start += seg + seg) {
            int low = start, mid = min(start + seg, len), high = min(start + seg + seg, len);
            int k = low;
            int start1 = low, end1 = mid;
            int start2 = mid, end2 = high;
            while (start1 < end1 && start2 < end2)
                b[k++] = a[start1] < a[start2] ? a[start1++] : a[start2++];
            while (start1 < end1)
                b[k++] = a[start1++];
            while (start2 < end2)
                b[k++] = a[start2++];
        }
        int* temp = a;
        a = b;
        b = temp;
    }
    if (a != arr) {
        int i;
        for (i = 0; i < len; i++)
            b[i] = a[i];
        b = a;
    }
    free(b);
}
```
2. 递归法
```c
void merge_sort_recursive(int arr[], int reg[], int start, int end) {
    if (start >= end)
        return;
    int len = end - start, mid = (len >> 1) + start;
    int start1 = start, end1 = mid;
    int start2 = mid + 1, end2 = end;
    merge_sort_recursive(arr, reg, start1, end1);
    merge_sort_recursive(arr, reg, start2, end2);
    int k = start;
    while (start1 <= end1 && start2 <= end2)
        reg[k++] = arr[start1] < arr[start2] ? arr[start1++] : arr[start2++];
    while (start1 <= end1)
        reg[k++] = arr[start1++];
    while (start2 <= end2)
        reg[k++] = arr[start2++];
    for (k = start; k <= end; k++)
        arr[k] = reg[k];
}
void merge_sort(int arr[], const int len) {
    int reg[len];
    merge_sort_recursive(arr, reg, 0, len - 1);
}
```
### 六、快速排序
在区间中随机挑选一个元素作基准，将小于基准的元素放在基准之前，大于基准的元素放在基准之后，再分别对小数区与大数区进行排序。
过程演示：

![Sorting_quicksort_anim](D:\我的文件\Typora\Typora图片\Sorting_quicksort_anim.gif)	

1. 迭代法
```c
typedef struct _Range {
    int start, end;
} Range;
Range new_Range(int s, int e) {
    Range r;
    r.start = s;
    r.end = e;
    return r;
}
void swap(int *x, int *y) {
    int t = *x;
    *x = *y;
    *y = t;
}
void quick_sort(int arr[], const int len) {
    if (len <= 0)
        return; // 避免len等於負值時引發段錯誤（Segment Fault）
    // r[]模擬列表,p為數量,r[p++]為push,r[--p]為pop且取得元素
    Range r[len];
    int p = 0;
    r[p++] = new_Range(0, len - 1);
    while (p) {
        Range range = r[--p];
        if (range.start >= range.end)
            continue;
        int mid = arr[(range.start + range.end) / 2]; // 選取中間點為基準點
        int left = range.start, right = range.end;
        do
        {
            while (arr[left] < mid) ++left;   // 檢測基準點左側是否符合要求
            while (arr[right] > mid) --right; //檢測基準點右側是否符合要求
 
            if (left <= right)
            {
                swap(&arr[left],&arr[right]);
                left++;right--;               // 移動指針以繼續
            }
        } while (left <= right);
 
        if (range.start < right) r[p++] = new_Range(range.start, right);
        if (range.end > left) r[p++] = new_Range(left, range.end);
    }
}
```
2. 递归法
```c
void swap(int *x, int *y) {
    int t = *x;
    *x = *y;
    *y = t;
}
void quick_sort_recursive(int arr[], int start, int end) {
    if (start >= end)
        return;
    int mid = arr[end];
    int left = start, right = end - 1;
    while (left < right) {
        while (arr[left] < mid && left < right)
            left++;
        while (arr[right] >= mid && left < right)
            right--;
        swap(&arr[left], &arr[right]);
    }
    if (arr[left] >= arr[end])
        swap(&arr[left], &arr[end]);
    else
        left++;
    if (left)
        quick_sort_recursive(arr, start, left - 1);
    quick_sort_recursive(arr, left + 1, end);
}
void quick_sort(int arr[], int len) {
    quick_sort_recursive(arr, 0, len - 1);
}
```
# 树
## 二叉索引树（树状数组）
1. 用途：常用于求前缀和
2. 
# 其他算法
## 1. 前缀和算法
例题：
题面：读取一个长度为n的由小写字母构成的字符串，接下来有m个询问，每个询问包括(l,r,c)，请你	     回答从第l个字符到第r个字符之间有字符类型为c的字符个数。
![屏幕截图 2021-11-25 210745](D:\我的文件\Typora\Typora图片\屏幕截图 2021-11-25 210745.png)

```c
#include<stdio.h>
int sum[100005][30]={0};
int main()
{
    int n,m,l,r,ans;
    char ch,c;
    while(scanf("%d %d",&n,&m)!=EOF){
        ans=0;
        for(int i=1;i<=n;i++){
            for(int j=0;j<26;j++){
                sum[i][j]=0;
            }
        }
        for(int i=1;i<=n;i++){
            scanf(" %c ",&ch);
             for(int j=0;j<26;j++){
                sum[i][j]=sum[i-1][j];
            }
           sum[i][ch-'a']=sum[i-1][ch-'a']+1;
        }
        for(int i=0;i<m;i++){
            scanf("%d %d %c",&l,&r,&c);
            ans=sum[r][c-'a']-sum[l-1][c-'a'];
            printf("%d\n",ans);
        }

    }
    return 0;
}
```
## 2. 高精度算法
### 1.高精度加法
```c++
// C = A + B, A >= 0, B >= 0
vector<int> add(vector<int> &A, vector<int> &B)
{
    if (A.size() < B.size()) return add(B, A);

    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ )
    {
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }

    if (t) C.push_back(t);
    return C;
}
```
### 2. 高精度减法
```C++
vector<int> sub(vector<int> &A,vector<int> &B)
{
	vector<int> C;
	int t=0;
	for(int i=0;i<A.size();i++)
	{
		t=A[i]-t;
		if(i<B.size())t-=B[i];
		C.push_back((t+10)%10);
		if(t<0)t=1;
		else t=0;
	}	
	while(C.size()>1&&C.back()==0)C.pop_back();
	return C;
 } 
```
###  3.高精度乘法
```C++
vector<int> mul(vector<int> &A,vector<int> &B)
{
	vector<int> C(A.size()+B.size(),0);
	for(int i=0;i<A.size();i++)
	{
		for(int j=0;j<B.size();j++)
		{
			C[i+j]+=A[i]*B[j];
			C[i+j+1]+=C[i+j]/10;
			C[i+j]%=10;
		}
	}
	while(C.size()>1&&C.back()==0)C.pop_back();
	return C;
}
```
### 4.高精度除法

## 3. 最大公因数(gcd函数)
### 1. gcd函数简介
大公因数（英语：highest common factor，hcf）也称最大公约数（英语：greatest common divisor，gcd）是数学词汇，指能够整除多个整数的最大正整数。而多个整数不能都为零。例如8和12的最大公因数为4。
#### 求两个整数最大公约数主要的方法：
1. 穷举法：分别列出两整数的所有约数，并找出最大的公约数。
2. 素因数分解：分别列出两数的素因数分解式，并计算共同项的乘积。
3. 短除法：两数除以其共同素因数，直到两数互素时，所有除数的乘积即为最大公约数。
4. 辗转相除法：两数相除，取余数重复进行相除，直到余数为0时，前一个除数即为最大公约数。
#### 相关介绍： https://blog.csdn.net/Ljnoit/article/details/104730787
### 2. gcd函数写法
1. while循环（常速）此段代码a、b可以为0
```C++
int gcd(int a,int b) 
{    
    int r;    
    while(b>0)
    {        
        r=a%b;        
        a=b;        
        b=r;    
    }    
    return a;
}
```
2. 三目运算符（较快）此段代码a、b可以为0
```C++
inline int gcd(int a,int b) 
{    
    return b>0 ? gcd(b,a%b):a;
}
```
3. 位运算（超快）此段代码a、b不能为0
```C++
inline int gcd(int a,int b) 
{    
    while(b^=a^=b^=a%=b);    
    return a;
}
```
4. if+while+位运算（超快）此段代码a、b可以为0
```C++
inline int gcd(int a,int b) 
{    
    if(b) while((a%=b) && (b%=a));    
    return a+b;
}
```
5. 辗转相除法（较快）此段代码a、b不能为0
```C++
inline int gcd(int a,int b)
{    
    if(a%b==0) 
    return b;        
    else return (gcd(b,a%b));
}
```
6. gcd库函数（较慢）此段代码a、b可以为0
```C++
#include <algorithm>
inline int gcd(int a,int b) {    
    return __gcd(a,b);
}
```
## 4.前缀和与差分
### 1. 一维前缀和
1. **题目**：
输入一个长度为 n 的整数序列。
接下来再输入 m 个询问，每个询问输入一对 l,r。
对于每个询问，输出原序列中从第 l 个数到第 r 个数的和。

2. **输入格式**：
第一行包含两个整数 n 和 m。
第二行包含 n 个整数，表示整数数列。
接下来 m 行，每行包含两个整数 l 和 r，表示一个询问的区间范围。

3. **输出格式**：
共 m 行，每行输出一个询问的结果。

4. **数据范围**
1≤l≤r≤n,
1≤n,m≤100000,
−1000≤数列中元素的值≤1000

5. **输入样例**
```C++
5 3
2 1 3 6 4
1 2
1 3
2 4
```
6. **输出样例**
```c++
3
6
10
```
**答案**
```c++
#include<bits/stdc++.h>
using namespace std;

const int N=100010;
int arr[N],S[N];

int main()
{
    int n,m,l,r;
    cin>>n>>m;
    S[0]=0;
    for(int i=1;i<=n;i++)
    {
        cin>>arr[i];
        S[i]=S[i-1]+arr[i];
    }
    while(m--)
    {
        cin>>l>>r;
        cout<<S[r]-S[l-1]<<endl;
    }
    return 0;
}
```

# 小笔记
### 1.打开输入输出文件
通过" freopen "函数可以省去反复输入测试数据验证代码的麻烦，很便利，但是要 ==记得在OJ上提交时注释掉== ，否则会出错。
关于r与w：

+ "r" :打开一个用于读取的文件。该文件必须存在。
+ "w" :创建一个用于写入的空文件。如果文件名称与已存在的文件相同，则会删除已有文件 	的内容，文件被视为一个新的空文件。
+ "a":追加到一个文件。写操作向文件末尾追加数据。如果文件不存在，则创建文件。
+ "r+":打开一个用于更新的文件，可读取也可写入。该文件必须存在。
+ "w+":创建一个用于读写的空文件。
+ "a+":打开一个用于读取和追加的文件。
```c
//读入
freopen("wenjian.txt","r",stdin);//stdin表示标准输入
//输出
freopen("wenjian.txt","w",stdout);//stdout表示标准输出

```
### 2.计算数的位数
```c
#include<cmath>//或者#include<math.h>
int num;//num是待测数字
int n;//n是位数
n=log10(num)+1;
```

# 题目及题解
## 一、OJ
## 二、洛谷
### 1.P1217 [USACO1.5]回文质数 Prime Palindromes(https://www.luogu.com.cn/problem/P1217)
#### 题目描述
因为 151 既是一个质数又是一个回文数（从左到右和从右到左是看一样的），所以 151 是回文质数。

写一个程序来找出范围 [a,b] (5 \le a < b \le 100,000,000)[a,b]5≤a<b≤100,000,000)( 一亿)间的所有回文质数。
#### 输入格式
第 1 行: 二个整数 a 和 b .
#### 输出格式
输出一个回文质数的列表，一行一个。
#### 输入输出样例
##### 输入#1
```c
5 500
```
##### 输出#1
```c

输出 #1复制
5
7
11
101
131
151
181
191
313
353
373
383
```
#### 解答（运用了深度搜索DPS）

```c
#include<iostream>
#include<cmath>
using namespace std;
int ISprime(int num);//判断是否为素数
int getnum(int size);//将数组转化为数字
void DFS(int now,int size);//深度搜索
int arr[15];
int a,b;//a、b是范围
int main()
{
    int x,y;//a、b是范围，x、y是位数
    cin>>a>>b;
    x=log10(a)+1;//计算位数的好方法
    y=log10(b)+1;//计算位数的好方法
    for(int i=x;i<=y;i++){
        if(i==1){//特判
            if(a<=5&&5<=b)cout<<5<<endl;
            if(a<=7&&7<=b)cout<<7<<endl;
            continue;
        }
        if(i==2){//特判
            if(a<=11&&11<=b)cout<<11<<endl;
            continue;
        }
        if(i%2==0)continue;//偶数位数的回文数字一定能被11整除
        if(i==9)break;//9位的只有100000000，不是
        //输出其他位数的回文质数
        DFS(1,i);
    }
    return 0;
}
void DFS(int now,int size)
{
    int flag=1;
    if(now<=(size+1)/2){
        for(int i=0;i<=9;i++){
            if(now==1&&(i==0||i%2==0))continue;//质数一定是奇数，
            //第一位不能是0
            arr[now]=i;
            DFS(now+1,size);//递归
            if(!flag)return;
        }
    }else{
        for(int i=now;i<=size;i++)arr[i]=arr[size+1-i];//12345
        int num=getnum(size);
        if(num<a)return;
        if(num>b){
            flag=0;
            return;
        }
        if(ISprime(num))cout<<num<<endl;
        return;
    }
}
int getnum(int size)
{
    int num=0;
    for(int i=1;i<=size;i++){
        num=num*10+arr[i];
    }
    return num;
}
int ISprime(int num)
{
    double t=sqrt(num);
    for(int i=2;i<=t;i++){
        if(num%i==0)return 0;
    }
    return 1;
}
```
## 三、其他
1. 打印杨辉三角
   解释：需加上第0行为1的情况，打印n+1行。

   ![QQ图片20211124233405](D:\我的文件\Typora\Typora图片\QQ图片20211124233405.png)

要求：严格按要求打印，保证美观（从没见过如此严格的格式化输出）。
 ==注意：第i（0<=i<=n）行第j个数的值a（第一个数除外）满足方程 a= a*(i-j+1)/j且(j<=i)==   
  ==a= a*(i-j+1)/j== 记住

```c
#include<stdio.h>
int main()
{
	int n,a;
	scanf("%d",&n);           
    for(int i=0;i<=n;i++){
        for(int d=2*n-2*i;d>0;d--)printf(" ");//打印行首的空格，这行很重要
        a=1;
        printf("%d   ",a);//要打印行的第一个值
        //打印行
        for(int j=1;j<=i;j++){
            a= a*(i-j+1)/j;//每一行的杨辉三角公式
            //保证每个数占四个格
            printf("%d",a);
            if(a<10)printf("   ");//三个空格
            else if(a>=10&&a<100)printf("  ");//两个空格
            else if(a>=100)printf(" ");//一个空格
        }
        printf("\n");
    }
	return 0;
}
```

# STL相关
## 一、容器
### 1. 栈（stack容器）
### 2. 队列（queue容器）
### 3. 链表（list容器）
### 4. 动态数组（vector容器）
### 5.hashtable(unordered_map)
一、成员函数
1. 迭代器
+ begin 　　返回指向容器起始位置的迭代器（iterator） 
+ end 　　   返回指向容器末尾位置的迭代器 
+ cbegin　   返回指向容器起始位置的常迭代器（const_iterator） 
+ cend 　　 返回指向容器末尾位置的常迭代器 
2. Capacity
+ size  　　 返回有效元素个数 
+ max_size  返回 unordered_map 支持的最大元素个数 
+ empty        判断是否为空 
3. 元素访问
+ operator[]  　　   访问元素 
+ at  　　 　　　　访问元素
4. 元素修改
+ insert  　　插入元素 
+ erase　　 删除元素 
+ swap 　　 交换内容 
+ clear　　   清空内容 
+ emplace 　构造及插入一个元素 
+ emplace_hint 按提示构造及插入一个元素
5. 操作
+ find 　　　　　　通过给定主键查找元素,没找到：返回unordered_map::end
+ count 　　　　　返回匹配给定主键的元素的个数 
+ equal_range 　　返回值匹配给定搜索值的元素组成的范围
6. Buckets
+ bucket_count 　　　返回槽（Bucket）数 
+ max_bucket_count    返回最大槽数 
+ bucket_size 　　　   返回槽大小 
+ bucket 　　　　　　返回元素所在槽的序号 
+ load_factor　　　　 返回载入因子，即一个元素槽（Bucket）的最大元素数 
+ max_load_factor 　  返回或设置最大载入因子 
+ rehash　　　　　　 设置槽数 
+ reserve 　　　　　  请求改变容器容量

二、例题
