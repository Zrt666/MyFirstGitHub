<h2>公共最长字符串算法</h2>

/*
 * 功能：公共最长字符串
 * 作者：张瑞涛 学号：13130110056
 */

public class LCString {

    public static void main(String[] args) {
    	String s1="xzyzzyx";
    	String s2="zxyyzxz";
    	String s3="ALLAAQANKESSSESFISRLLAIVAD";
    	String s4="KLQKKLAETEKRCTLLAAQANKENSNESFISRLLAIVAG";
        if(s1.length()>=s2.length()){
        	//获取长度较短的字符串并调用获取字符串长度函数
            System.out.println(MaxSubString(s2,s1));
        }
        else{
            System.out.println(MaxSubString(s1,s2));
        }
        if(s3.length()>=s4.length()){
        	//获取长度较短的字符串并调用获取字符串长度函数
            System.out.println(MaxSubString(s3,s4));
        }
        else{
            System.out.println(MaxSubString(s3,s4));
        }
    }

    private static String MaxSubString(String shortstr, String longstr) {
        String temp = new String("");
        for(int i = 0;i<shortstr.length();i++){
        	//先从短字符串的长度开始，逐步递减长度，直到出现符合的字符串
        	for(int j = 0,k = shortstr.length()-i;k<=shortstr.length();j++,k++){
                temp = shortstr.substring(j, k);
                if(longstr.contains(temp)){
                	// 当且仅当此字符串包含指定的 char值序列时，返回 true。
                	return temp;
                }
            }
        }
        return null;
    }

}