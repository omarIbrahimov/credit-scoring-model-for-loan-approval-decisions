1. Data preparation
	- 
	- Mapping
		First, we mapped all the numerical values to their human-readible format to better understand the contents of the data.
	- Give 0 to good and 1 to bad
		I decided to give 0 tot good credits and 1 to bad ones. In that way marking bad credits would result in 1.
	- Little Analysis
		The analysis showed that 700 out of 1000 (70%) credits were good. The others were bad. Also we got a table of mean, median and std for different categories for both good and bad credits with graphs to understand everything visually. For some other categories, we got the percentage of the bad credits for their values.


	- Train/test splitting
		Train/test split by 80/20. We have 70% of good and 30% bad in each of training and testing sets.

	- Encoding
	Give One-Hot Encoding and Ordinal Encoding to the corresponding features

2. Models
	-

	- First, I put Logistic Regression model with Standard Scaler.
		This is the industry standard so I put it to both see the general results, and also compare with XGBoost in the future.

	- Balancing everything
		After balancing everything using (class_weight = "balanced"). The comparison table for unweighted and weighted results.

	- XGBoost
		I used XGBoost and the results are in the notebook.

	- Comparison between models
		Test ROC-AUC
		Logistic regression (baseline): 0.76
XGBoost (calibrated): **0.81**
As seen, XGBoost did a better job.

3. Threshold selection
	-

	For threshold selection, I created a graph of cost to see the cost at each point of the threshold. The result at 0.5 was 179 and the best result 99 appeared at 0.20 threshold. However, to not miss good clients, I manually raised it to 0.35 with cost of 119.

4. SHAP
	- 
 
SHAP was computed on the XGBoost model. Reading the global beeswarm plot:

Push risk up:

- Longer loan duration and larger credit amount.

- High installment rate (a larger share of income going to repayments).

- No known property (Property Unknown/No Property).

- Having a checking account with a balance (see caveat below).


Push risk down:

- Longer employment.

- No other installment plans.

- Purpose = used car.

- Critical account / other credits existing (see caveat below).

- Older age (small effect).
