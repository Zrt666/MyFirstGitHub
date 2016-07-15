<h1>整理几个简单的排序</h1>
<li/>快速排序<br/>

import java.util.Calendar;

//import java.util.*;

public class QuickSort {<br/>

	final int ArraryLen=10;<br/>
	public static void main(String[] args){<br/>
		Quick qs=new Quick();
		int len=100000;
		int a[]=new int[len];
		for(int i=0;i<len;i++){
			int t=(int)(Math.random()*10000);
			a[i]=t;
			
		}
		Calendar cal=Calendar.getInstance();
		System.out.println(cal.getTime());
		qs.quick(a, 0, a.length-1);
		cal=Calendar.getInstance();
		System.out.println(cal.getTime());
			
	}

}

//分割函数
class Division{

	int division(int a[],int left,int right){
		int base=a[left];
		while(left<right){
			while(left<right&&a[right]>base)
				--right;
			a[left]=a[right];
			while(left<right&&a[left]<base)
				++left;
			a[right]=a[left];
		}
		a[left]=base;
		return left;
	}
}

//快速排序
class Quick{

	public void quick(int a[],int left,int right){
		int i,j;
		Division dev=new Division();
		if(left<right){
			i=dev.division(a, left, right);
			quick(a,left,i-1);
			quick(a,i+1,right);
		}
	}
}

<li/>归并排序<br/>
//归并排序nlogn<br/>
class Sort1{

	void Merge(int A[],int p,int q,int r){
		int n1=q-p+1;
		int n2=r-q;
		int L[]=new int[n1+1];
		int R[]=new int[n2+1];
		for(int i=0;i<n1;i++)
			L[i]=A[p+i];
		for(int j=0;j<n2;j++)
			R[j]=A[q+j+1];
		L[n1]=(int)Double.POSITIVE_INFINITY;
		R[n2]=(int)Double.POSITIVE_INFINITY;
		int i=0;
		int j=0;
		for(int k=p;k<=r;k++){
			if(L[i]<=R[j]){
				A[k]=L[i];
				i++;
			}
			else{
				A[k]=R[j];
				j++;
			}
		}
	}
	
	void Merge_sort(int A[],int p,int r){
		if(p<r){
			int q=(p+r)/2;
			Merge_sort(A,p,q);
			Merge_sort(A,q+1,r);
			Merge(A,p,q,r);
		}
	}
}

<li/>计数排序<br/>

public class CountingSort {

	public static void main(String []args){
		int a[]={2,5,3,0,2,3,0,3};
		int b[]=new int[a.length];
		CSort cs=new CSort();
		System.out.print("输出原数组：");
		for(int i=0;i<a.length;i++)
			System.out.print(a[i]+" ");
		cs.sort(a, b, 6);
		System.out.print("\n排序后的数组：");
		for(int i=0;i<a.length;i++)
			System.out.print(b[i]+" ");
	}

}

class CSort{

	void sort(int A[],int B[],int k){
		int C[]=new int[k+1];
		for(int i=0;i<=k;i++)
			C[i]=0;
		for(int j=0;j<A.length;j++)
			C[A[j]]=C[A[j]]+1;
		for(int i=1;i<=k;i++)
			C[i]=C[i]+C[i-1];
		for(int j=A.length-1;j>=0;j--){
			
			B[C[A[j]]-1]=A[j];
			C[A[j]]=C[A[j]]-1;
		}
	}
}

<li/>堆排序<br/>

class Heap1{

	int parent(int i){
		return i/2;
	}
	int Left(int i){
		return 2*i;
	}
	int Right(int i){
		return (2*i+1);
	}
	void Max_Heap(int A[],int i){
		int l=Left(i);
		int r=Right(i);
		int largest=0;
		int base;
		if(l<=A.length&&A[l-1]>A[i-1])
			largest=l;
		else largest=i;
		if(r<=A.length&&A[r-1]>A[largest-1])
			largest=r;
		if(largest!=i){
			base=A[i-1];
			A[i-1]=A[largest-1];
			A[largest-1]=base;dui
			Max_Heap(A,largest);
		}
	}
	
	//建堆
	void Build_Max_Heap(int A[]){
		int heapsize=A.length;
		for(int i=heapsize/2;i>0;--i)
			Max_Heap(A,i);
	}
	
	//堆排序
	void Heap_Sort(int A[]){
		Build_Max_Heap(A);
		int base;
		int heapsize=A.length;
		for(int i=A.length;i>1;--i){
			base=A[0];
			A[0]=A[i-1];
			A[i-1]=base;
			heapsize--;
			Max_Heap(A, 1);
		}
	}
}