# C++ sort()

><h2>底层原理
>
>`sort()并非只是普通的快速排序`，除了对普通的快速排序进行优化，它还结合了插入排序和堆排序。根据不同的数量级别以及不同情况，能自动选用合适的排序方法
>
><h2>使用方法</h2>
>
>1. sort函数包含在头文件<algorithm.h>中
>2. sort()函数可以对给定区间所有元素进行排序。它有三个参数`sort(begin, end, cmp)`
>3. 其中begin为指向待sort()的数组的第一个元素的指针，**end为指向待sort()的数组的最后一个元素的下一个位置的指针**，cmp参数为排序准则，**cmp参数可以不写，如果不写的话，默认从小到大进行排序**。如果我们想从大到小排序可以将cmp参数写为greater<int>()就是对int数组进行排序，当然<>中我们也可以写double、long、float等等。如果我们需要按照其他的排序准则，那么就需要我们自己定义一个bool类型的函数来传入。比如我们对一个整型数组进行从大到小排序：
>3. cmp为bool类型，可以比较结构体啊，多组关键字排序啊等等，只要**设定好cmp函数就行**