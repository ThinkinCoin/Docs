# Governance Risk Framework \(Part 2\)

The less liquidity available in the market, the more likely the price impact will work against realizable value and the higher the volatility of the collateral value, the less likely we are to recover the full loan in the event of default.

Liquidity risk involves evaluating the liquidity of an asset in the market while volatility examines the risk associated with large swings in the market value of a token.

To evaluate the risk associated with the liquidity of a token, we need to consider the relationship between liquidity and free float. Free float is the readily traded portion of the available supply of tokens — the amount not held over the long term by founders and large institutions. Therefore, any real liquidity presented in the market is a result of the free float.

The Debt Ceiling helps mitigate the risk of creating an illiquid market. We include a predetermined maximum amount of time to liquidate the position and adjust the collateral calculation for it.

From volatility risk we can calculate the initial amount of required capital and make a liquidity adjustment to the calculation. Given the length of time to liquidate that collateral, the final change would be the time — or expected liquidation period.

## Example <a id="example"></a>

How much gold would be needed to collateralize a $100 loan? If the volatility of the price of gold is 10% per day, you would probably want something around $125. If you're conservative, you would probably want twice the volatility of the daily price incorporated into the collateral value, which is conservative as the chance of the price falling by 20% in one day is very small.

The collateral we would need would be $100/0.8 = $125, or, put another way, starting at $125: if the collateral value drops by 20% that would equal a $25 loss in value but we would still have \$100 in value which is enough to cover the outstanding loan, given nothing is paid back.

Now we include the Liquidity Risk Factor. We have assumed that $125 of gold would be sufficient to cover the $100 loan. What about a $1m loan? Well we know the amount of collateral we would need is $1.25m, but getting rid of $1.25m in gold is a more complicated problem than getting rid of $125 of gold. We have to consider the liquidity of the market yet again.

What is required is an adjustment of the collateral value to compensate for liquidity risk. If we assume the liquidity adjustment is 1.15 or an increase of 15% in value. Then the final collateral value required would be \$1.435m.

Given the volatility risk, and a uniform application of the liquidity risk adjustment, we have determined that to borrow $100 one would need to pledge $143.50 in collateral.

The outstanding issue is the duration of the loan. If the loan is for longer than a day, then more collateral needs to be posted or an adjustment to the collateral needs to be performed on a daily basis.

Considering the loans in MakerDAO are open-ended, we don't need a massive amount of collateral. Unlike a traditional loan, loans of Dai are immediately liquidated if a default occurs.

The applicable period to consider is then the length of time to liquidate the position. So we will include a predetermined maximum amount of time to liquidate the position and adjust the collateral calculation for it.

To summarize, from volatility risk we can calculate the initial amount of required capital, from liquidity risk we can make a liquidity adjustment to the calculation. Given the length of time to liquidate that collateral, the final change would be the expected liquidation period.

## Risk Management Function <a id="risk-management-function-4"></a>

The liquidation ratio is the required amount of collateral as a proportion of the loan.

So in our example, if we consider that from volatility the necessary amount of gold as collateral was $125. Then after adjusting for liquidity, it was $143.50, then adjusting for the expected liquidation period it turned out to be $175. The liquidation ratio would then be $175/\$100 = 175%. So the liquidation ratio can be generally approximated by:

![liquidation ratio calculation](https://cdn-images-1.medium.com/max/1600/1*hr05cBlHByBkFK3_kEOv5g.png)

Where the VaR term is the value at risk at a given confidence level, an idea and calculation we will explore further in a more detailed paper focussed on the liquidation ratio.

Participants in the system liquidate the collateral if the collateral to debt ratio falls to or below this level. A level that ensures, given certain confidence, the collateral when liquidated should be sufficient to recover the loan. With any excess collateral returned to the borrower. If the collateral is insufficient, MKR token holders will be diluted to make up for any outstanding part of the loan that has not recovered.

