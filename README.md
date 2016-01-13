import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Given a list of N coins, their values (V1, V2, … , VN), and the total sum S.
 *  Find the minimum number of coins the sum of which is S (we can use as many coins of one type as we want), 
 * or report that it’s not possible to select coins in such a way that they sum up to S.
 * @author kayethi 
 * 
 * set min[i] = infinity for all i
 * min[0]=0;
 * for i = 1 to S
 * for j = 0  to n-1
 * 	if(vj <=i && min[i-vj]+1 < min[i])
 * 		then min[i] = min[i-vj] +1
 * output min[s]
 *
 */
public class sumCoin {
	public int sumCoinsDP(int[] values, int sum){
		int N= values.length;
		int[] min = new int[sum+1]; // minimum value of coins to i
		Arrays.fill(min, Integer.MAX_VALUE-1);
		min[0]=0;
		for (int i = 1; i <= sum; i++) {
			//System.out.println(i +" : "+min[i]);
			for (int k = 0;k<N; k++) {
				//System.out.print("i : "+i+" k : "+k+" Minvalue : "+ min[i]+ " | ");
				if(values[k] <=i &&min[i-values[k]]+1 < min[i] /*&& min[i-values[k]]>=0*/ ){
					//System.out.println();
					min[i] = min[i-values[k]]+1; 
					//System.out.println(" Minvalue : "+ min[i] + " values[k] : "+values[k]);
				}
			}
			System.out.println(i +" : "+min[i]);
		}
		if(min[sum] == Integer.MAX_VALUE-1 ){
			return 0;
		}
		return min[sum];
		
		
	}
	public static void main(String[] args){
		sumCoin s = new sumCoin();
		int[] values = {3,5};
		System.out.println(s.sumCoinsDP(values, 10));
	}
}
