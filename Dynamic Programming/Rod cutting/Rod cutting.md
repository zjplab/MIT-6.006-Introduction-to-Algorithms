Given a rod of length n inches and an array of prices that contains prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces. For example, if length of the rod is 8 and the values of different pieces are given as following, then the maximum obtainable value is 22 (by cutting in two pieces of lengths 2 and 6)


length   | 1   2   3   4   5   6   7   8  

----------------------------------------
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
## Memoized Rod cuttting 
```
import sys

def cut_rod(price,n):
    r=[-sys.maxsize-1]*(n+1)
    #or r=[-sys.maxsize-1 for x in range(0,n+1)]
    return cut_rod_aux(price,n,r)

def cut_rod_aux(price,n,r):
    if r[n]>=0 return r[n] 
    if n==0 q=0
    else:
        q=-sys.maxize-1
        for i in range(n):
            q=max(q,price[i]+cut_rod_aux(price,n-i-1,r)) # n-1-i goes from n-1 to 0, n values, plus the inital value n, so you can see   it is meaningful to set an array r of (n+1) size 
                                                         
    r[n]=q
    return q 
```    

## Bottomed-up rod cutting 
```
import sys

def cut_rod_bottom_up(price,n):
    r=[-sys.maxsize-1]*(n+1)
    r[0]=0
    for j in range(1,n+1):
        q=-sys.maxsize-1
        for i in range(0,j):
            q=max(q,price[i]+r[j-i-1])
        r[j]=q
    return r[n]        
```
## Bottomed-up rod cutting to show the choices
```
import sys

def cut_rod_bottom_up(price,n):
    r=[-sys.maxsize-1]*(n+1)
    s=[-1]*n
    r[0]=0
    for j in range(1,n+1):
        q=-sys.maxsize-1
        for i in range(0,j):
            if q<price[i]+r[j-1-i]:
                q=price[i]+r[j-1-i]
                s[j-1]=i
        r[j]=q
    return r,s 

def print_cut_rod_solution(price,n):
    (r,s)=cut_rod_bottom_up(price,n)
    while n>0:
        print("{}\n".format(s[n-1)+1))
        n-=s[n-1]+1

```
