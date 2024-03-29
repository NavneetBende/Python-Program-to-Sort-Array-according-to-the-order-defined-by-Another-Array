Sort Array according to the order defined by Another Array
In this article, we will learn In this article, we will learn about Python Program to Sort Array according to the order defined by Another Array.

We have given two arrays A1[] and A2[], sort A1 in such a way that the relative order among the elements will be same as those are in A2. For the elements not present in A2, append them at last in sorted order.

Sort an array according to the order defined by another array in python
Here, we will discuss the following method for sorting the array according to the order that defined by another array.

Method 1 : Using Sorting and Binary searching.
Method 2 :  Using concept of hashing.
Let’s discuss above methods one by one in brief.

Method 1 :
Declare a temporary array temp of size m and copy the contents of arr1[] to it.
Declare another array visited[] and initialize all entries in it as false. visited[] is used to mark those elements in temp[] which are copied to arr1[].
Sort temp[] using any sorting technique
Declare the output index ind as 0.
Do following for every element of arr2[i] in arr2[]
Binary search for all occurrences of arr2[i] in temp[], if present then copy all occurrences to arr1[ind] and increment ind. Also mark the copied elements visited[]
Copy all unvisited elements from temp[] to arr1[]
Method 1 : Code in Python
def first(arr, low, high, x, n) :
    if (high >= low) :
        mid = low + (high - low) // 2; 
        if ((mid == 0 or x > arr[mid-1]) and arr[mid] == x) :
            return mid
        if (x > arr[mid]) :
            return first(arr, (mid + 1), high, x, n)
        return first(arr, low, (mid -1), x, n)
         
    return -1
     

def sortAccording(A1, A2, m, n) :
   
    temp = [0] * m
    visited = [0] * m
     
    for i in range(0, m) :
        temp[i] = A1[i]
        visited[i] = 0
  
    # Sort elements in temp
    temp.sort()
     
    ind = 0   
  
    for i in range(0, n) :
         
        f = first(temp, 0, m-1, A2[i], m)
  
        if (f == -1) :
            continue
  
        j = f
        while (m>j and temp[j]== A2[i]) :
            A1[ind] = temp[j];
            ind = ind + 1
            visited[j] = 1
            j = j + 1
     
    for i in range(0, m) :
        if (visited[i] == 0) :
            A1[ind] = temp[i]
            ind = ind + 1
             

def printArray(arr, n) :
    for i in range(0, n) :
        print(arr[i], end = " ")
    print("")
     
  
# Driver program to test above function.
arr1 = [ 20, 1, 20, 5, 7, 1, 9, 39, 6, 18, 18 ];
arr2 = [ 20, 1, 18, 39 ];
m = len(arr1)
n = len(arr2)
sortAccording(arr1, arr2, m, n)
printArray(arr1, m)
Related Pages
Determine can all numbers of an array be made equal

Finding Minimum sum of absolute difference of given array

Replace each element of the array by its rank in the array

Finding equilibrium index of an array

Rotation of elements of array- left and right 

Output
20 20 1 1 18 18 39 5 6 7 9
Output
20 20 1 1 18 18 5 6 7 9 39
Method 2 :
In this method we will use the concept of hashing to sort the array arr1 on the basis of the order of arr2 elements.

Method 2 : Code in Python
from collections import Counter

def solve(arr1, arr2):
    res = []
    
    f = Counter(arr1)
     
    for e in arr2:
       
        res.extend([e]*f[e])
         
        f[e] = 0
         
    rem = list(sorted(filter(lambda x: f[x] != 0, f.keys())))
     
    for e in rem:
        res.extend([e]*f[e])
         
    return res
 
 
# Driver Code
arr1 = [ 20, 1, 20, 5, 7, 1, 9, 39, 6, 18, 18 ];
arr2 = [ 20, 1, 18, 39 ];
print(*solve(arr1, arr2))
Output
20 20 1 1 18 18 39 5 6 7 9
