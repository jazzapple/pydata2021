# Keeping sensitive data safe with Recommendation Systems
* DS at Paypal, Approach is Google Patented: https://patents.google.com/patent/US20210073409A1/en?oq=US20210073409
* https://implicit.readthedocs.io/en/latest/

## Problem: improve control of sensitive data by detecting unauthorised access to database tables
* authorised access
* avoid potential security incidents

## Solution: Recommender systems for detecting anomaly detection
* Types of Feedback: explicit (direct from user, review), implicit (user and item iteractions - page views, purchases, clicks, likes)
* Implicit feedback is noisy
* Collaborative Filtering Techniques
    * Matrix factorization - find latent factor embeddings (items, user) which dot product generates predicted rating for all users. Not well suited for implicit feedback due to missing value unknown meaning
    * Implicit feedback Algorithm: better accounts for missing values (where user has not "interacted" he product)
        * introduce Confidence Weight - strength of use preference, or confidence in observing preference
        * optimising cost function is expensive, so use **Alternet Least Squares cost function** - alternate between re-computing user factors and item factors. Python implementation: `pip install implicit` library

## Anomalies in Database access
* Users "consume" Tables
* Tables = Items
* High (low) volume queries >> High (low) confidence
* Lower number of interactions >> lower confidence
* Anomalies - unexpected table access

## Recommendation systems in detecting anomalies
* usually, looking for item user is thought to like
* now, we look for items user is "not supposed" to like - opposite direction
* Building the model:
    * Access to tables matrix  - amount of queries made
    * Parameters: regularisation factor, ALS iterations, latent factors, scaling factor
* Multiple access to same table by same user with same query on same day counted only once
* Experiments
    1. Assumption: Users with high usage (known preference) should get high scores. For Test set, filter for users who accessed a table at least 10 times - i.e. known preference. Confirmed test scores are high (~1), due to known preference. 
    2. Assumption: Users in same team use same group of tables. Simulate suspicious access by randomly choosing 2 unseen tables for random user (accessed by team, not accessed by team). KDE showed clear separation in PDF between same team and not same team, with mode ~1 and ~0 respectively. AUC ~0.90

## Alternative use cases
* Granting user access
* Clustering scores by tables accessed, to prompt collaboration
* Other fraud detection alerts    