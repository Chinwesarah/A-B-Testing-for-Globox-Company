# A-B-Testing-for-Globox-Company
A/B testing for a new banner on the Company's mobile website to investigate its effect on revenue and conversion rate.
## Project Overview
The Company introduced a new banner that highlights key products in the food and drink category at the top of the mobile website to see if it leads to increased revenue and conversion rate. A user visits the main page and is randomly assigned to either the control (does not see new banner) or treatment (sees new banner) groups. Users may or may not make purchase, making purchase is termed ‘conversion’. The experiment ran for 13 days
## Tools
Postgresql - Used for data anlysis
Google spreadsheet - Used for hypothesis testing
Tableau - Used for data visualization
## Data sources
Please refer to the attached Microsoft Word document for the Entity Relationship Diagram and Data Dictionary
## Data Analysis
1. Two metrics were measured in this experiment, conversion rate and average amount
spent per user.
2. Users were assigned randomly to two groups, group A(control) and B(treatment).
3. There was a total of 48,943 users, 24,343 in group A and 24,600 in group B.
4. 955 users made purchase in group A and 1,139 in group B.
5. The total amount spent by customers in group B was higher than group A with $1,269  The conversion rate in group B was higher than group A with 0.71%
6. **A power analysis** was also carried out to determine whether the total number of users (sample size) in the experiment was adequate to detect meaningful effects. The purpose of this analysis was to determine not only the statistical significance of the difference between the two groups but also how meaningful and practical it is in the real world. We wanted to check if our study had adequate number of users to confidently spot a difference between the two groups. We considered a difference of 10%, this is called the effect size, which is simply the difference we're looking for between Group A and Group B and it represents the smallest change or improvement we want our study to be able to detect. A Power of 80% was used, this is the probability that the study will correctly detect a true effect if it exists.  
     **Link to sample size calculator used for the power analysis:**

     **Conversion rate:** https://www.statsig.com/calculator?mde=10&bcr=3.92&twoSided=true&splitRatio=0.5&alpha=0.05&power=0.8  

     **Average amount spent per user:** https://www.gigacalculator.com/calculators/power-sample-size-calculator.php  
     calcType=ss&eType=groups&type=cont&sType=cont&hyp=sup&diffType=abs&alpha=0.05&power=0.8&groups=1&ratio=1&inputType=prop&ssize=&prop=&mean=3.375&stdev=25.936&sinputType=prop&effect=0.3375&margin=0

8.  **Two Hypothesis tests** were further carried out to determine whether there is a statistically significant difference between the two groups and rule out the possibility that the above listed results were due to chance. For the difference in means (average amount spent per user), a two-tailed T-test with a 95% confidence level and 0.05 as threshold for statistical significance was conducted. For the difference in proportions (conversion rate), a two-tailed Z-test with a 95% confidence level and 0.05 as threshold for statistical significance was conducted.
**Link to hypothesis testing:** https://docs.google.com/spreadsheets/d/1Q7qtdndJwJrzMmrkker17K1XQJRPFs-yMrqHFfi5tHA/edit?usp=drive_link





