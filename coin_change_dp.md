## Coin Change Problem

This is a note about approaching the coin change problem suing dynamic programming.

- Approach using a 2D matrix table.
- Approach using a 1D array.



### DP 2D Matrix Table Approach

``` cpp
int coinChangeDP2(vector<int>& coins, int target)
{
    sort(coins.begin(), coins.end());
    // initialize the table
    vector<vector<int>> T(coins.size()+1, vector<int>(target+1, 0));

    // initialize the first row
    for(int col = 1; col <= target; col++) T[0][col] = INT_MAX;

    // itr the row
    for(int row = 1; row <= coins.size(); row++)
    {
        for(int col = 1; col <= target; col++)
        {
            int x = (row-1 >= 0) ? T[row-1][col] : 1;
            int y = (col-coins[row-1] >= 0) ? T[row][col-coins[row-1]]+1 : INT_MAX;
            T[row][col] = min(x, y);
        }
    }
    return T[coins.size()][target];
}
```


### DP 1D Array Approach (reduce space from O(M*N) to O(N))

``` cpp
int coinChangeDP1(vector<int>& coins, int target)
{
    sort(coins.begin(), coins.end());
    // Declare/initialize the 1D array to remember the previous results
    vector<int> dp(target+1, INT_MAX);
    dp[0] = 0;

    // iterate through the coins
    for(int i = 0; i < coins.size(); i++)
    {
        // iterate from 1 up to target
        for(int j = 1; j <= target; j++)
        {
            int alternate = (j-coins[i] >= 0) ? dp[j-coins[i]]+1 : INT_MAX;
            dp[j] = min(dp[j], alternate);
        }
    }
    return dp[target];
}
```
