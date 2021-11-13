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
```