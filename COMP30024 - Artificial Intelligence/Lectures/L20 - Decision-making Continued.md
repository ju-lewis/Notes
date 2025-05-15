# Decision Networks
**(AKA Influence diagrams)**

- Chance nodes (ovals) represent uncertainty
- Decision nodes (rectangles) represent choices
- Utility nodes (diamonds) represent preferences

These are developed from [[L17 - Bayesian Networks|Bayesian Networks]]

## Algorithm
For each value of the action (decision) node:
- Compute the expected value of the utility node, given the action and evidence
Return the action that maximises expected utility

Determining the best value to take becomes very similar to [[L8 - Adversarial Search Continued#Expectiminimax|expectiminimax]]
- (It could be considered expectimax)

We can use a similar algorithm


## Value of Information
One of the most important parts of decision making is knowing what questions to ask
- Deciding what information is valuable


>[!Example]
>With the "should you bring an umbrella" example, we can consider two scenarios:
>- **Forecast received**: base decision on the forecast
>- **No forecast**: Base decision on prior probability of rain

Initial information state:
$$EU(\text{action}^*) = \sum_{\text{outcome}}P(\text{outcome }|\text{ action}) \times U(\text{outcome})$$
After observing evidence:
$$EU(\text{action}^*|e_j) = \sum_{\text{outcome}}P(\text{outcome }|\text{ action}, e_j) \times U(\text{outcome})$$
- These are both just "weighted means"


>[!Info]
>VPI = Value of Perfect Information
>- Difference in expected utility between decisions with and without the forecast


- High confidence, high stakes -> information has little value
- High uncertainty, high stakes -> information is valuable
- High uncertainty, low stakes   -> information not valuable

