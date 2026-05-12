import java.util.*;

public class Main {
    public static void main(String[] args) {
    
      int[] arr = {10,98,12,54,10,34,121,100,90,10};
      int[] arrforZero = {0,98,12,0,10,0,121,100,90,10};
      int high = 0;
      int secondHigh = 0;
      List<Integer> reverse = new ArrayList<>();
      int count10 = 0;
      List<Integer> moveZeros = new ArrayList<>();
   
   
      for(int i = 0; i < arr.length;i++){
        if(arr[i] > high){
          
          secondHigh = high;
          high = arr[i];
         
        } else if (arr[i] > secondHigh && arr[i] < high) {
           secondHigh = arr[i];
        }
      }
      
      
      for(int i = arr.length - 1;i >= 0;i-- ){
        reverse.add(arr[i]);
      }
      
      for(int i = 0; i < arr.length;i++){
        if(arr[i] == 10){
          count10++;
        }
      }
      
      int countZeros = 0;
      
      for(int i = 0; i < arrforZero.length;i++){
        
        if(arrforZero[i] == 0){
          countZeros++;
          continue;
        }
        
        moveZeros.add(arrforZero[i]);
      }
      
      for(int i = 0; i < countZeros;i++){
        moveZeros.add(0);
      }
      
      
      System.out.println("highest : " + high);
      System.out.println("Second highest : " + secondHigh);
      System.out.println("reversed : " + reverse);
      System.out.println("Total count of int 10 : " + count10);
      System.out.println("moved 0's to right : " + moveZeros + " zeros : " + countZeros);
    
    }
}




//this contains the solution for largest,second largest,reverse,frequency and move zeros for basic array.
