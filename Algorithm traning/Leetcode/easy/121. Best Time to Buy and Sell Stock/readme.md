### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

~~~python
class Solution:
    def maxProfit(self,prices):
        left = 0 # Buy
        right = 1 # Sell
        max_profit = 0
        while right < len(prices):
            currentProfit = prices[right] - prices[left]
            if prices[left] < prices[right]: # + profit
                max_profit =max(currentProfit,max_profit)
            else: # - profit
                left = right # Start from the new left
            right += 1
        return max_profit
~~~
