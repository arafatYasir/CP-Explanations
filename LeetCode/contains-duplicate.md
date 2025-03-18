# Intuition
So basically this is a simple problem. Which asks us to check weather an array contains any duplicate values.

There are three solution strategies for this problem.

## Strategy 1
The first strategy is simple. Most beginners will think about the brute-force solution, which involves using two for loops (nested) to check the whole array to see if there is any duplicate value.

**Time:** O(n^2) → Since we are using nested for loops.

**Space:** O(1) → Since we are not using any extra memory.

**Code:**
```cpp
bool containsDuplicate(vector<int> &nums)
{
    for (int i = 0; i < nums.size(); i++)
    {
        for (int j = 0; j < nums.size(); j++)
        {
            if (nums[i] == nums[j] && i != j)
            {
                return true;
            }
        }
    }
    return false;
}
```
**Note**: If you submit this code you will get TLE.

## Strategy 2
The second strategy is cunning. Let’s say we sort the array in ascending or even descending order. No matter how we sort the array the duplicate values will be side-by-side or adjacent values. So then we can simply check `if(nums[i] == nums[i + 1]) return true;` as simple as it is. It’s much faster than the previous solution. Since the `sort()` function in C++ takes O(n log n) time so this is faster.

**Time:** O(n log n) → We are sorting the array and iterating over it once, so combining both of them will be O(n log n) + O(n). In these cases, we take the biggest notation.

**Space:** O(1) → We are not using any extra memory.

**Code:**
```cpp
bool containsDuplicate(vector<int> &nums)
{
    sort(nums.begin(), nums.end());
    for (int i = 0; i < nums.size() - 1; i++)
    {
        if (nums[i] == nums[i + 1])
        {
            return true;
        }
    }
    return false;
}
```

## Strategy 3
This is going to be the most optimal solution. Now we can think of an O(n) solution. So for that, we have to use a set or a map. Yes, we have to use extra memory to reduce the time. We will just iterate through the array once and every time we get a value we will check if the same value is already present inside our set. If it is true that means already we have the same value in our set and we are getting it again. Finally, it’s clear that we got a duplicate! But if the condition is false, then we can simply insert the value inside our set.

Now maybe you are thinking how is that solution O(n)? It seems like the first strategy. No! It’s not. The fun fact is that we can check if a value is present inside a set/map in O(1) time! It doesn’t take O(n) time.

**Time:** O(n) → Because we are iterating through the array.

**Space:** O(n) → In the worst case we will have to put n - 1 values inside our set.

**Code:**
```cpp
bool containsDuplicate(vector<int> &nums)
{
    unordered_set<int> check;

    for (int i = 0; i < nums.size(); i++)
    {
        if (check.find(nums[i]) != check.end()) // checking if the values is present
        {
            return true;
        }
        check.insert(nums[i]); // inserting the value in set
    }
    return false;
}
```