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
        d = d%n;

        int[] nums = new int[n];
        for(int i = 0; i<n ; i++){
            nums[i] = pp.nextInt();
        }

        reverse(nums , 0 , n-1);
        reverse(nums, 0, d-1); //line 14
        reverse(nums, d, n-1); //line 15

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
### To find a pattern within a string
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

## 7. Manacher's Algorithm
### To find longest palindrome substring

```java 
import java.util.*; 

class GFG 
{ 
	static void findLongestPalindromicString(String text) 
	{ 
		int N = text.length(); 
		if (N == 0) 
			return; 
		N = 2 * N + 1;  
		int[] L = new int[N + 1];  
		L[0] = 0; 
		L[1] = 1; 
		int C = 1; // centerPosition 
		int R = 2; // centerRightPosition 
		int i = 0; // currentRightPosition 
		int iMirror; // currentLeftPosition 
		int maxLPSLength = 0; 
		int maxLPSCenterPosition = 0; 
		int start = -1; 
		int end = -1; 
		int diff = -1; 

		for (i = 2; i < N; i++) 
		{ 		
			iMirror = 2 * C - i; 
			L[i] = 0; 
			diff = R - i; 
			
			if (diff > 0) 
				L[i] = Math.min(L[iMirror], diff); 
			
			while (((i + L[i]) + 1 < N && (i - L[i]) > 0) && 
							(((i + L[i] + 1) % 2 == 0) || 
						(text.charAt((i + L[i] + 1) / 2) == 
						text.charAt((i - L[i] - 1) / 2)))) 
			{ 
				L[i]++; 
			} 

			if (L[i] > maxLPSLength) // Track maxLPSLength 
			{ 
				maxLPSLength = L[i]; 
				maxLPSCenterPosition = i; 
			} 
			
			if (i + L[i] > R) 
			{ 
				C = i; 
				R = i + L[i]; 
			} 
			
		} 

		start = (maxLPSCenterPosition - maxLPSLength) / 2; 
		end = start + maxLPSLength - 1; 
		System.out.printf("LPS of string is %s : ", text); 
		for (i = start; i <= end; i++) 
			System.out.print(text.charAt(i)); 
		// System.out.println(); 
	} 

	public static void main(String[] args) 
	{ 
        Scanner pp = new Scanner(System.in);
		String text =pp.next() ; 
		findLongestPalindromicString(text);
        pp.close(); 

} 
```
## 8. QuickSort Algorithm

```java
import java.util.Scanner;
class QuickSort 
{ 
	int partition(int arr[], int low, int high) 
	{ 
		int pivot = arr[high]; 
		int i = (low-1); // index of smaller element 
		for (int j=low; j<high; j++) 
		{ 
			// If current element is smaller than or equal to pivot 
			if (arr[j] <= pivot) 
			{ 
				i++; 
				// swap arr[i] and arr[j] 
				int temp = arr[i]; 
				arr[i] = arr[j]; 
				arr[j] = temp; 
			} 
		} 

		// swap arr[i+1] and arr[high] (or pivot) 
		int temp = arr[i+1]; 
		arr[i+1] = arr[high]; 
		arr[high] = temp; 

		return i+1; 
	} 

	/* arr[] --> Array to be sorted, 
	low --> Starting index, 
	high --> Ending index */
	void sort(int arr[], int low, int high) 
	{ 
		if (low < high) 
		{ 
			/* pi is partitioning index, arr[pi] is 
			now at right place */
			int pi = partition(arr, low, high); 

			sort(arr, low, pi-1); 
			sort(arr, pi+1, high); 
		} 
	} 
	public static void main(String args[]) 
	{ 
        Scanner pp = new Scanner(System.in);
        int n = pp.nextInt();
        int[] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = pp.nextInt();
        }
        
		QuickSort qs = new QuickSort(); 
		qs.sort(arr, 0, n-1); 

		for(int i=0; i<n; ++i) {
            System.out.print(arr[i]+" "); 
        }
        pp.close();
	} 
} 
```
## 9. BubbleSort Algorithm

```java
import java.util.Scanner;

class Solution {
    public static void main(String args[]){
        Scanner pp = new Scanner(System.in);
        int n = pp.nextInt();
        int[] arr = new int[n];
        // take array input
        for(int i = 0;i<n;i++){
            arr[i] = pp.nextInt();
        }
        bubblesort(arr,n);
        // print sorted array
        for(int i = 0;i<n;i++){
            System.out.print(arr[i] + " ");
        }
        pp.close();
    }

    static void bubblesort(int[] arr, int n){
        for(int k =0 ;k<n-1;k++){
            int flag = 0;
            for(int i=0;i<n-k-1;i++){
                if(arr[i]>arr[i+1]){
                    arr[i] ^= arr[i+1];
                    arr[i+1] ^= arr[i];
                    arr[i] ^= arr[i+1];
                    flag = 1;
                }
            }
            if(flag==0){
                break;
            }
        }
    }
}
```
## 10. Binary Search 

```java
import java.util.Scanner;
import java.util.Arrays;

class Solution {
    public static void main(String args[]){
        Scanner pp = new Scanner(System.in);
        int n = pp.nextInt();
        int[] arr = new int[n];
        for(int i = 0;i<n;i++){
            arr[i] = pp.nextInt();
        }
        Arrays.sort(arr);
        int x = pp.nextInt();
        System.out.print(binarysearch(arr, n, x));
        pp.close();
    }

    static int binarysearch(int[] arr, int n, int x){
        int start = 0;
        int end = n-1;
        while (start<=end){
            int mid = (start+end)/2;
            if(arr[mid]==x){
                return mid;
            }
            else if(arr[mid]>x){
                end = mid-1;
            }
            else {
                start = mid +1;
            }
        }
        return -1;
    }
}
```
