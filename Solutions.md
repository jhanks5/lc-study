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

2. O(n) Python
```
class Solution:
    def isValid(self, s: str) -> bool:
        d = {"(":")", "{":"}", "[":"]"}
        stack = []
        
        for c in s:
            if c in d:
                stack.append(c)
            elif len(stack) == 0 or d[stack.pop()] != c:
                return False
        
        return len(stack) == 0
        
    # d[key] returns d[val], so in first testcase
    # d[stack.pop()] translates to ")" returned from dictionary
    # meaning ) != ) is not true, we exit loop and return bool for len(stack) == 0
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
```

O(n) time, O(1) memory Python code
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        l, r = 0, 1
        maxProfit = 0
        
        while r < len(prices):
            currProfit = prices[r] - prices[l]
            if prices[l] < prices[r]:
                maxProfit = max (currProfit, maxProfit)
            else:
                l = r
            r += 1
        
        return maxProfit
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

# 22. [Majority Element](https://leetcode.com/problems/majority-element/)
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

# 23. [Unique Email Addresses](https://leetcode.com/problems/unique-email-addresses/)
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

# 24. [License Key Formatting](https://leetcode.com/problems/license-key-formatting/)
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

# 25. [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
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

# 26. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
1. O(n)
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int max = 0;
        for (int i = 0, j = 0; i < s.length(); i++){
            if (map.containsKey(s.charAt(i))){
                j = Math.max(j, map.get(s.charAt(i))+1);
            }
            map.put(s.charAt(i), i);
            max = Math.max(max, i-j+1); //on the first pass, max becomes 1
            //every subsequent step find the longest substring
        }
        return max;
    }
}
```

2. O(n) time, O(n) space Python
```
        charSet = set()
        l, res = 0, 0
        
        for r in range(len(s)):
            while s[r] in charSet: # visited char is in set, update window
                charSet.remove(s[l])
                l += 1 # slide window
            charSet.add(s[r]) # r += 1 on following line also works
            res = max(res, r - l + 1)
        
        return res
```

# 27. [Same Tree](https://leetcode.com/problems/same-tree/)
1. Recursive O(n) solution (only takes as long as the smallest tree)
```
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null || q == null) return (p==q);
        if (p.val == q.val){ //roots would be the same
            return isSameTree(p.left, q.left) && isSameTree(p.right, q.right); //true, true, returns true
        }
        
        return false;
    }
}
```

# 28. [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/solution/)
```
class Solution {
    
    int diameter = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        dfs(root);
        return diameter;
    }
    
    private int dfs(TreeNode root){
        if (root == null) return 0;
        
        int depthLeft = dfs(root.left);
        int depthRight = dfs(root.right);
        
        diameter = Math.max(diameter, depthLeft + depthRight);
        
        return Math.max(depthLeft, depthRight) + 1;
    }
}
```

# 29. [Palindrome Number](https://leetcode.com/problems/palindrome-number/submissions/)
```
class Solution {
    public boolean isPalindrome(int x) {
        if (x == 0) return true; //0 is a palindrome
        if (x < 0 || x%10 == 0) return false; //negative or ends with 0, not a palindrome
        
        int reversed_x = 0;
        while (x > reversed_x) {
            int pop = x%10; //pop the end off x
            x = x / 10;
            reversed_x = (reversed_x * 10) + pop;
        }
        
        return (x==reversed_x || x==reversed_x/10);
    }
}
```

# 30. [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
```
class Solution {
    public boolean isPalindrome(String s) {
        int i = 0;
        int j = s.length() - 1;
        
        while (i < j){
            while(i<j && !Character.isLetterOrDigit(s.charAt(i))){
                i++;
            }
            while(i<j && !Character.isLetterOrDigit(s.charAt(j))){
                j--;
            }
            if (i<j && Character.toLowerCase(s.charAt(i++)) != Character.toLowerCase(s.charAt(j--))){
                return false;
            }
        }
        
        return true;
    }
}
```

- O(n)
```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l = 0
        r = len(s) - 1
        
        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
            if s[l].lower() != s[r].lower():
                return False
            l += 1
            r -= 1
        
        return True
```

# 31. [BackSpace Compare](https://leetcode.com/problems/backspace-string-compare/)
```
class Solution {
    public boolean backspaceCompare(String s, String t) {
        return buildStr(s).equals(buildStr(t)); //compare two strings with helper function
    }
    
    private String buildStr(String str){
        StringBuilder sb = new StringBuilder();
        
        for (char c : str.toCharArray()){
            if (c != '#'){ //valid char
                sb.append(c);
            }
            else if (sb.length() != 0){ //backspace
                sb.deleteCharAt(sb.length() - 1);
            }
        }
        
        return sb.toString(); //fully built str with no #
    }
}
```

# 32. [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
- Was able to brute force a few test cases for this using a splitting algorithm before going with this solution from discussions.
```
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        
        return slow;
    }
}
```

# 33. [3Sum](https://leetcode.com/problems/3sum/)
- O(n^2)
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort() # O(nlogn)
        
        for i, a in enumerate(nums): # index, val
            if i > 0 and a == nums[i - 1]: # avoid duplicates
                continue
                
            l, r = i + 1, len(nums) - 1 # start two pointer after i
            while l < r:
                threeSum = a + nums[l] + nums[r]
                if threeSum > 0:
                    r -= 1
                elif threeSum < 0:
                    l += 1
                else:
                    res.append([a, nums[l], nums[r]])
                    l += 1
                    while nums[l] == nums[l-1] and l < r: # avoid duplicate
                        l += 1
                        
        return res
```

# 34. [Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- O(n), two pointers
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        l = 0
        r = len(nums) - 1
        res = []
        
        while l < r:
            twoSum = nums[r] + nums[l]
            if twoSum == target:
                res.extend((l + 1, r + 1))
                return res
            elif twoSum > target:
                r -= 1
            elif twoSum < target:
                l += 1
        
        return res # for edge cases
```

# 35. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- O(n)
```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        res = 0
        
        while l < r:
            minHeight = min(height[l], height[r])  # take min to get largest possible container
            length = r - l
            area = length * minHeight
            res = max(res, area) # find largest possible area
            if height[l] < height[r]:
                l += 1
            else: # height[r] <= height[l] cases
                r -= 1
        
        return res
```

# 36. [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

1. O(n) space, O(n) memory
```
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = {}
        l, res, maxFreq = 0, 0, 0
        
        for r in range(len(s)):
            count[s[r]] = 1 + count.get(s[r], 0)
            maxFreq = max(maxFreq, count[s[r]]) # find longest substring
            # windowLen = r - l + 1; must be computed in place
            if r - l + 1 - maxFreq > k: # insufficient replacements available
                count[s[l]] -= 1
                l += 1 # slide window
                
            res = max(res, r - l + 1)
            
        return res
```

# 37. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
1. O(n) time
```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if t == "": return "" # empty str edgecase
        
        tCount, window = {}, {} # initialize hashmaps
        
        for c in t: # populate tCount
            tCount[c] = 1 + tCount.get(c, 0)
            
        have, need = 0, len(tCount) # initialize keeper vals for hashmaps
        res, resLen = [-1, -1], float("infinity") # infinity bc taking min
        l = 0
        for r in range(len(s)):
            c = s[r]
            window[c] = 1 + window.get(c, 0) # count char in s for window
            
            if c in tCount and window[c] == tCount[c]: # check if t contains c (from window)
                have += 1
            
            while have == need: # all chars required are in window
                if (r - l + 1) < resLen: # minimizing window
                    res = [l, r]
                    resLen = (r - l + 1)
                window[s[l]] -= 1 # remove char from left of window
                if s[l] in tCount and window[s[l]] < tCount[s[l]]: # no longer have needed char
                    have -= 1
                l += 1 # slide window to the right
                
        l, r = res # retrieve window size
        return s[l:r+1] if resLen != float("infinity") else ""
        # checking that resLen was updated, because answer may not exist
```

# 38. [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- O(logn) solution
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] == target:
                return mid
            
            if nums[l] <= nums[mid]: # left portion
                if nums[l] > target or target > nums[mid]: # L is to right of target, OR target is to right of MID
                    l = mid + 1 # move to right side of sorted array
                else: # L is to the left of target, OR target is to the LEFT of mid
                    r = mid - 1 # move to left side of sorted array
            else: # right portion
                if nums[r] < target or target < nums[mid]:
                    r = mid - 1
                else:
                    l = mid + 1
            
        return -1
```

# 39. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
1. O(n) with explanation
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev, curr = None, head # initialize null pointer prior to start of list
        
        while curr:
            temp = curr.next # placeholder for next value in list
            curr.next = prev # reversal of list pointer
            prev = curr # shift prev pointer
            curr = temp # set curr (1 on first pass) to curr.next (2 on first pass)
            # 2 1 3 4 5 at end of first pass, with 1 as curr and 2 as prev
            # both pointers are shifting to the right each pass
            # simply reversing the list pointers (see function of curr.next), NOT exchanging values
    
        return prev
```

# 40. [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
1. O(n + m) time, O(1) space
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        tail = dummy
        
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next # increment
        
        # checking for null list (in case of uneven length)
        # readability, but can be simplified to tail.next = l1 or l2
        if l1: # l2 is null
            tail.next = l1
        else:
            tail.next = l2
        
        return dummy.next
```

# 41. [Reorder List](https://leetcode.com/problems/reorder-list/)
1. O(n) time, O(1) space
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        slow = head
        fast = head.next
        
        # find middle
        while fast and fast.next: # until last val in list
            slow = slow.next # slow pointer ends at middle
            fast = fast.next.next
        
        # reverse second half of list
        curr = slow.next
        prev = slow.next = None
        while curr:
            temp = curr.next
            curr.next = prev
            prev = curr
            curr = temp
        
        # merge the two lists, first and second half
        first, second = head, prev
        while second:
            temp = first.next
            first.next = second
            first = temp
            
            temp = second.next
            second.next = first
            second = temp
```

42. [Remove Nth Node from End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
1. O(n), two pointer solution
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        left = dummy
        right = head
        
        while n > 0:
            right = right.next
            n -= 1
        
        while right:
            left = left.next
            right = right.next
        
        # delete, left is curr.prev.prev to node to be deleted
        left.next = left.next.next
        return dummy.next
```

43. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
1. O(n), Floyd's Cycle Finding Algorithm, Tortoise and Hare
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if head is None:
            return False
        
        slow = head
        fast = head.next
        
        while slow != fast:
            if fast is None or fast.next is None:
                return False
            fast = fast.next.next
            slow = slow.next
        
        return True
```

44. [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
1. O(log k), where k is the number of lists. Requires you to know how to merge sorted linked lists.
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        if not lists or len(lists) == 0:
            return None
        
        while len(lists) > 1:
            mergedLists = []
            for i in range(0, len(lists), 2):
                l1 = lists[i]
                l2 = lists[i + 1] if i + 1 < len(lists) else None
                mergedLists.append(self.mergeList(l1, l2))
            lists = mergedLists
        return lists[0]
                
        
    def mergeList(self, l1, l2):
        dummy = ListNode()
        tail = dummy    
        
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        if l1:
            tail.next = l1
        if l2:
            tail.next = l2
        return dummy.next
```

45. [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
1. O(n) time/space
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        
        root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
        
        return root
```

46. [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
1. O(n) time/space
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        if not root.left and not root.right:
            return 1
        
        leftHeight = 1 + self.maxDepth(root.left)
        rightHeight = 1 + self.maxDepth(root.right)
        
        return max(leftHeight, rightHeight)
```

47. [Same Tree](https://leetcode.com/problems/same-tree/)
1. O(n)
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:    
        if not p and not q:
            return True
        if not p or not q:
            return False
        if p.val != q.val:
            return False
            
        return self.isSameTree(p.right,q.right) and self.isSameTree(p.left, q.left)
```

48. [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
1. O(n*m)
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not subRoot:
            return True
        if not root:
            return False
        if self.sameTree(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
        
    def sameTree(self, root, subRoot) -> bool:
        if not root and not subRoot:
            return True
        if root and subRoot and root.val == subRoot.val:
            return self.sameTree(root.left, subRoot.left) and self.sameTree(root.right, subRoot.right)
        return False
```

49. [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
1. O(n)
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        parentVal = root.val
        pVal = p.val
        qVal = q.val
        
        if pVal > parentVal and qVal > parentVal:
            return self.lowestCommonAncestor(root.right, p, q)
        if pVal < parentVal and qVal < parentVal:
            return self.lowestCommonAncestor(root.left, p, q)
        return root
```

50. [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
1. Recursive O(n)
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        
        def validate(node, left, right):
            if node is None:
                return True
            if not (node.val > left and node.val < right):
                return False
            return validate(node.left, left, node.val) and validate(node.right, node.val, right)
            
        return validate(root, float("-inf"), float("inf"))
```

51. [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
1. DFS inorder traversal O(n) solution
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        
        def inorder(root):
            return inorder(root.left) + [root.val] + inorder(root.right) if root else []
        
        return inorder(root)[k-1]
```
2. DFS inorder iterative solution, easier to understand
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        curr = root
        
        while stack or curr:
            while curr:
                stack.append(curr)
                curr = curr.left
            curr = stack.pop() # occurs when curr.left == null
            k -= 1
            if k == 0:
                return curr.val
            curr = curr.right # check right child after processing left
```

52. [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
1. O(n)
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder or not inorder:
            return None
        
        root = TreeNode(preorder[0])
        mid = inorder.index(preorder[0]) # values to the left are left sub-tree, right is right sub-tree
        root.left = self.buildTree(preorder[1:mid + 1], inorder[:mid]) # end of sub-array is not inclusive in python
        root.right = self.buildTree(preorder[mid + 1:], inorder[mid + 1:])
        return root
```

- Important to understand for this problem:
    - Inorder traversal means that `root` is in the middle: the values to the left are in the left sub-tree, and the values to the right are in the right sub-tree.
    - Preorder traversal, the `root` is always the first item in the list.

53. [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
1. O(n) memory, O(tree_height) space
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res = [root.val]
        
        # return max path sum without split
        def dfs(root):
            if not root:
                return 0
            
            leftMax = dfs(root.left)
            rightMax = dfs(root.right)
            
            # catch negative cases
            leftMax = max(leftMax, 0)
            rightMax = max(rightMax, 0)
            
            # compute max path sum WITH split
            res[0] = max(res[0], root.val + leftMax + rightMax)
            # without split, for finding max path sums of sub-trees
            return root.val + max(leftMax, rightMax)
        
        dfs(root)
        return res[0]
```

- Main reason this problem is a `Hard` problem is the negative cases. Finding the max on each function call between 0 and `${side}Max` catches this.
- Important to note the return value of the `dfs` helper function is specifically for DFS on the sub-trees, NOT finding the `res` as the return value for `dfs`.
- "Can the values be negative?" would be an important question to clarify with an interviewer on a problem like this.

54. [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
1. O(n) time/space
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Codec:
    
    """Encodes a tree to a single string.
        :type root: TreeNode
        :rtype: str
        """
        
    def serialize(self, root):
        res = []
        
        def dfs(node):
            if not node:
                res.append("null")
                return
            res.append(str(node.val))
            dfs(node.left)
            dfs(node.right)
        
        dfs(root)
        return ",".join(res)

    """Decodes your encoded data to tree.    
        :type data: str
        :rtype: TreeNode
        """
        
    def deserialize(self, data):
        vals = data.split(",")
        self.i = 0
        
        def dfs():
            if vals[self.i] == "null":
                self.i += 1
                return None
            node = TreeNode(int(vals[self.i]))
            self.i += 1
            node.left = dfs()
            node.right = dfs()
            return node
        
        return dfs()

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

- Don't overcomplicate it when you decide the delimiters.
- Setting global indices and data structures is very helpful during helper function + recursion approaches.

55. [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
1. Insertion: O(n * maxLen) / Search: O(maxLen) / Space: O(n * maxlen)
```
class TrieNode:
    def __init__(self):
        self.children = {}
        self.endOfWord = False

class Trie:

    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        curr = self.root
        
        for char in word:
            if char not in curr.children:
                curr.children[char] = TrieNode() # add to hashmap
            curr = curr.children[char] # iterate
            
        curr.endOfWord = True 
        
    def search(self, word: str) -> bool:
        curr = self.root
        
        for char in word:
            if char not in curr.children:
                return False
            curr = curr.children[char] # iterate
            
        return curr.endOfWord 

    def startsWith(self, prefix: str) -> bool:
        curr = self.root
        
        for char in prefix:
            if char not in curr.children:
                return False
            curr = curr.children[char]
        
        return True

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

56. [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)
1. O(n) where n is word length
```
class TrieNode:
    def __init__(self):
        self.children= {}
        self.word = False

class WordDictionary:

    def __init__(self):
        self.root = TrieNode()
        

    def addWord(self, word: str) -> None:
        curr = self.root
        for char in word:
            if char not in curr.children:
                curr.children[char] = TrieNode()
            curr = curr.children[char]
        curr.word = True

    def search(self, word: str) -> bool:
        def dfs(j, root):
            curr = root
            
            for i in range(j, len(word)):
                char = word[i]
                if char == ".":
                    for child in curr.children.values():
                        if dfs(i + 1, child):
                            return True
                    return False
                else:
                    if char not in curr.children:
                        return False
                    curr = curr.children[char]
            return curr.word
        return dfs(0, self.root)
        
# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```

57. [Word Search 2](https://leetcode.com/problems/word-search-ii/)
1. LC solution
```
class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        WORD_KEY = '$'
        
        trie = {}
        for word in words:
            node = trie
            for letter in word:
                # retrieve the next node; If not found, create a empty node.
                node = node.setdefault(letter, {})
            # mark the existence of a word in trie node
            node[WORD_KEY] = word
        
        rowNum = len(board)
        colNum = len(board[0])
        
        matchedWords = []
        
        def backtracking(row, col, parent):    
            
            letter = board[row][col]
            currNode = parent[letter]
            
            # check if we find a match of word
            word_match = currNode.pop(WORD_KEY, False)
            if word_match:
                # also we removed the matched word to avoid duplicates,
                #   as well as avoiding using set() for results.
                matchedWords.append(word_match)
            
            # Before the EXPLORATION, mark the cell as visited 
            board[row][col] = '#'
            
            # Explore the neighbors in 4 directions, i.e. up, right, down, left
            for (rowOffset, colOffset) in [(-1, 0), (0, 1), (1, 0), (0, -1)]:
                newRow, newCol = row + rowOffset, col + colOffset     
                if newRow < 0 or newRow >= rowNum or newCol < 0 or newCol >= colNum:
                    continue
                if not board[newRow][newCol] in currNode:
                    continue
                backtracking(newRow, newCol, currNode)
        
            # End of EXPLORATION, we restore the cell
            board[row][col] = letter
        
            # Optimization: incrementally remove the matched leaf node in Trie.
            if not currNode:
                parent.pop(letter)

        for row in range(rowNum):
            for col in range(colNum):
                # starting from each of the cells
                if board[row][col] in trie:
                    backtracking(row, col, trie)
        
        return matchedWords
```

58. [Find Median From Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)
1. Good example of heaps from a LC hard
```
class MedianFinder:

    def __init__(self):
        self.small, self.large = [], []

    def addNum(self, num: int) -> None:
        heapq.heappush(self.small, -1 * num)
        
        # make sure every num small is <= every num in large
        if (self.small and self.large 
            and (-1 * self.small[0]) > self.large[0]):
            val = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large, val)
            
        # uneven size?
        if len(self.small) > len(self.large) + 1:
            val = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        if len(self.large) > len(self.small) + 1:
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -1 * val)
        

    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -1 * self.small[0]
        elif len(self.large) > len(self.small):
            return self.large[0]
        return (-1 * self.small[0] + self.large[0]) / 2

# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```