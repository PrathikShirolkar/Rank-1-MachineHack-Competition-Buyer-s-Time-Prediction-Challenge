# Rank-1-MachineHack-Competition-Buyers-Time-Prediction-Challenge

My approach to solving the "Buyers Time Prediction Challenge"(https://machinehack.com/hackathon/buyers_time_prediction_challenge/overview) was very simple. It was to concentrate a lot on feature engineering and spend very little time on modelling.

Some of the feature engineering done, were
1.	manually classify client agents into hand held devices and desktops
2.	Extracting the browser version.
3.	Creating a combined feature for “purchased”, “added_in_cart” and “checked_out” into one feature, and giving numeric weights to them
4.	Calculating Daily average traffic and some other features from client_agent feature
5.	Using a tfidf vectorizer for both characters and words

Some things I focused on was to create the cross validation strategy in such a way that the proportions match that of the actual train and test data provided.
I built 3 models using
1.	CatBoost
2.	XGBoost and
3.	LightGBM
I found that the results were LightGBM were the best, and XGB the worst.
LightGBM predicted all values within a certain small range, while XGB’s range was pretty wide, and CatBoost performed in the middle.

I quickly realized that I had to incorporate the variance provided by XGB but in a controlled way

Hence I took the weighted average of all the above 3 models, giving
	50% weightage to LightGBM
	45% weightage to CatBoost and
	5% weightage to XGBoost
The above numbers arent magic numbers, I arrived at them by considering the combined cv for multiple permutations of weights.

I did try Stacking these models, but a simple weighted average proved to be better for me.
