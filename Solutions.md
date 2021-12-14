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

# 12. [Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/)
```
class Solution {
    public int[][] matrixReshape(int[][] mat, int r, int c) {
        int n = mat.length;
        int m = mat[0].length;
        if (r * c != n * m){
            return mat; //edge case
        }
        
        int[][] res = new int[r][c];
        for (int i = 0; i < r*c; i++){ //r*c is res.length for practical purposes
            res[i/c][i%c] = mat[i/m][i%m];
        }
        
        return res;
    }
}

//Revisit, found this hard, copied solution, do more problems with multi-dimensional arrays
```

# 13. [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)
```
class Solution {
    public List<List<Integer>> generate(int numRows) {
        
        List<List<Integer>> result = new ArrayList<>();
        
        for (int i = 0; i < numRows; i++){
            List<Integer> looplist = new ArrayList<>();
            
            for (int j = 0; j < i + 1; j++){
        
                if(j == 0 || j == i){ //add 1 to list when empty or when index match
                    looplist.add(1); //end up with [1,1] on second iteration; keeps 1 on outer
                }
                else{ //get indices and add
                    int a = result.get(i-1).get(j-1); //leftmost val, [r][c]
                    int b = result.get(i-1).get(j); //rightmost val
                    looplist.add(a+b); //progress triangle
                }
            
            }
            result.add(looplist); //populate result list
        }
        return result;
    }
}
```

# 14. [Search Insert Position](https://leetcode.com/problems/search-insert-position/)
```
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        
        while (left <= right){
            int mid = (left+right)/2;
            if (nums[mid] == target){
                return mid; //index
            }
            else if (nums[mid] > target){ //target is to the left of mid
                right = mid - 1;
            }
            else { //nums[mid] < target, target is to the right of mid
                left = mid + 1;
            }
        }
        return left;
    }   
}
```

# 15. [First Unique Character In A String](https://leetcode.com/problems/first-unique-character-in-a-string/)
1. O(n)
```
class Solution {
    public int firstUniqChar(String s) {
        int freq[] = new int[256];
        for (int i = 0; i < s.length(); i++){
            freq[s.charAt(i)]++;
        }
        for (int i = 0; i < s.length(); i++){
            if(freq[s.charAt(i)] == 1){
                return i; //return index
            }
        }
        return -1;
    }
}

//My original brute force solution was going to use two nested for loops
//With a placeholder var for the index of a character that didn't trigger the == in 2nd loop
//It would probably work but exceeds the time limit
//Found the above O(n) solution in discussions
/*
int res = 0;

for (int i = 0; i < s.length(); i++){
    for (int j = 0; j < s.length(); j++){
        while (s.charAt(i) !== s.charAt(j)){
            res = i;
        }
    }
    return res;
}
return -1;
*/
```

# 16. [Ransom Note](https://leetcode.com/problems/ransom-note/)
1. O(n+m) solution pulled from discussion
```
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int arr[] = new int[256];
        for (int i = 0; i < magazine.length(); i++){
            arr[magazine.charAt(i)]++;
        }
        for (int i = 0; i < ransomNote.length(); i++){
            if (--arr[ransomNote.charAt(i)] < 0){
                return false;
            }
        }
        
        return true;
    }
}
```

# 17. [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
1. O(n)
```
class Solution {
    public boolean isAnagram(String s, String t) {
        int res[] = new int[256];
        for (int i = 0; i < s.length(); i++){
            res[s.charAt(i)]++; //populate arr for each char in i
        }
        for (int i = 0; i < t.length(); i++){
            res[t.charAt(i)]--; //decrement arr for each char in t
            if (res[t.charAt(i)] < 0){
                return false;
            }
        }
        for (int i : res){
            if (i != 0){
                return false;
            }
        }
        
        return true;
    }
}

//Only one array on the stack at a time
//Extra conditional for exit, so don't need to use the third loop
//Third loop is only for cases where s length exceeds t
```

# 18. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
1. O(1) space, O(n) memory
```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) return false; //edge case
        ListNode once = head; //start at beginning
        ListNode twice = head;
        
        //while each pointer has a spot to go to
        while (twice.next != null && twice.next.next != null){ //one pointer
            once = once.next; //iterate once
            twice = twice.next.next; //iterate twice
             if (twice == once) {
                    return true; //they will meet in the list if there's a cycle
                }
        }
        
        return false; //no match
    }
    
//Note twice.next.next!null && twice.next != null returns a runtime error for single item lists
//Need to scan the single jump first
}
```

# 19. [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
1. Recursive O(n+m) solution
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        if (l1.val < l2.val){
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else{ //l1.val > l2.val
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

# 20. [Plus One](https://leetcode.com/problems/plus-one/)
1. O(n) space & time. Obv faster when no MSB is needed
```
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        for (int i = n-1; i >= 0; i--){ //start at LSB, decrement through arr
            if (digits[i] < 9){
                digits[i]++;
                return digits;
            }
            else digits[i] = 0;
        }
        
        //if no return from prev loop
        int[] newDigits = new int[n + 1];
        newDigits[0] = 1; //new MSB
        return newDigits;
    }
}
```

# 21. [Fizz Buzz](https://leetcode.com/problems/fizz-buzz/)
1. O(n) space & time
```
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> ans = new ArrayList<String>();
        for (int i = 1; i <= n; i++){
            if (i%3 == 0 && i%5 == 0){
                ans.add("FizzBuzz");
            }
            else if (i%3 == 0){
                ans.add("Fizz");
            }
            else if (i%5 == 0){
                ans.add("Buzz");
            }
            else {
                ans.add(Integer.toString(i));
            }
        }
        return ans;
    }
}
```

22. [Majority Element](https://leetcode.com/problems/majority-element/)
```
class Solution {
    public int majorityElement(int[] nums) {
        if (nums.length == 1){
            return nums[0];
        }
        
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i : nums){
            if (map.containsKey(i) && map.get(i) + 1 > nums.length/2){
                return i;
            }
            else{
                map.put(i, map.getOrDefault(i, 0) + 1);
            }
        }
        
        return -1;
    }
}
```

23. [Unique Email Addresses](https://leetcode.com/problems/unique-email-addresses/)
1. O(n) time and space
```
class Solution {
    public int numUniqueEmails(String[] emails) {
        HashSet<String> set = new HashSet<String>(); //hold # of valid emails
        
        for (String str : emails) { //sanitize and build local input
            
            StringBuilder cleanLocal = new StringBuilder();
            for (int i = 0; i < str.length(); ++i){
                char curr = str.charAt(i);
                
                if (curr == '+' || curr == '@') break;                
                if (curr != '.') cleanLocal.append(curr);
            }
            
            StringBuilder cleanDom = new StringBuilder();
            for (int i = str.length() - 1; i >= 0; --i){
                char curr = str.charAt(i);
                cleanDom.append(curr);
                if (curr == '@') break;
                }
            
            cleanDom = cleanDom.reverse();
            cleanLocal = cleanLocal.append(cleanDom);
            set.add(cleanLocal.toString());
        }
        
        return set.size();
    }
}
```

24. [License Key Formatting](https://leetcode.com/problems/license-key-formatting/)
1. O(n) time and space
```
class Solution {
    public String licenseKeyFormatting(String s, int k) {
            StringBuilder res = new StringBuilder();
            s = s.toUpperCase();
            int count = 0;
            
            //read in reverse to allow flexibility on first section
            for (int i = s.length() - 1; i >= 0; i--){
                char j = s.charAt(i);
                
                if (j != '-'){
                    if (count == k){
                        res.append('-');
                        count = 0;
                        res.append(j);
                        count++; //to catch edge cases
                    }
                    else{
                        res.append(j);
                        count++;
                    }
                }
            }
            
            //reverse res (s read into StringBuilder in reverse)
            //convert StringBuilder to String for output
            return res.reverse().toString();
        }
    }
```

25. [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
1. O(n) time, O(1) space thanks to hashmap
```
class Solution {
    public int totalFruit(int[] fruits) {  
        if (fruits == null || fruits.length == 0){
            return -1;
        } //error checking
        
        int max = 1;
        int i = 0; //leftmost
        int j = 0; //rightmost
        HashMap<Integer, Integer> map = new HashMap<Integer,Integer>();
        
        while (j < fruits.length){
            if (map.size() <= 2){
                map.put(fruits[j], j++); //k, v
            }
            if (map.size() > 2){
                int min = fruits.length - 1; //start large
                for (int val : map.values()){
                    min = Math.min(min, val); //find actual min
                }
                i = min + 1; //move leftmost pointer to the right
                map.remove(fruits[min]); //rm key
            }
            max = Math.max(max, j - i); //compare max to current substr len
        }
        return max;       
    }
}
```