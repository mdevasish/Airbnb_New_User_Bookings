# Airbnb_New_User_Bookings
Kaggle Recruitment Contest

Problem Statement:

New users on Airbnb can book a place to stay in 34,000+ cities across 190+ countries. By accurately predicting where a new user will book their first travel experience, Airbnb can share more personalized content with their community, decrease the average time to first booking, and better forecast demand.

In this recruiting competition, Airbnb challenges you to predict in which country a new user will make his or her first booking. Kagglers who impress with their answer (and an explanation of how they got there) will be considered for an interview for the opportunity to join Airbnb's Data Science and Analytics team.

Evaluation Metrics:

As per the competition,for each user we predict 5 country destinations with decreasing order of probabilities. The evaluation metric is designed based on the rank of the prediction with respect to the target. If the top prediction of the 5 countries match the target we achieve high score(in this case 1) and subsequently the score decreases if the target matches with second ranked destination the score achieved would be lower.

The evaluation metric for this competition is NDCG (Normalized discounted cumulative gain) @k where k=5. NDCG is calculated as:

$$DCG_{k}$$ = ∑i=1 to k 2^reli−1/log_2 (i+1),

nDCG_k = DCG_k/IDCG_k,

where reli is the relevance of the result at position i.

IDCGk is the maximum possible (ideal) DCG for a given set of queries. All NDCG calculations are relative values on the interval 0.0 to 1.0.

For each new user, you are to make a maximum of 5 predictions on the country of the first booking. The ground truth country is marked with relevance = 1, while the rest have relevance = 0.

For example, if for a particular user the destination is FR, then the predictions become:

[FR]  gives a NDCG=2^1−1log2(1+1)=1.0
[US,FR] gives a DCG=20−1log2(1+1)+21−1log2(2+1)=11.58496=0.6309 

$$\sum_{i=1}^n X_i$$
