import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     String name = "Sahli";
     char[] arr = name.toCharArray();
      
     int left = 0;
     int right = name.length() - 1;
     
     
     
     
      while(left < right){
        char temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
      }
     
    
    System.out.println(new String(arr));
    
    
    }
}
-----------------------------------------------------------
import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     String name = "JOJO";
     char[] arr = name.toCharArray();
      
     int left = 0;
     int right = name.length() - 1;
     
     boolean isPalindrome = true;
     
     
     
      while(left < right){
       if(arr[left] != arr[right]){
         isPalindrome = false;
         break;
       }else{
         left++;
         right--;
       }
       
       
      }
     
    
    System.out.println(isPalindrome);
    
    
    }
}
---------------------------------------------------------------------

import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     String name = "amanaplanacanalpanama";
     char[] arr = name.toCharArray();
      
     int countVowels = 0;
     
     for(int i = 0;i < arr.length-1;i++){
       if(arr[i] == 'a' || arr[i] == 'e'||arr[i] == 'i'||arr[i] == 'o'||arr[i] == 'u'){
         countVowels++;
       }
     }
     
     
    
    System.out.println(countVowels);
    
    
    }
}
