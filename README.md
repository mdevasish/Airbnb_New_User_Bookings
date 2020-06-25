# Airbnb_New_User_Bookings
Kaggle Recruitment Contest

Problem Statement:

New users on Airbnb can book a place to stay in 34,000+ cities across 190+ countries. By accurately predicting where a new user will book their first travel experience, Airbnb can share more personalized content with their community, decrease the average time to first booking, and better forecast demand.

In this recruiting competition, Airbnb challenges you to predict in which country a new user will make his or her first booking. Kagglers who impress with their answer (and an explanation of how they got there) will be considered for an interview for the opportunity to join Airbnb's Data Science and Analytics team.

Evaluation Metrics:

As per the competition,for each user we predict 5 country destinations with decreasing order of probabilities. The evaluation metric is designed based on the rank of the prediction with respect to the target. If the top prediction of the 5 countries match the target we achieve high score(in this case 1) and subsequently the score decreases if the target matches with second ranked destination the score achieved would be lower.

The evaluation metric for this competition is NDCG (Normalized discounted cumulative gain) @k where k=5. NDCG is calculated as:

<img src="https://render.githubusercontent.com/render/math?math=DCG = \sum_{i=1}^{k} (2^r - 1)/(log_2 (i%2B1))">,

<img src="https://render.githubusercontent.com/render/math?math=nDCG_k = DCG_k/IDCG_k">,

where r is the relevance of the result at position i. And IDCGk is the maximum possible (ideal) DCG for a given set of queries. All NDCG calculations are relative values on the interval 0.0 to 1.0.

For each new user, you are to make a maximum of 5 predictions on the country of the first booking. The ground truth country is marked with relevance = 1, while the rest have relevance = 0.

For example, if for a particular user the destination is FR, then the predictions become:

[FR]  gives a score <img src="https://render.githubusercontent.com/render/math?math=NDCG = (2^1 - 1)/(log_2 (1%2B1)) = 1">

[US,FR] gives a score <img src="https://render.githubusercontent.com/render/math?math=DCG = ((2^0 - 1)/(log_2 (1%2B1)) %2B (2^1 - 1)/(log_2 (2%2B1)) = 0.6309 ">

Data accessible at : https://drive.google.com/drive/folders/144LKYOmOlcuKli82W8qoNqbOTeDQ7jCN?usp=sharing

Approach:

Firstly the data related to click stream (sessions.csv) contained lot of null values. The clcik stream data capture the web elements each user has clicked upon and the time spent on each page. The diversity in the webelements columns was huge. The task to consolidate the webelements into various buckets based on the user activity was a exhaustive task and has consumed the maximum time. Next the data related to the user demographics have lot of inconsistent values and null values. The user profile data had to be sanitized based on datetime features. Despite the higher missing values percentages in the user demographics we have retained the features by imputing certain columns because the outcome of the problem statement is hugely dependent on the user demographics. Also we have use Levenstein distances framework into the implementation to create a proximity score based on the mother toungue of the user the Language of the destination as a feature. Our approach was based on few hypotheses and they are:

•	Age might be a major predictor because
  o	Older people have more savings and time, meaning they can afford to travel to expensive places
  o	Younger people are more adventurous. So, they might be open to trying offbeat countries, but can probably only afford cheaper ones
  o	The more the proportion of people of their own age in the destination country, more the suitability of the activities/tourist attractions to the user
  o	Older people might prefer going to countries where it is easy to get by, maybe due to similarity of languages. Younger ones might be more open to countries with alien languages.
 
•	Financial affluence of the person
  o	No direct indicator present in the data. Therefore, it wasn’t possible to do any form of user-level feature cross using user’s financial status and the cost of living of the destination country.
  o	Instead, we tried to derive implicit features, like number of unique devices the person owns, the number of apple products and number of tablets (the more they own, the higher the probability of them being affluent)
•	Seasonality
•	Latent information contained in browsing patterns
  o	There was no information in sessions data regarding which country the user browsed for. So, action-wise time elapsed and frequencies were used to determine if they implicitly captured any hidden pattern connected to the first travel destination.

Challenges :
•	Unacceptable amount of Missing data in few prominent features.
•	Heavily imbalanced dataset. 
•	Leveraging the data collectively from all datasets to create a final table of meaningful features was a herculean task.
•	There was no information regarding the content the user browsed for.
•	Additional features like cost of living of destination country couldn’t be combined with this data since user-level financial information or other pertinent details were not provided, thereby preventing meaningful feature crosses.
•	Custom generation of NDCG scorer and memory handling was a challenge too.
