Given a rod of length n inches and an array of prices that contains prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces. For example, if length of the rod is 8 and the values of different pieces are given as following, then the maximum obtainable value is 22 (by cutting in two pieces of lengths 2 and 6)

length   | 1   2   3   4   5   6   7   8  
--------------------------------------------
price    | 1   5   8   9  10  17  17  20


## Recursive top-down implementation 
```
#include <limits>
#include <algorithm>
#include <iostream>

template <typename T> auto  cut_rod(T p[],int n)
{
if(n==0) return 0;
auto q=std::numeric_limits<T>::min();
for(int i=0;i<n;i++)
{
    q=std::max(q,p[i]+cut_rod(p,n-i-1));
}
return q;

}

int main()
{
    int arr[] = {1, 5, 8, 9, 10, 17, 17, 20};
    int size = sizeof(arr)/sizeof(arr[0]);
    std::cout<<"Maximum Obtainable Value is "<< cut_rod(arr, size)<<std::endl;
    
    return 0;
}
```
