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

8. [Intersection of Two Arrays II]
1. Sorted solution, O(n)
```
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        int pointer1 = 0; //nums1 pointer
        int pointer2 = 0; //nums2 pointer
        ArrayList<Integer> list = new ArrayList<Integer>();
        Arrays.sort(nums1); Arrays.sort(nums2);
        
        while (true) {
            if (pointer1 >= nums1.length || pointer2 >= nums2.length){
                break; //length 0, exit loop
            }
            if (nums1[pointer1] == nums2[pointer2]){
                list.add(nums1[pointer1]);
                pointer1++;
                pointer2++;
            }
            else if (nums1[pointer1] > nums2[pointer2]){
                pointer2++;
            }
            else if (nums1[pointer1] < nums2[pointer2]){
                pointer1++;
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