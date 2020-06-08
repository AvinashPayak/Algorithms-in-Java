# Algorithms in JAVA
## 1. Array Rotation using Reversal Algorithm
### To right rotate the array by d elements using reversal algorithm

```java
// To left rotate make d = n-d at line 14 and 15

import java.util.Scanner;

class Solution{
    public static void main(String[] args){
        Scanner pp = new Scanner(System.in);
        int n = pp.nextInt();
        int d = pp.nextInt();
        int[] nums = new int[n];
        for(int i = 0; i<n ; i++){
            nums[i] = pp.nextInt();
        }

        reverse(nums , 0 , n-1);
        reverse(nums, 0, d-1);
        reverse(nums, d, n-1);

        for(int i = 0; i<n ; i++){
            System.out.print(nums[i] +" ");
        }

        pp.close();
    }

    public static void reverse(int[] nums, int start, int end){

        while(start<end){
            int temp = nums[start];
            nums[start]= nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

## 2. Sieve Of Eratosthenes
### To Find prime numbers
```java
import java.util.Scanner;
class Solution{
    public static void main(String[] args){
        Scanner pp = new Scanner(System.in);
        int n= pp.nextInt();
        int ar[] = new int[n];
        for(int i = 2; i*i<n;i++){
            if(ar[i] == 0){
                for(int j = i;j*i<n;j++){
                    ar[j*i] = 1;
                }
            }
        }
        int count = 0;
        for(int i = 2;i<n;i++){
            if(ar[i] == 0){
                count++;
            }
        }
        System.out.print(count);
        
        pp.close();
    }
}
```

## 3. Merge Sort

```java
import java.util.Scanner;
public class merge{
    public static void main(String[] args){
        Scanner pp=new Scanner(System.in);
        int n =pp.nextInt();
        int[] ar=new int[n];
        //take array input
        for(int i=0;i<n;i++){
            ar[i]=pp.nextInt();
        }
        mergesort(ar);
        //print sorted array
        for(int i=0;i<n;i++){
        System.out.print(ar[i]+" ");
        }
        pp.close();
    }
    static int[] mergesort(int ar[]){
        int n=ar.length;
        //if length less than 2 then return array
        if(n<2){
            return ar;
        }
        else {
        int mid=(int)n/2;
        int[] l=new int[mid];
        int[] r=new int[n-mid];

        //left array insertion
        for(int i=0;i<mid;i++){
            l[i]=ar[i];
        }
        
        //right array insertion
        for(int i=0;i<n-mid;i++){
            r[i]=ar[mid+i];
        }

        //divide further
        mergesort(l);
        mergesort(r);
        merges(l,r,ar,mid,n);
        return ar;
    }
    }
    static int[] merges(int l[],int r[],int[] ar,int mid,int n){
        int i=0;
        int j=0;
        int k=0;
        while(i<mid && j<n-mid){
            if(l[i]<r[j]){
                ar[k]=l[i];
                i++;
            }
            else{
                ar[k]=r[j];
                j++;
            }
            k++;
        }
        while(i<mid){
            ar[k]=l[i];
            i++;
            k++;
        }
        while(j<n-mid){
            ar[k]=r[j];
            j++;
            k++;
        }
        return ar;
    }
}
```
## 4. Knuth Morris Patt algorithm (String Manipulation)

```java
import java.util.*;
class KMP {
    public static void main(String[] args){
        Scanner pp= new Scanner(System.in);
        String txt = pp.next(); //text 
        String pat = pp.next(); //pattern
        int N = txt.length(); 
        int M = pat.length(); 
        int lps[] = new int[M]; // LPS table (Longest proper prefix which is also suffix)
        int j = 0;  //to traverse pattern
        computeLPSArray(pat, M, lps); 
        int i = 0;  //to traverse text
        while (i < N) { 
            if (pat.charAt(j) == txt.charAt(i)) { 
                j++; 
                i++; 
            } 
            if (j == M) { 
                System.out.println("Found pattern " + "at index " + (i - j)); 
                j = lps[j - 1]; 
            } 
            else if (i < N && pat.charAt(j) != txt.charAt(i)) { 
                if (j != 0) 
                    j = lps[j - 1]; 
                else
                    i = i + 1; 
            } 
        } 
        pp.close();
    }

    static void  computeLPSArray(String pat, int M, int[] lps){
        int len = 0; 
        int i = 1; 
        lps[0] = 0; 
        while (i < M) { 
            if (pat.charAt(i) == pat.charAt(len)) { 
                len++; 
                lps[i] = len; 
                i++; 
            } 
            else // (pat[i] != pat[len]) 
            {            
                if (len != 0) { 
                    len = lps[len - 1];   // Also, note that we do not increment i here 
                } 
                else // if (len == 0) 
                { 
                    lps[i] = len; 
                    i++; 
                } 
            } 
        } 
    }
}
```

## 5. Stairs and Ladders Algorithm (Dynamic Programming)
### To find number of minimum jumps required to reach end of an array. Each element of array represents max number of jumps it can make.

```java
import java.util.Scanner;
class Solution {
    public static void main(String[] args) {
        Scanner pp = new Scanner(System.in);
        int n = pp.nextInt();
        int[] nums = new int[n];
        for(int i =0; i<n;i++){
            nums[i]=pp.nextInt();
        }

        int ladder = nums[0];
        int stairs = nums[0];
        int jump = 1;
        if(nums.length == 1 || nums[0] == 0){
            System.out.println(0);
        }
        for(int level = 1; level<nums.length;level++){
            if(level == nums.length - 1){
                System.out.println(jump);
            }
            if(level + nums[level]>ladder){
                ladder = nums[level] + level;
            }
            stairs--;
            if(stairs == 0){
                jump++;
                stairs = ladder - level;
            }
        }
        System.out.println(jump);
        pp.close();
    }
}
```
## 6. Kandane's Algorithm (Dynamic Programming)
### To find max subcontiguous array i.e max sum of subarray which is contiguous
```java
import java.util.*;
class Solution {
    public static void main(String[] args){
        Scanner pp = new Scanner(System.in);
        int n=pp.nextInt();
        int[] nums = new int[n];
        for(int i = 0; i<n; i++){
            nums[i]=pp.nextInt();
        } 
        int[] max_ar = new int[n];
        max_ar[0]= nums[0];
        for (int i = 1; i < n; i++) 
        {
            max_ar[i] = Math.max(nums[i], nums[i]+max_ar[i-1]);  
    }
        int max=max_ar[0];
        for(int i=1;i<n;i++){
            if(max_ar[i]>max){
                max = max_ar[i];
            }
        }
        System.out.print(max);
        pp.close();
    }
}
```