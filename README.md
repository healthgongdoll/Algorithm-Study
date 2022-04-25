# Algorithm-Study

This is Jay Chung's Algorithm Study 

## Recursion

#### Q. Determine if the number n is 2^n

```
class Solution {
    public boolean isPowerOfTwo(int n) {
       
        // 2^0 case
        if(n == 1){
            return true;
        }
        
        //check other case (number is odd)
        if(n % 2 != 0 || n == 0){
            return false;
        }
        
        return isPowerOfTwo(n/2);
    }
    
}
```

#### Q. Fibonacci Number 

Fibonacci Sequence is F(0), F(1) = 1 </br>
F(n) = F(n-1) + F(n-2)

```
class Solution {
    public int fib(int n) {
        
        if( n == 0){
            return 0;
        }
        if(n == 1){
            return 1;
        }
        
        return fib(n-1) + fib(n-2);
    }
}
```

#### Q. Binary Search Recursion

Binary Recursion basic logic is that </br>
Binary Search only available on **Sorted Array** </br>
There is three pointer Left, Right, Mid. Left is setted to be 0 and Right is setted to be Array.length-1. </br>
If target is bigger than Mid set Left as Mid+1 , If target is smaller than Mid set Right as Mid-1. </br>
Since it is recursive method, each condition must search recursively. </br>

```
class Solution {
    public int search(int[] nums, int target) {
        return bsearch(nums, 0, nums.length-1, target);
    }
    
    public int bsearch(int[] nums, int l, int r, int target)
    {
       int mid = (l+r) /2;
        if(l>r)
        {
            return -1;
        }
        if(target == nums[mid])
        {
            return mid;
        }
        if(target < nums[mid])
        {
            return bsearch(nums, l, mid - 1, target);
        }
        
        if(target > nums[mid])
        {
            return bsearch(nums,mid+1, r, target);
        }
        
        return 0;
    }
}
```



