```
// C++ 11 code 
#include <limits>
#include <tuple>
#include <cstdio>
template <typename T> auto find_max_crossing_array(T A[],int low, int mid, int high)
{
T leftsum=std::numeric_limits<T>::min();
T sum=0;
int maxleft,maxright;
for(int i=mid;i>=low;i--)
{
 sum+=A[i];
 if(sum>leftsum){
     maxleft=i;
     leftsum=sum;
 }
}// for ends
T rightsum=std::numeric_limits<T>::min();
sum=0;
for(int j=mid+1;j<=high;j++)
{
    sum+=A[j];
    if(sum>rightsum)
    {
        rightsum=sum;
        maxright=j;
    }// if 
}//for
return std::make_tuple(maxleft,maxright,leftsum+rightsum);
}

template <typename T> auto find_max_subarray(T A[],int low, int high)
{
    if(low==high) return std::make_tuple(low,high,A[low]); //base case 
    int mid=low+(high-low)/2;
    int left_low,left_high;
    T left_sum;
    std::tie(left_low,left_high,left_sum)=find_max_subarray(A,low,mid);
    
    int right_low, right_high;
    T right_sum;
    std::tie(right_low, right_high, right_sum)=find_max_subarray(A,mid+1,high);
    
    int cross_low, cross_high;
    T cross_sum;
    std::tie(cross_low, cross_high, cross_sum)=find_max_crossing_array(A,low,mid,high);
    if(left_sum>=right_sum && left_sum>=cross_sum)
        return std::make_tuple(left_low,left_high,left_sum);
    else if(right_sum>=left_sum && right_sum>=cross_sum)
        return std::make_tuple(right_low,right_high,right_sum);    
    else 
        return std::make_tuple(cross_low,cross_high,cross_sum);
}

int main()
{
int arr[] = {2, 3, 4, 5, 7};
int n = sizeof(arr)/sizeof(arr[0]);
int left,right,max_sum;
std::tie(left,right,max_sum) = find_max_subarray(arr, 0, n-1);
std::printf("Maximum contiguous sum is %d, max_left is %d, max_right is %d", max_sum, left, right);

return 0;
}


```
