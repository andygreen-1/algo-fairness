# Disparate Impact Testing Framework

This is an example framework that lenders can use to conduct disparate impact testing and mitigate fair lending risk.

## Scope
- Testing should start with the approve/decline decision, but it should also extend to other aspects of credit decisioning --- APR/pricing, credit lines/loan amounts, etc.
- Testing should focus on the full set of factors that contribute to decision-making --- models, decision thresholds, hard diqualification rules, etc.

## Identifying Disparities
- Should include a measure of outcomes-based disparities, such as the Adverse Impact Ratio (AIR)
- Optionally, may also include a measure of differential validity-based disparities, such as the False Positive Rate (FPR)
- Key thresholds that determine if remediation is necessary should be set in policy
    - Commonly accepted AIR thresholds include 80% and 90%
- Metric conflicts are common when dealing with different types of fairness. If multiple metrics are used to identify disparities, policy should provide clear logic for how metric conflicts will be handled
    - See [here](https://openbanker.beehiiv.com/p/algorithmicfairness) for a practical example of reconciling between outcomes-based and differential validity-based metrics

## LDA Search
- LDA searches often focus on models, but they should additionally focus on non-model factors if those factors meaningfully contribute to disparities
- Lenders should set a reasonable band of accuracy loss that they can accept while still meeting their business need. There are many different ways to set this value, including:
    - Considering how much accuracy loss they accept to meet other goals (e.g., choosing not to use variables in their model due to reputational risk or regulatory risk; limiting the number of variables in their model or the complexity of their model architecture due to computational cost or logistical challenges)
    - Rigorously testing how small changes in model accuracy affect profitability (e.g., using an LDA model that is less accurate than the incumbent model by X% to make decisions for randomly selected applicants and measuring how profitability is affected).
- Conduct a robust LDA search using rigorous debiasing methods (i.e., not "drop one")
- Evaluate the candidate LDA models relative to the incumbent model using a fairness-accuracy tradeoff framework
    - The fairness metric is the disparity that they're trying to reduce (e.g., AIR for group X)
    - The accuracy metric is the lender's preferred accuracy metric
- The lender may decide to adopt the LDA model that offers the largest fairness gains while remaining within their acceptable band of accuracy loss. Alternatively, they may find a candidate LDA model that offers a slightly smaller improvement to fairness, but has a more appealing ratio of fairness improvement to accuracy loss.
- Confirm that the candidate LDA model would not violate other conditions set in policy (e.g., improving disparities for group X while creating new disparities for group Y)

