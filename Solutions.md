# 1. [2 Sum](https://leetcode.com/problems/two-sum/)
1. Initial brute force solution, O(n^2):
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for (int i = 0; i < nums.length; i++){
            for (int j = i+1; j<nums.length; j++){
                if (nums[i]+nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                }
            }
        }
    return result;
    }
}
```
2. Optimizing with hashmap O(n):
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++){
            int ans = target - nums[i]; 
            if(map.containsKey(ans)) { 
                return new int[]{map.get(ans), i};   
            }
            else {
                map.put(nums[i], i); //populate hashmap
            }
        }
        return null;
    }
}

//Instantiate hashmap
//Fix point in the array for first number, i
//Search hashmap to see if it contains a value that is 'target - nums[i]'
//Return pair of values
//Map<K,V>
```

# 2. [2 Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
1. Hashmap solution, O(n):
```
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] res = new int[2];
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < numbers.length; i++){
            int val = numbers[i];
            if (map.containsKey(val)) {
                return new int[]{map.get(val) + 1, i + 1};
            }
            else {
                map.put(target - val, i);
            }
        }
        return null;
    }
}

//Create res arr
//Create hashmap to hold arr key + val for one pass
//Pass through array, populate hashmap
//You can get away with this algo because the array is already sorted
```

# 3. [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
1. Brute force, O(n^2), exceeds time limit:
```
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++){
                if (nums[i] == nums[j]){
                    return true;
                }
            }
        }
        return false;
    }
}
```

2. HashSet solution, O(n):
```
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++){
            if (set.contains(nums[i])){
                return true;
            }
            else{
                set.add(nums[i]);
            }
        }
        return false;
    }
}
```

# 4. [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
1. Stack solution O(n):
```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<Character>();
        for (char c : s.toCharArray()){
            if (c == '(') st.push(')');
            else if(c == '[') st.push (']');
            else if(c == '{') st.push ('}');
            else if (st.isEmpty() || st.pop() != c) 
                return false;
            }
        return st.isEmpty(); //returns boolean
        }
    }

//Create stack
//For each loop, s as charArray
//If charArray contains hit input, push corresponding parentheses to stack
//If stack is empty for char, return false.
//If stack pop doesn't return current char c, return false
//return st.isEmpty() should return true for valid strings
//Only checks for beginning parentheses so the "pop" takes place on the closing parentheses
```

# 5. [Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/)
1. O(n) loop solution:
```
class Solution {
    public int[] shuffle(int[] nums, int n) {
        int[] result = new int[2*n];
        
        int a = 0; //pointer at beginning, start of x
        int b = n; //pointer at n, start of y
        
        for (int i = 0; i < (n*2); i++){
            if (i%2 == 0){ //i is even
                result[i] = nums[a];
                a++;
            }
            else{ //i is odd
                result[i] = nums[b];
                b++;
            }
        }
        return result;
    }
}
```

# 6. [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
1. O(n) loop solution:
```
class Solution {
    public int maxSubArray(int[] nums) {
        int max = Integer.MIN_VALUE; //need a way to store the max, start with constant
        int res = 0;
        for (int i = 0; i < nums.length; i++){
            res += nums[i];
            if (res > max){
             max = res;
            }
            if (res < 0){
                res = 0;
            }
        }
        return max;
    }
}
```

# 7. [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
1. O(m+n) time, O(1) space: 
```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int tail1 = m-1, tail2 = n-1, sumTail = (m+n)-1; //recall nums1.len = m + n
        while (tail2 >= 0){ //while iterating through second array
            if (tail1 >= 0 && nums1[tail1] > nums2[tail2]){ //if nums1[m] bigger than nums2[n]
                nums1[sumTail--] = nums1[tail1--]; //then put nums1 tail in sumTail (m+n len)
            }
            else { //if nums1[m] smaller than nums2[n] || if ==, sumtail loc becomes tail2 val
                nums1[sumTail--] = nums2[tail2--]; //put nums2 tail in sumTail pointer location
            }
        }
    }
}
```

# 8. [Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)
1. Sorted solution, O(n)
```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        int p1 = 0;
        int p2 = 0;
        Arrays.sort(nums1); Arrays.sort(nums2);
        
        while(true){
            if (p1 >= nums1.length || p2 >= nums2.length){
                break;
            }
            else if (nums1[p1] == nums2[p2]){
                list.add(nums1[p1]);
                p1++;
                p2++;
            }
            else if (nums1[p1] > nums2[p2]){
                p2++;
            }
            else if (nums1[p1] < nums2[p2]){
                p1++;
            }
        }
        
        int[] res = new int[list.size()];
        
        for (int i = 0; i < res.length; i++){
            res[i] = list.get(i);
        }
        
        return res;
    }
}

//Pretty much copied verbatim from top solution, struggled a bit with the logic behind pointers
//Do understand the logic for this solution though, sorting enables intuitive use of pointers
```

2. Flawed logic, passes problem test case but fails submission. Similar solution would be O(n^2) anyway.
```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        
        if (nums1.length <= 0 || nums2.length <= 0){
            return null; //edge case
        }
        
        for (int i = 0; i < nums1.length; i++){
            for (int j = 0; j < nums2.length; j++){
                if (nums1[i] == nums2[j]){
                    list.add(nums1[i]);
                    i++;
                }
            }
        }
        
        int[] res = new int[list.size()];
        for (int i = 0; i < res.length; i++){
            res[i] = list.get(i);
        }
        
        return res;
    }
}

//Passes test case but fails submission
//Logic fails on criteria "must appear as many times as it shows in both arrays"
//Submitting to repo because this experience suggests that it will be useful to remember that sorting before scanning is a viable option
//Especially when it helps in understanding/utilizing pointer logic for more space efficient solution, rather than nested loop
```

# 9. [Best Time To Buy And Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
1. Original code, exceeds time limit.
```
class Solution {
    public int maxProfit(int[] prices) {
        int max = 0; 
        int min = prices[0]; //placeholder
        
        for (int i = 0; i < prices.length; i++){
            if (prices[i] < min){
                min = prices[i];
            }
            if (max < prices[i]){
                max = prices[i];
            }
        }
        
        int i = 0; int maxIndex = 0; int minIndex = 0;
        while (i < prices.length){ //find index
            if(prices[i] == max) {
                maxIndex = i;
            }
            else if (prices[i] == min){
                minIndex = i;
            }
        }
        
        if (minIndex < maxIndex){ 
            return max - min;
        }
        
        return 0;
    }
}
```

2. Solution from Discussion
```
class Solution {
    public int maxProfit(int[] prices) {
        int res = 0;
        
        if (prices.length == 0){
            return res; //edge case
        }
        
        int buy = prices[0]; //set placeholder to iterate through arr
        
        for (int i = 1; i < prices.length; i++){
            if(prices[i] > buy){
                if (res < (prices[i] - buy)){ //ensure max profit
                    res = prices[i] - buy; //res is new max profit
                }
            }
            else{ //prices[i] < buy
                    buy = prices[i];
                }
        }
        
        return res;
    }
}
```

3. Revised Original Solution
```
class Solution {
    public int maxProfit(int[] prices) {
        int sell = 0; 
        int buy = prices[0]; //placeholders
        
        if (prices.length == 0) {
            return 0; //edge case
        }
        
        for (int i = 1; i < prices.length; i++){
            if (prices[i] > buy){
                if (sell < (prices[i]-buy)){
                    sell = prices[i] - buy; //find max profit logic
                }
            }
            else{ //if prices[i] < buy
                buy = prices[i]; //move up buy index to highest val
            }
            
        }
        
        return sell;
    }
}

//Refined original code using the solution from discussion
//Am pleased that I got the required indices correct; middle logic from original solution is a mess though
//Need more work on logic mid-iteration & syntax for deriving desired values
```

# 10. [Binary Search](https://leetcode.com/problems/binary-search/)
1. O(log n)
```
class Solution {
    public int search(int[] nums, int target) {
        int l = 0; 
        int r = nums.length - 1;
        
        while (l <= r){
            int mid = (l+r)/2; //inside loop to continuously re-define
            if (nums[mid] == target){
                return mid;
            }
            if (nums[mid] > target){ //target is in left sub-array
                r = mid - 1;
            }
            else{ //target is in right sub-array
                l = mid + 1;
            }
        }
        
        return -1;
    }
}
```

# 11. [First Bad Version](https://leetcode.com/problems/first-bad-version/)
1. O(log n)
```
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int l = 1;
	    int r = n;

	    while (l < r) {
    		int mid = l + (r - l) / 2;

	    	if (isBadVersion(mid)) {
		    	r = mid;
		    } else {
		    	l = mid + 1;
		    }

	    }

	    return l;

    }
}
```