# Race Exploratory_analysis

## Table of Content
- [Project Overview](#project-overview)
- [Data Cleaning/Preparation](#data-cleaning/preparation)
- [Exploratory Analysis](#exploratory-analysis)
- [Data Analysis](#data-analysis)
- [Findings](#findings)
- [Recommendation](#recommendation)
- [References](#reference)

### Project Overview 
---

I conducted an exploratory data analysis on races conducted in the USA in 2020, ages of the athletes, performances and the impact of seasons on their performance.

![Gender distribution](https://github.com/CRYP-19/Exploratory_analysis/assets/78747034/76ba9b45-c4fd-4f52-8d10-55d75760c907)

### Data Source
---
Data was obtained from https://www.kaggle.com/datasets/aiaiaidavid/the-big-dataset-of-ultra-marathon-running/discussion/420633
## Tool
Python [Download here](https://www.python.org/downloads/)
### Data cleaning/preparation
---
1. Filtering the data for only USA races
2. Removed the blank spaces
3. Renamed each column
4. Removed duplicates
5. Sort by 50km and 50mi

### Exploratory Analysis
---

1. Find two races a single athlete ran in 2020
2. race_day
3. race_name
4. race_length
5. race_number_of_finishers
6. athlete_id
7. athlete_gender
8. athlete_age
9. athlete_performance
10. athlete_average_speed
11. Data analysis
12. Difference in speed for the 50k, 50mi male to female male
13. what age groups are the worst in the 50m race (20 + races min) (show 20)
14. #Seasons for the data -> slower in the summer than winter?
15. spring 3-5
16. summer 6-8
17. fall 12-2


![Athlete_age_speed_distribution](https://github.com/CRYP-19/Exploratory_analysis/assets/78747034/58e8cebd-90ff-429e-a163-a41c823f3c19)

### Data Analysis
---

```Python
import pandas as pd
import seaborn as sns
df3[df3['athlete_id'] == 222509]
sns.histplot(df3, x = 'race_length', hue = 'athlete_gender')
sns.violinplot(data = df3, x = 'race_length', y = 'athlete_average_speed', hue = 'athlete_gender', split = True, inner = 'quart', inlinewith = 1)
df3.groupby(['race_length', 'athlete_gender'])['athlete_average_speed'].mean()
df3.query('race_length == "50mi"').groupby('athlete_age')['athlete_average_speed'].agg(['mean','count']).sort_values('mean',ascending = False).query('count>19').head(15)
df3.query('race_length == "50mi"').groupby('athlete_age')['athlete_average_speed'].agg(['mean','count']).sort_values('mean',ascending = True).query('count>9').head(20)
df3['race_month'] = df3['race_day'].str.split('.').str.get(1).astype(int)
df3['race_season'] = df3['race_month'].apply(lambda x: 'Winter' if x > 11 else 'Fall' if x > 8 else 'Summer' if x > 5 else 'Spring' if x > 2 else 'Winter')
df3.groupby('race_season')['athlete_average_speed'].agg(['mean','count']).sort_values('mean', ascending = False)
df3.query('race_length == "50mi"').groupby('race_season')['athlete_average_speed'].agg(['mean','count']).sort_values('mean', ascending = False)
```
### Findings
---

The results shows as follows:
1. Athlete with ID 222509 age 23 ran two races in the US, a 50km and 50mi race at a top speed of 10.4mph for the 50km race and 8.7mph at the 50mi race
2. Over 20,000 people ran the 50km race while less than 6000 ran the 50mi race
3. Across the 50km race the gender distribution was almost the same while for the 50mi race, more male took part in the race.
4. Data also showed that the average speed of female in the 50km race is 7.1mph while for male is 7.7mph a difference of .6mph, while for the 50mi race female had 6.8mph, male had 7.3mph, a difference of .4mph
5. I also checked to see the impact of seasons on athletes speed and the data showed
Spring	7.7mph
Winter	7.5mph
Fall	7.4mph
Summer	6.9mph
This means athletes run faster in spring

### Recommendation
---

1. For races in the summer athletes should do their training in Africa where temperature is quite high
2. Athletes training should be by 50miles in order to be ready for both 50km and 50mi races
3. Sponsors should that are interested in building a brand around a race athlete should go for athletes between the ages of 20 to 28 years because that is when they hit their top speed

### Reference
---
- Ryan Nolan (https://www.youtube.com/watch?v=4sZFkPw87ng)
- Raw datasets (https://www.kaggle.com/datasets/aiaiaidavid/the-big-dataset-of-ultra-marathon-running/discussion/420633)
  
🤓
