import java.util.*;

public class Main {
    public static void main(String[] args) {
      
     HashMap<Character,Integer> map = new HashMap();
     map.put('a',1);
     map.put('b',2);
     map.put('c',3);
     
      
     System.out.println(map.get('a'));
     System.out.println(map.containsKey('a'));
      
    }
}

-----------------------------------------------------------------------------
import java.util.*;

public class Main {
    public static void main(String[] args) {
    String name = "the quick brown fox jumps over the lazy dog";
    char[] charArray = name.toCharArray(); 
    HashMap<Character,Integer> map = new HashMap<>();
    for(int i = 0;i < charArray.length;i++){
      if(map.containsKey(charArray[i])){
        int oldCount = map.get(charArray[i]);
         map.put(charArray[i], oldCount + 1);
      }else if(charArray[i] != ' '){
        map.put(charArray[i],1);
      }
    }
     System.out.println(map);
    }
}
-----------------------------------------------------------------------------------

import java.util.*;

public class Main {
    public static void main(String[] args) {
    String name = "programming";
    char[] charArray = name.toCharArray(); 
    
    HashMap<Character,Integer> map = new HashMap<>();
    
    for(int i = 0;i < charArray.length;i++){
      
      if(map.containsKey(charArray[i])){
        int oldCount = map.get(charArray[i]);
         map.put(charArray[i], oldCount + 1);
      }else if(charArray[i] != ' '){
        map.put(charArray[i],1);
      }
    }
    
    for(int i = 0; i < charArray.length;i++){
      if(map.get(charArray[i]) == 1){
        System.out.println(charArray[i]);
        break;
      }
    }
    
    -----------------------------------------------------------------------------------------
    import java.util.*;

public class Main {
    public static void main(String[] args) {
        
        String word1 = "aab";
        String word2 = "aba";
        
        
        char[] charArray1 = word1.toCharArray();
        char[] charArray2 = word2.toCharArray();
        
        
        if(charArray1.length != charArray2.length){
          System.out.println("Incorrect length");
        }
        
        
        HashMap<Character,Integer> map = new HashMap<>();
        
        for(int i = 0;i < charArray1.length;i++){
          
          if(map.containsKey(charArray1[i])){
            
            int count = map.get(charArray1[i]);
            map.put(charArray1[i],count + 1);
            
          }else{
             map.put(charArray1[i],1);
          }
        }
        
        boolean isAnagram = true;
 
        
        for(int i = 0;i < charArray2.length;i++){
          
          if(map.containsKey(charArray2[i])){
            map.put(charArray2[i],0);
          }
          
          if(map.get(charArray2[i]) != 0){
            isAnagram = false;
            break;
          }
        }
        
 
 
 
      System.out.println(isAnagram);
 
    }
}
    
    
     System.out.println(map);
    }
}
