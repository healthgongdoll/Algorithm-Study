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





