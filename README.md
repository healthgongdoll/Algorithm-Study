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
## Multiplication Divide and Conquer (Karatsuba Algoritm)

If we multiply two numbers

```
        4526
  x      347
  -------------
        31682
       181040
      1357800
 ---------------
      1570522
```

This will take O(n^2) -> Where n is number of digits </br>
To reduce more time complexity we use the Karatsuba Algorithm (Divide and Conquer) 

Logic of the algorithm:

```
x = 146123 , we divide this to a = 143 b = 123

x = a * 10^n/2 + b 

y = 352120, we divide this to c = 352, d = 120

y = c * 10^n/2 + d

x * y = (a * 10^n/2+b) (c * 10^n/2 + d) 
= (a * 10^n/2)(c * 10^n/2) + ad * 10^n/2 + bc * 10^n/2 + bd
= ac * 10^(2(n/2)) + (ad + bc) * 10^n/2 + bd
```
we can split them into two part and use the expression 

ac = karatsuba(a,c) </br>
bd = karatsuba (b,d) </br>
ad_plus_bc = karatsuba (a+b, c+d) - ac - bd  -> (a+b)(c+d) - ac - bd = (ac + ad + bc + bd) - ac - bd = ad + bc

Code Algorithm:

```
def karatsuba(x,y):
    if x < 10 or y < 10:
        return x * y
    else:
        n = max(len(str(x)), len(str(y)))
        half = n//2 
        a = x // (10 ** (half)) #left part of x 
        b = x % (10 ** (half)) # right part of x 
        c = y // (10 ** (half)) #left part of y 
        d = y % (10 ** (half)) # right part of y
        ac = karatsuba(a,c)
        bd = karatsuba(b,d) 
        ad_plus_bc = karatsuba(a+b, c+d)-ac-bd 
        return ac * (10 ** (2 * half)) + (ad_plus_bc * (10 ** half)) + bd
 ```
 
![image](https://user-images.githubusercontent.com/79100627/173430437-452a5799-1b0e-4a71-afb0-cc629c08f60f.png)

![image](https://user-images.githubusercontent.com/79100627/173430629-a58e141d-0efa-4637-987c-a5fecee98af4.png)

![image](https://user-images.githubusercontent.com/79100627/173430953-85771048-eb31-4afe-abe8-19cc19cc7ed1.png)

### Time Complexity 
![image](https://user-images.githubusercontent.com/79100627/173431047-fd4a6240-b604-4ad9-88ff-0ab47a5ea160.png)
![image](https://user-images.githubusercontent.com/79100627/173431134-e921ea4c-1582-45e7-832b-e6d9eab5c640.png)

## Linked List 

### LinkedList Reverse 

```
NULL -> 1 -> 2 -> 3 -> NULL

1. Step Set the Current Node as Head and Set the prev as NULL (First null )

NULL (Prev, Next) -> 1 (Head, Curr) -> 2 -> 3 -> NULL

2. Set Next pointer to the current's next 

NULL(Prev) -> 1 (Head, Curr) -> 2 (Next) -> 3 -> NULL

3. Set Current's Next as Prev 

NULL (Prev) <- 1 (Head, Curr) -> 2(Next) -> 3 -> NULL

4. Set prev as current 

NULL <- 1 (Head,Curr, Prev) -> 2(Next) -> 3 -> NULL

5. Set Current as next 

Null <- 1(Head, Prev) -> 2(Curr,Next) -> 3 -> NULL

Iterate 1 to 5 
```
## Sorting

### Counting Sort 

Couting sort is a sorting based on keys between specific range. It works by counting the number of objects having distinct key values (kind of hashing). Then do some arithmetic to calculate the position of each object in output sequence

- Counting sort makes assumption about the data, for example, it assumes that values are going to be in the range of 0 to 10 or 10 - 99 etc. Some other assumptions counting sort makes are input data will be all real numbers. 
- Like other algorithms this sorting is **not a comparison based algorithm** it hashes the value in a temporary count array and uses them for sorting. 
- It uses a temporary array making it a non In Place algorithm. 

```
[1,4,1,2,7,5,2]

Count each element in the given array and place the count at the appropriate index

i: 0 1 2 3 4 5 6 7 8 9
  [0,2,2,0,1,1,0,1,0,0]
  
 Modify the count array such that each element at each index stores the sum of previous counts 
 
 0, 0+2, 0+2+2, 0+2+2+0, 0+2+2+0+1,... 
 
 [0,2,4,4,5,6,6,7,7,7]
 
Rotate the array clockwise for one time 

1.
 [1,4,1,2,7,5,2]

i: 0 1 2 3 4 5 6 7 8 9
  [0,2,4,4,5,6,6,7,7,7]
  
Sorted Array:
We place the objects in their correct position and decrease the count by one 
i: 1 2 3 4 5 6 7
  [0,1,0,0,0,0,0]

2.
 [1,4,1,2,7,5,2]
 
i: 0 1 2 3 4 5 6 7 8 9
  [0,1,4,4,4,6,6,7,7,7]

Sorted Array:
i: 1 2 3 4 5 6 7
  [0,1,0,0,4,0,0]
  
3.
  [1,4,1,2,7,5,2]
  
i: 0 1 2 3 4 5 6 7 8 9
  [0,0,4,4,4,6,6,7,7,7]
 
Sorted Array:
i: 1 2 3 4 5 6 7
  [1,1,0,0,4,0,0]

4.
  [1,4,1,2,7,5,2]
  
 i: 0 1 2 3 4 5 6 7 8 9
  [0,0,3,4,4,6,6,7,7,7]
  
  Sorted Array:
i: 1 2 3 4 5 6 7
  [1,1,0,2,4,0,0]
  
  5.
   [1,4,1,2,7,5,2]
   
i: 0 1 2 3 4 5 6 7 8 9
  [0,0,3,4,4,6,6,6,7,7]
  
  Sorted Array:
i: 1 2 3 4 5 6 7
  [1,1,0,2,4,0,7]
  
  ...
  
  Final 
   [1,4,1,2,7,5,2]
   
i: 0 1 2 3 4 5 6 7 8 9
  [0,0,2,4,4,5,6,6,7,7]
  
  Sorted Array:
i: 1 2 3 4 5 6 7
  [1,1,2,2,4,5,7]
 
```
   
