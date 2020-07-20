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

