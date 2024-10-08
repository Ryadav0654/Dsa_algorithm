# Kadane's Algorithm : Maximum Subarray Sum in an Array

> Question link: https://www.naukri.com/code360/problems/630526?topList=striver-sde-sheet-problems&leftPanelTabValue=SUBMISSION

> https://leetcode.com/problems/maximum-subarray/description/

## Intuition:

The intuition of the algorithm is not to consider the subarray as a part of the answer if its sum is less than 0. **`A subarray with a sum less than 0 will always reduce our answer and so this type of subarray cannot be a part of the subarray with maximum sum.`**

- Here, we will iterate the given array with a single loop and while iterating we will add the elements in a sum variable. Now, `if at any point the sum becomes less than 0, we will set the sum as 0 as we are not going to consider any subarray with a negative sum.` Among all the sums calculated, we will consider the maximum one.

- Thus we can solve this problem with a single loop.

## Approach:

The steps are as follows:

- We will run a loop(say i) to iterate the given array.
- Now, while iterating we will add the elements to the sum variable and consider the maximum one.
- If at any point the sum becomes negative we will set the sum to 0 as we are not going to consider it as a part of our answer.
- **Note**: In some cases, the question might say to consider the sum of the empty subarray while solving this problem. So, in these cases, before returning the answer we will compare the maximum subarray sum calculated with 0(i.e. The sum of an empty subarray is 0). And after that, we will return the maximum one.
- `For e.g. if the given array is {-1, -4, -5}, the answer will be 0 instead of -1 in this case.`

- But if this case is not explicitly mentioned we will not consider this case.

## Code:

```C++
int maxSubArray(vector<int>& nums) {
    int n = nums.size();
    // initialise two variable sum and maxi to track the sum and maximum sum
    int sum = 0;
    int maxi = INT_MIN;

    // applying the algorithm
    for(int i = 0; i < n; i++){
        // add the element in sum
        sum += nums[i];

        // if sum is greater than maxi we will set it
        maxi = max(sum, maxi);

        // if sum becomes less than 0 we will set it to 0

        if(sum < 0){
            sum = 0;
        }
    }

    // if the maximum sum is 0 that means that it is not possible to make a subarray with a sum greater than zero
    return maxi;
}
```

**Time Complexity:**` O(N)`, where N = size of the array.

- Reason: We are using a single loop running N times.

**Space Complexity:** `O(1)`as we are not using any extra space.

## Follow-up question:

There might be more than one subarray with the maximum sum. We need to print any of them.

## Intuition:

Our approach is to store the `starting index` and the `ending index of the subarray`. Thus we can easily get the subarray afterward without actually storing the subarray elements.

If we carefully observe our algorithm, we can notice that the subarray always starts at the particular index where the sum variable is equal to 0, and at the ending index, the sum always crosses the previous maximum sum(i.e. maxi).

- So, we will keep a track of the starting index inside the loop using a start variable.
- We will take two variables ansStart and ansEnd initialized with -1. And when the sum crosses the maximum sum, we will set ansStart to the start variable and ansEnd to the current index i.e. i.
- The rest of the approach will be the same as Kadane’s Algorithm.

## Code:

```C++
vector<int> maxset(vector<int> &nums, int n) {
    // initialise two variable sum and maxi to track the sum and maximum sum
    long long maxi = LONG_MIN;
    int sum = 0;
    int start = 0;
    // initialise two variable ansstart and ansend to track the subarray start and end index
    int ansstart = -1;
    int ansend = -1;

    // applying the algorithm
    for(int i = 0; i < n; i++){
        //if sum is equal to 0 we will set start to i
        if(sum == 0){
            start = i;
        }

        // add the element in sum
        sum += nums[i];

        // if sum is greater than maxi we will set it
        // and also set the ansstart and ansend
        if (sum > maxi) {
            maxi = sum;
            ansStart = start;
            ansEnd = i;
        }

        // if sum becomes less than 0 we will set it to 0
         if (sum < 0) {
            sum = 0;
        }
    }

    vector<int> ans;
    for(int i = ansStart; i <= ansEnd; i++){
        ans.push_back(nums[i]);
    }

    return ans;
}
```
**Time Complexity:** `O(N)`, where N = size of the array.
Reason: We are using a single loop running N times.

**Space Complexity:** `O(K)` , where K = size of the subarray.