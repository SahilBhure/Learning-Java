import java.util.*;

public class Main {
    public static void main(String[] args) {
      
      int[] arr = {1,2,3,4,5,6};
      int left = 0;
      int right = arr.length - 1;
      
      while(left < right){
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
      }
      
      System.out.println(Arrays.toString(arr));
    
    }
}

--------------------------------------------------------------------------

import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     int[] arr = {1,2,3,4,5,6,7,6,5,4,3,2,1};
     boolean isPalindrome = false;
     int left = 0;
     int right = arr.length - 1;
     
     while(left < right){
       if(arr[left] != arr[right]){
         isPalindrome = false;
         break;
       }else{
         isPalindrome = true;
         left++;
         right--;
       }
     }
     
     System.out.println(isPalindrome);
     
     
     
      
      //System.out.println(Arrays.toString(arr));
    
    }
}
----------------------------------------------------------------------------------

import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     int[] arr = {12,3,0,21,0,54,31,0};
      int left = 0;
      for(int right = 0; right < arr.length; right++){

      if(arr[right] != 0){

          int temp = arr[left];
          arr[left] = arr[right];
          arr[right] = temp;

          left++;
      }
     
      }
     
      
      System.out.println(Arrays.toString(arr));
    
    }
}

-------------------------------------------------------------------------------------


import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     int[] arr = {1,1,2,2,2,3,4,5,6,6};
     List<Integer> sortArr = new ArrayList<>();
     int left = 0;
     sortArr.add(arr[left]);
     
     for(int right = 1; right < arr.length;right++){
       if(arr[left] != arr[right]){
         sortArr.add(arr[right]);
         left = right;
       }
     }
     
      
      System.out.println(sortArr);
    
    }
}
-----------------------------------------------------------------------------------------

