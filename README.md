# A-B-Testing-for-Globox-Company
A/B testing for a new banner on the Company's mobile website to investigate its effect on revenue and conversion rate.
## Project Overview
The Company introduced a new banner that highlights key products in the food and drink category at the top of the mobile website to see if it leads to increased revenue and conversion rate. A user visits the main page and is randomly assigned to either the control (does not see new banner) or treatment (sees new banner) groups. Users may or may not make purchase, making purchase is termed ‘conversion’. 
## Keynotes
1. Two metrics were measured in this experiment, conversion rate and average amount
spent per user.
2. The experiment ran for 13 days. 
3. Users were assigned randomly to two groups, group A(control) and B(treatment).
4. There was a total of 48,943 users, 24,343 in group A and 24,600 in group B.
5. 955 users made purchase in group A and 1,139 in group B.
6. The total amount spent by customers in group B was higher than group A with $1,269  The conversion rate in group B was higher than group A with 0.71%
## Tools
Postgresql - Used for data anlysis.  
Google spreadsheet - Used for hypothesis testing.  
Tableau - Used for data visualization.  
Microsoft Powerpoint - Used for report presentation, kindly see attached.  

## Data sources
1. Google spreadsheet( for the extracted table): https://docs.google.com/spreadsheets/d/1Q7qtdndJwJrzMmrkker17K1XQJRPFs-yMrqHFfi5tHA/edit?usp=drive_link
2. Please refer to the attached Microsoft Word document for the original Entity Relationship Diagram and Data Dictionary
## Data Analysis
SQL code to extract the user ID, country, gender, device type, test group, and whether or not they converted (spent > $0) and how much they spent in total ($0+).
```sql
SELECT 
    id,
    COALESCE(country, 'Unknown') AS Country,
    COALESCE(gender, 'Unknown') AS Gender,
    COALESCE(groups.device, 'Unknown') AS Device,
    "group",
    SUM(COALESCE(spent, 0)) AS Amount_spent,
    CASE 
        WHEN SUM(spent) > 0 THEN '1'
        ELSE '0' 
    END AS conversion
FROM
    users
LEFT JOIN 
    groups ON groups.uid = users.id
LEFT JOIN 
    activity ON users.id = activity.uid
GROUP BY
    id, groups.device, "group";
```

The data gotten from the above query was used for the following visualizations in tableau:

1. Compare the conversion rate and average amount spent between the test groups.
See here: https://public.tableau.com/views/Comparingtheconversionrateandaverageamountspentbetweenthetestgroups/Sheet1?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link
2. The distribution of the amount spent per user for each group.
See here: https://public.tableau.com/views/Thedistributionoftheamountspentperuserforeachgroup_/Sheet2?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link
3. The relationship between the test metrics (conversion rate and average amount spent) and the user’s device.
See here: https://public.tableau.com/views/Exploretherelationshipbetweenthetestmetricsconversionrateandaverageamountspentandtheusersdevice_/Sheet3?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link
4. The relationship between the test metrics (conversion rate and average amount spent) and the user’s gender.
See here: https://public.tableau.com/views/Exploretherelationshipbetweenthetestmetricsconversionrateandaverageamountspentandtheusersgender_/Sheet4?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link
5. The relationship between the test metrics (conversion rate and average amount spent) and the user’s country.
See here: https://public.tableau.com/views/Visualizationstoexploretherelationshipbetweenthetestmetricsconversionrateandaverageamountspentandtheuserscountry/Sheet5?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link

**Two Hypothesis tests** were further carried out to determine whether there is a statistically significant difference between the two groups and rule out the possibility that the above listed results were due to chance. For the difference in means (average amount spent per user), a two-tailed T-test with a 95% confidence level and 0.05 as threshold for statistical significance was conducted. For the difference in proportions (conversion rate), a two-tailed Z-test with a 95% confidence level and 0.05 as threshold for statistical significance was conducted.
**Link to hypothesis testing:** https://docs.google.com/spreadsheets/d/1Q7qtdndJwJrzMmrkker17K1XQJRPFs-yMrqHFfi5tHA/edit?usp=drive_link  

**A power analysis** was also carried out to determine whether the total number of users (sample size) in the experiment was adequate to detect meaningful effects. The purpose of this analysis was to determine not only the statistical significance of the difference between the two groups but also how meaningful and practical it is in the real world. We wanted to check if our study had adequate number of users to confidently spot a difference between the two groups. We considered a difference of 10%, this is called the effect size, which is simply the difference we're looking for between Group A and Group B and it represents the smallest change or improvement we want our study to be able to detect. A Power of 80% was used, this is the probability that the study will correctly detect a true effect if it exists. 
 
  **Link to sample size calculator used for the power analysis:**  
**Conversion rate:** https://www.statsig.com/calculator?mde=10&bcr=3.92&twoSided=true&splitRatio=0.5&alpha=0.05&power=0.8  
**Average amount spent per user:** https://www.gigacalculator.com/calculators/power-sample-size-calculator.php  
calcType=ss&eType=groups&type=cont&sType=cont&hyp=sup&diffType=abs&alpha=0.05&power=0.8&groups=1&ratio=1&inputType=prop&ssize=&prop=&mean=3.375&stdev=25.936&sinputType=prop&effect=0.3375&margin=0  

## RESULTS  

## Hypothesis Tests
**Conversion rate:**
The p-value obtained from our analysis is **0.0001**, which is much smaller than the significance level of 0.05. This low p-value indicates that the observed difference in conversion rates between the two groups is highly unlikely to be due to random chance alone. Therefore, we can confidently say that there is a statistically significant difference in conversion rates between the two groups.  

**Average amount spent per user:**
The p-value we obtained from this analysis is **0.944**, which is much larger than the significance level of 0.05. This high p-value suggests that the observed difference in the average amount spent per user between the two groups could likely be due to random chance. Consequently, we cannot confidently say there is a significant difference in the spending behaviour between the two groups.  

## Power Analysis  

For a difference/effect size of 10% and Power of 80%, we will require:  

**Conversion rate:** A sample size of **70,000**  

**Average Amount spent per user:** A sample size of **146, 046**  

This means we cannot confidently say that we have an 80% chance of detecting a 10% difference between the 2 groups with our current sample size of **48,943.**  

## Recommendations  

Our recommendation is that the banner should be launched. This is because of the following reasons:

1. One of the metrics (conversion rate) showed a statistically significant increase in the
treatment group.
2. The cost required to launch the banner is not expensive.
   
We believe this approach strikes a balance between statistical rigor and the need for practical, impactful decision-making.






