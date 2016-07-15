<h2>公共最长子序列算法</h2>
/*
 * 功能：公共最长子序列
 * 作者：张瑞涛 学号：13130110056
 */

public class LCS {

	public static void main(String[] args) {

		LongestComSubQuence lcs=new LongestComSubQuence();
		String x="xzyzzyx";
		String y="zxyyzxz";
		lcs.PrintLCS(lcs.LCSLength(x, y), x, x.length(), y.length());
		System.out.println();
		String a="ALLAAQANKESSSESFISRLLAIVAD";
		String b="KLQKKLAETEKRCTLLAAQANKENSNESFISRLLAIVAG";
		lcs.PrintLCS(lcs.LCSLength(a, b), a, a.length(), b.length());

	}

}

//计算LCS的长度

class LongestComSubQuence{

	public int[][] LCSLength(String x,String y){
		int m=x.length();
		int n=y.length();
		int b[][]=new int[m][n];
		int c[][]=new int[m+1][n+1];
		for(int i=0;i<=m;i++)
			c[i][0]=0;
		for(int j=0;j<=n;j++)
			c[0][j]=0;
		for(int i=1;i<=m;i++){
			for(int j=1;j<=n;j++){
				if(x.charAt(i-1)==y.charAt(j-1)){//如果两个字母相等的情况
					c[i][j]=c[i-1][j-1]+1;
					b[i-1][j-1]=1;
				}
				else if(c[i-1][j]>=c[i][j-1]){
					c[i][j]=c[i-1][j];
					b[i-1][j-1]=2;
				}
				else{
					c[i][j]=c[i][j-1];
					b[i-1][j-1]=3;
				}
			}
		}
		return b;
	}
	
	//构造LCS
	public void PrintLCS(int b[][],String x,int i,int j){
		if(i==0||j==0)
			return;
		if(b[i-1][j-1]==1){
			PrintLCS(b,x,i-1,j-1);
			System.out.print(x.charAt(i-1));
		}
		else if(b[i-1][j-1]==2){
			PrintLCS(b,x,i-1,j);
		}
		else{
			PrintLCS(b,x,i,j-1);
		}
	}
}
