# C++ lower_bound 和 upper_bound

><h2>底层原理</h2>
>lower_bound( )和upper_bound( )都是利用**二分查找**的方法在一个排好序的数组中进行查找的
>
><h2>总述</h2>
>
>lower_bound()跟upper_bound()返回迭代器类型，前两个参数也是迭代器类型，第四个参数的类型是bool类型跟sort（）的差不多，默认按升序排列
>
><h2>使用方法</h2>
>
>1. lower_bound( begin,end,num)：从数组的begin位置到end-1位置二分查找第一个**大于或等于**num的数字，找到返回该数字的地址，不存在则返回end。通过返回的地址减去起始地址begin,得到找到数字在数组中的下标。（**lower_bound - 1即为最后一个小于num的值的下标的**）
>
>2. upper_bound( begin,end,num)：从数组的begin位置到end-1位置二分查找第一个**大于**num的数字，找到返回该数字的地址，不存在则返回end。通过返回的地址减去起始地址begin,得到找到数字在数组中的下标。(**upper_bound - 1即为最后一个小于等于num值的下标**)
>
>3. lower_bound( begin,end,num,greater() ):从数组的begin位置到end-1位置二分查找第一个小于或等于num的数字，找到返回该数字的地址，不存在则返回end。通过返回的地址减去起始地址begin,得到找到数字在数组中的下标。
>
>4. upper_bound( begin,end,num,greater() ):从数组的begin位置到end-1位置二分查找第一个小于num的数字，找到返回该数字的地址，不存在则返回end。通过返回的地址减去起始地址begin,得到找到数字在数组中的下标。
>
><h2>注意:第一点跟第二点用得多一些</h2>
>
>