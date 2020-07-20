# Array questions in JAVA
## 1. To Reverse an Array
> ### Method 1 (Using another array)
### `1. Take inputs`
### `2. Send the input to `reverse`  function and send the array` 
### `3. Set the values in the duplicate array from last index to first index in the duplicate array`

```java 
class Solution { 
  
    /* function that reverses array and stores it  
       in another array*/
    static void reverse(int a[], int n) 
    { 
        int[] b = new int[n]; 
        int j = n; 
        for (int i = 0; i < n; i++) { 
            b[j - 1] = a[i]; 
            j = j - 1; 
        } 
  
        /*print the reversed array*/
        System.out.println("Reversed array is: \n"); 
        for (int k = 0; k < n; k++) { 
            System.out.println(b[k]); 
        } 
    } 
  
    public static void main(String[] args) 
    { 
        int [] arr = {10, 20, 30, 40, 50}; 
        reverse(arr, arr.length); 
    } 
} 
```
>### Method 2 (Swapping using temp variable)
### `1. take inputs`
### `2. Send inputs to `reverse` method`
### `3. swap first element with last using temp variable`
```java
public class arrayReverse { 
  
    /*function swaps the array's first element with last element,  
      second element with last second element and so on*/
    static void reverse(int a[], int start, int end) 
    { 
        int i, k, t; 
        for (i = 0; i < n / 2; i++) { 
            t = a[i]; 
            a[i] = a[n - i - 1]; 
            a[n - i - 1] = t; 
        } 
  
        /*printing the reversed array*/
        System.out.println("Reversed array is: \n"); 
        for (k = 0; k < n; k++) { 
            System.out.println(a[k]); 
        } 
    } 
  
    public static void main(String[] args) 
    { 
        int [] arr = {10, 20, 30, 40, 50}; 
        reverse(arr,0, arr.length-1); 
    } 
}
```