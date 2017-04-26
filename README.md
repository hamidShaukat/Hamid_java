
package com.test.app;
import java.util.ArrayList;
import java.util.List;

public class BerlinClockTest {
 
     public static void main(String str[]){
       String strr[]=changeToBerlinClock("18:01:01");
       
       for(String str1:strr){
        System.out.println(str1);
       }
     }
 
 
    public static String[] changeToBerlinClock(String time) {
     // int[] parts = Stream.of(time.split(":")).mapToInt(Integer::parseInt).toArray();
    	List<Integer> list=new ArrayList<Integer>();
    	for(String strTime:time.split(":")){
    		list.add(Integer.parseInt(strTime));
    	}
        return new String[] {
                findSeconds(list.get(2)),
                findTopHours(list.get(0)),
                findBottomHours(list.get(0)),
                findTopMinutes(list.get(1)),
                getBottomMinutes(list.get(1))
        };
    }
 
    protected  static String findSeconds(int number) {
        if (number % 2 == 0) return "Y";
        else return "O";
    }
 
    protected static String findTopHours(int number) {
        return fetchOnOff(4, fetchTopNumberOfOnSigns(number));
    }
 
    protected static String findBottomHours(int number) {
        return fetchOnOff(4, number % 5);
    }
 
    protected static String findTopMinutes(int number) {
        return fetchOnOff(11, fetchTopNumberOfOnSigns(number), "Y").replaceAll("YYY", "YYR");
    }
 
    protected static  String getBottomMinutes(int number) {
        return fetchOnOff(4, number % 5, "Y");
    }
 
    private static String fetchOnOff(int lamps, int onSigns) {
        return fetchOnOff(lamps, onSigns, "R");
    }
    private static String fetchOnOff(int lamps, int onSigns, String onSign) {
        String out = "";
        for (int i = 0; i < onSigns; i++) {
            out += onSign;
        }
        for (int i = 0; i < (lamps - onSigns); i++) {
            out += "O";
        }
        return out;
    }
 
    private static int fetchTopNumberOfOnSigns(int number) {
        return (number - (number % 5)) / 5;
    }
 
}
