### ***Project 3 Feedback***

***Nico Van de Bovenkamp***

***

**Overall:**  
Great work on this assignment! You worked through every fundamental step to successfully model your data! You even built out a logistic regression AND a KNN. Also, great point on dropping the `sum_precip` feature from your prediction task. It may have been obvious to you, but it is an easy thing to miss! There may be an argument for visibility also being some data leakage as most low visibility is actually because there *is* some precipitation.

I noticed your comments at the end of your notebook. Those are all very, very good questions. I know this homework assignment was submitted before my review session, so I hope some of those questions have been clarified. Nonetheless, I'll walk through a few of them here so that you have some of your own code to contextualize those lessons! **Please let me know if you have any questions on your hw feedback.**

**Some Notes**  

* **Train/test Split earlier** As we discussed in our review session, the first thing that you want to do is perform your train/test split (once you have your data). You don't want any information about your test set to "leak" into what you are learning about your training set. All preprocessing, transformations, handling of missing values, etc. should be done on your train set as the goal is to have it generalize onto your test set. Again, the concept is: "We don't have the test yet, that comes tomorrow."
* **Shaping your data to solve the problem**  Now, this note is a bit of an aside, but an interesting one. You want to frame your analysis/data such that it solves the problem. In this formulation, you are actually predicting if it will rain "today" given the weather information of the same day. This is *okay*, but what might be more interesting is to predict if it will rain the **next** day. What you could do is iterate through the rows and label that row a `1` if it rained on the day after! It is always a good idea to keep the "use" of your model in mind. How would you want to "predict" and when?
* **Hyperparameter optimization**  As we discussed in our review session, once you have decided on a solid set of features, you want to do some level of hyper parameter tuning. You currently aren't adding any penalty to your model, which could help with some over-fitting (though, honestly, there isn't much overfitting going on. You can tell because your out-of-sample error on your cross-validations are not much lower than your train errors.).
    - Logistic regression:
        - C : Amount of penalty you apply to your weights! Remember that in this implementation, it is actually 1/C. Thus, a smaller C means more penalty as you are adding MORE of the weights to the penalty.
        - penalty: 'l1' vs. 'l2'
        - fit_intercept : (this is a parameter, but you likely always use this term)
        - solver : {‘newton-cg’, ‘lbfgs’, ‘liblinear’, ‘sag’, ‘saga’} this is your term to change the optimization procedure! These can be interesting to experiment with. On a smaller dataset, this may not be so important, but when datasets become huge... This is very important.
* **Scoring functions**  A quick note on passing values into the scoring functions: you want to pass the **TRUE** labels in first and then the **PREDICTED** in second: `accuracy_score(y_train, preds)`
* **Using different models**  So, why would you want to use LogisticRegression vs. KNN? I hope you have a better idea after our review session, but here are some points:
    - **Model structure**  Logistic regression is modeling the probability of a class occurring, given some data, to make a linear classification boundary. KNN does not have a model form, it is just empirically taking the structure of your training data and hoping that there is some local information given your data that will have once class be closer to another class (distance).
    - **Model output**  Logistic regression output model probabilities. This means that we can rank the outcomes of things (based on probability) and we can see a band of different outcomes! You have more information in there. When you use KNN, we are just applying a label to a new datapoint.
    - **Efficiency and performance**  If you have tons of features, KNN is going to be SLOW. At times, it will even be totally useless as distance becomes meaningless in high dimensions. Logistic Regression are very, very fast.
* **Scaling your data**  Again, as we discussed in our review session, it's pretty much always a good idea.
* **Maximizing precision/recall/f1**  So, if you think about it, you would likely want to *maximize* recall. If you think about how weather reporters tell us about the weather, they would rather have more False Positives because they would rather tell you it is going to rain, snow, etc. and be wrong versus telling you it **won't** rain and being wrong. In this case, then, we would choose a model that maximizes our recall. How can we do that? Well:
    - Try different models, with different hyperparameters, features, or totally different all together, and pick the one that gives you the best recall (without losing too many False Positives).
    - With logistic regression, because we have probabilities, you can actually change a threshold for making the classification. Instead of making it a majority vote (probability > 0.5 in binary), you can cut it off at a higher threshold. If you make the cut-off to say it is going to rain (class 1) at probability 0.4, you are being more flexibile to saying "Hey, it may rain." This will lower your chance of making a False Negative prediction!
    - The last option is by weighting... You can actually give more weight to a certain class if it has more cost: https://stackoverflow.com/questions/30972029/how-does-the-class-weight-parameter-in-scikit-learn-work

**Any questions on this, let me know!**
