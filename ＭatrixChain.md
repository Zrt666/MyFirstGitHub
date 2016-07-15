<h2>矩阵链乘法算法</h2>
/*
 * 功能：矩阵链乘法问题
 * 作者：张瑞涛 学号：13130110056
 */
import java.util.*;

public class Matrix_chain {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		MatChain mc=new MatChain();
		int p1[]={3,5,2,1,10};
		int p2[]={2,7,3,6,10};
		int p3[]={10,3,15,12,7,2};
		int p4[]={7,2,4,15,20,5};
		for(int i=0;i<p1.length;i++)
			System.out.print(p1[i]+" ");
		System.out.print("\na:");
		mc.PrintOptimalParens(mc.MatrixChainOrder(p1), 1, p1.length-1);
		System.out.println();
		for(int i=0;i<p2.length;i++)
			System.out.print(p2[i]+" ");
		System.out.print("\nb:");
		mc.PrintOptimalParens(mc.MatrixChainOrder(p2), 1, p2.length-1);
		System.out.println();
		for(int i=0;i<p3.length;i++)
			System.out.print(p3[i]+" ");
		System.out.print("\nc:");
		mc.PrintOptimalParens(mc.MatrixChainOrder(p3), 1, p3.length-1);
		System.out.println();
		for(int i=0;i<p4.length;i++)
			System.out.print(p4[i]+" ");
		System.out.print("\nd:");
		mc.PrintOptimalParens(mc.MatrixChainOrder(p4), 1, p4.length-1);

	}

}

class MatChain{

	//计算最优代价
	public int[][] MatrixChainOrder(int p[]){
		int n=p.length;
		int j=0,q=0;
		//表示计算矩阵Aij所需要的标量乘法次数的最小次数
		int m[][]=new int[n][n];
		//记录分割点k
		int s[][]=new int[n][n];
		
		for(int i=0;i<n;i++){
			m[i][i]=0;
		}
		for(int l=2;l<n;l++){
			for(int i=1;i<n-l+1;i++){//注意
				j=i+l-1;
				m[i][j]=(int)Double.POSITIVE_INFINITY;
				for(int k=i;k<j;k++){
					q=m[i][k]+m[k+1][j]+p[i-1]*p[k]*p[j];
					if(q<m[i][j]){
						m[i][j]=q;
						s[i][j]=k;
						//System.out.println(i+" "+j+" "+k+" ");
					}
				}
			}
		}
		return s;
	}
	
	//构造最优解
	public void PrintOptimalParens(int s[][],int i,int j){
		if(i==j){
			System.out.print("A"+i);
		}
				
		else{
			System.out.print("(");
			PrintOptimalParens(s,i,s[i][j]);
			PrintOptimalParens(s,s[i][j]+1,j);
			System.out.print(")");
		}
	}
	
}