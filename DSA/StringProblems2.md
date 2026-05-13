import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     String name = "amanaplanacanalpanama";
      char[] arr = name.toCharArray();
      char target = 'a';
      int count = 0;
      
      for(int i = 0;i < arr.length;i++){
        if(arr[i] == target){
          count++;
        }
      }
    
    
      System.out.println("Frequency of " +  target +  " is " + count);
    
    }
}
---------------------------------------------------------------------------
import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     String name = "amanaplanacanalpanama";
      char[] arr = name.toCharArray();
      StringBuilder nodupli = new StringBuilder();
  
      
      for(int i = 0;i < arr.length;i++){
       if (nodupli.indexOf(String.valueOf(arr[i])) == -1) {
                nodupli.append(arr[i]);
            }
      }
      
      System.out.println(nodupli);
    
    }
}
