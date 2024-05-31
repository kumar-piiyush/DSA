Question : https://www.geeksforgeeks.org/problems/array-subset-of-another-array2317/1?page=1&category=Binary%20Search&sortBy=difficulty

Answer :

//{ Driver Code Starts
//Initial Template for Java

//Initial Template for Java

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {
	public static void main(String[] args) throws IOException
	{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine().trim());
        while(t-->0)
        {
            StringTokenizer stt = new StringTokenizer(br.readLine());
            
            long n = Long.parseLong(stt.nextToken());
            long m = Long.parseLong(stt.nextToken());
            long a1[] = new long[(int)(n)];
            long a2[] = new long[(int)(m)];
            
            
            String inputLine[] = br.readLine().trim().split(" ");
            for (int i = 0; i < n; i++) {
                a1[i] = Long.parseLong(inputLine[i]);
            }
            String inputLine1[] = br.readLine().trim().split(" ");
            for (int i = 0; i < m; i++) {
                a2[i] = Long.parseLong(inputLine1[i]);
            }
            
            
            Compute obj = new Compute();
            System.out.println(obj.isSubset( a1, a2, n, m));
            
        }
	}
}

// } Driver Code Ends


//User function Template for Java


class Compute {
    public boolean presentIna1(long a1[], long target){
        
        //here my aim is to search the given elemet
        //basic approch is linear search algorithm
        
        for (int i = 0; i<a1.length; i++){
            if (a1[i]==target) return true;
        }
        return false;
    }
    public String isSubset( long a1[], long a2[], long n, long m) {
        
        //have to check whether a2 is a subset of a1 or not
        
        //approch
        //I am planning to get each element of a2 and search it in a1;
        //if any of the element which is present in a2 but not in a1 , return false;
        //as it can not be subset in that case
        //esle return true
        
        String ans = "Yes";
        
        for (int i = 0; i<m; i++){
            if(presentIna1(a1, a2[i]) == false) {
                ans="No";
                break;
            }
            else if(presentIna1(a1, a2[i]) == true) {
                ans="Yes";
                continue;
            }
        }
        
        
        return ans;
        
    }
    
//edge cases
    
    
//     51 /209
// For Input: 
// 8 4
// 1 2 3 4 5 6 7 8
// 1 2 3 1
// Your Code's output is: 
// Yes
// It's Correct output is: 
// No
// Output Difference
// YesNo


// approch to handle this edge case
// Approach 1 - Frequency count (Maps)
// count the occurrences of each element in both arrays. Use maps to store the frequencies of elements in a1 then 
// For each element in a2, check if it appears at least as many times in a1 as it does in a2. If any element in a2 does not meet this criterion, return "No".

//Approach 2 - Two Pointer (Sort and then compare) - better
// one is sort both of the arrays and then do two pointer approach 
// Two-Pointer Technique: Use two pointers, one for each array (a1 and a2). Initialize both pointers at the start of their respective arrays.
// Traverse the Arrays:
// If the element pointed to by the pointer in a1 matches the element pointed to by the pointer in a2, move both pointers forward.
// If the element in a1 is less than the element in a2, move the pointer in a1 forward.
// If the element in a1 is greater than the element in a2, it means the current element in a2 cannot be found in a1, so you should return "No".
// Completion Check: If you reach the end of a2 while following the above steps, it means all elements of a2 were found in a1 in the correct order, so return "Yes". If not, return "No".
// This approach ensures that you efficiently check for the subset condition by leveraging the sorted order of the arrays, with a time complexity of O(n + m).


public String isSubset(long a1[], long a2[], long n, long m) {
    int i = 0, j = 0;

    // Traverse both arrays using two pointers
    while (i < n && j < m) {
        if (a1[i] == a2[j]) {
            i++;
            j++;
        } else if (a1[i] < a2[j]) {
            i++;
        } else {
            return "No";
        }
    }

    // Check if all elements of a2 were found in a1
    if (j == m) {
        return "Yes";
    } else {
        return "No";
    }
}


Now I moved to understand two pointer approach - https://www.youtube.com/watch?v=9kdHxplyl5I&list=PLgUwDviBIf0q7vrFA_HEWcqRqMpCXzYAL
}
