&emsp; &emsp; &emsp; &emsp; [![logo](https://github.com/petrarkaselin/mid_project/blob/main/slides/Slide%2016_9%20-%201%20start.jpg)](https://github.com/petrarkaselin/mid_project/blob/main/slides/Slide%2016_9%20-%201%20start.jpg)
# Exploring a Movie Database
### Team:
##### &emsp;   Francisco Caupers
##### &emsp;   Imrane Mourigh
##### &emsp;   Tatyana Tarasova
#### 
### Objects
- What?  &rarr; Films
- When?  &rarr; 2019-2023
- Where? &rarr; USA
- How?   &rarr; IMDB, Oscars

As the main database for our analysis we chose the IMDB database. The whole database contains all the films starting from 1927. The initial file is more than 400 MB, so we decided to filter it by choosing time period from 2019 till 2023 and by main production country USA. At this point we had a bit more than 30 000 lines. 

### Questions
1. What factors contribute to the box office success of films in the USA between 2019-2023?
2. Which film genres are most popular among audiences during this period?
3. How are film budgets distributed across different genres and production companies?
4. Do ratings impact revenue?
5. Are production companies nominated for the Academy Awards (in or case the Oscars) consistently associated with high-performing film?

### Hypotheses
1. H0: There is no relationship between film that was nominated for Oscar and its genre.
2. H0: There is no relationship between genres and ratings of the film.

For the purpose of our analysis we filtered our main table. We took only those films that have information about revenue (revenue > 0) and show interest from the audience (vote count > 100). 

[![filtering](https://github.com/petrarkaselin/mid_project/blob/main/slides/Slide%2016_9%20-%205%20filtering.jpg)](https://github.com/petrarkaselin/mid_project/blob/main/slides/Slide%2016_9%20-%205%20filtering.jpg)

As additional data sets we used information about age ratings, Oscar nominated film and Oscar nominated companies in 2022. We join all related information from these tables to the main table and merged them all in one. At this point we had 642 lines.

[![merging](https://github.com/petrarkaselin/mid_project/blob/main/slides/Slide%2016_9%20-%206%20merged%20data.jpg)](https://github.com/petrarkaselin/mid_project/blob/main/slides/Slide%2016_9%20-%206%20merged%20data.jpg)

### Data cleaning measures:
- Changed column 'release_data' to 'date' datatype
- Manually added one missing value in 'production_companies' and two missing values in 'spoken_languages' from www.imdb.com

For some questions we also performed some filtering and cleaning:
- In columns 'production_companies' and 'genres' we took only the main company and deleted the rest. As Oscar nominations and ratings consider only the leading company and genre.
- We kept only necessary columns for each question and saved filtered data frames for each question.
- Calculated revenue and budget in millions and used them for calculations
- for Question 5 in column 'license' we filled NaN values with 'unknown'
- for questions and hypotheses where we analyzed rating, we didn't use rows with value 'unknown' in 'license'

For **Question_1** we created a data frame 'numerical_columns' and checked correlation between numerical variables by calculating the correlation matrix. We observed 3 correlated columns **'vote_count'** and **'budget'** with correlation coefficient 0,63, **'vote_count'** and **'revenue'** 0,74, **'revenue'** and **'budget'**. We calculated VIF for each column and got following results:
1.  vote_count  2.993886
2.   budget_M  2.793599
3.  revenue_M  3.091482

**All three of them were less than 4, which indicated absence of multicollinearity, so we plotted a scatter plots for each correlation.**

For **Question_2** we compared distribution of number of films and their revenues by genres. We plotted two bar charts and observed that **the most popular genres are Action (with highest total revenue), Adventure, Animation(with highest average vote), Science fiction and Comedy.**

In **Question_3** we made a data frame to define Top 15 production companies. We used 'groupby' by production companies and chose 'sum' as aggregation function. Ordering them in descending order, we could highlight Top 15 companies. We used this list to assign rest of the companies as 'other' to make a visualization. We drew two pie charts, one to compare Top 15 with Other companies and the other one to compare them among themselves. The companies with the biggest budget are **Walt Disney, Marvel Studios, Warner Bros. Pictures and Universal Pictures.** 

In **Question_4** we took the film that have information about ratings (we didn't take rows with value of rating 'unknown'). **On the graph we can easily see that film with rating PG-13 has much higher total value across different genres.**

To answer **Question_5** we used boolean column 'company_nominated' with values 0 and 1. And also filtered the data set by release year. We took only film from year 2022, as we previously said, that we took information about company nominee only for year 2022. We compared to bar plots with average and total revenue. In both cases we can see that Oscar nominated companies have higher revenue comparing to not nominated companies. **We assume that a nomination for Oscar Award increases prestige of the company and consequently increases audience interest to these companies films.** 

##### Hypotheses
For both hypotheses me made contingency tables and performed Chi^2^ test. 
- Results for Hypothesis 1:
&emsp;Chi-Square Statistic: 76.15
&emsp;P-value: 0.0
&emsp;Degrees of Freedom: 17
- Results for Hypothesis 1:
&emsp;Chi-Square Statistic: 187.36
&emsp;P-value: 0.0
&emsp;Degrees of Freedom: 68

Fot both Hypotheses the Chi-Square Statistic is relatively large, indicating a significant difference between the observed and expected frequencies. The extremely small p-value ~0 is well below the typical significance level of 0.05. This suggests strong evidence against the null hypothesis of no association between the two categorical variables. **Which means that Oscar nominated film correlates with its genre. And film genre correlates with its rating.**

For **Hypothesis_1** we made two tree maps where we can see that the highest number of films among Oscar nominated films is **Drama**, at the same time the lead genre in film that weren't nominated for Oscar is **Action**.

For **Hypothesis_2** we made a bar chart where we can see that **rating PG-13 have mostly Action, Science Fiction and Animation genres. In rating R there are more Horror films.**

In delving into a movie database, we set our sights on films in the USA from 2019 to 2023, drawing from the extensive IMDB and Oscar datasets. After narrowing down our selection to include only films with revenue and substantial audience interest, we integrated additional datasets, resulting in a dataset of 642 films. Our data-cleaning efforts involved adjusting data types, making manual additions, and focusing on key columns. A closer look at correlations revealed intriguing connections between revenue, budget, and audience vote counts. Genres like Action, Adventure, Animation, Science Fiction, and Comedy emerged as the audience favorites. We also identified top production companies, with giants like Walt Disney and Marvel Studios leading the pack. Analyzing film ratings, we observed higher revenue for films with a PG-13 rating. Hypothesis testing further strengthened our understanding of the relationships between Oscar nominations, film genres, and ratings. Visualizations, including treemaps and bar charts, provided a vivid representation of genre distributions. In essence, our analysis uncovered valuable insights into the dynamics of film success, genre preferences, and the impact of prestigious awards on both production companies and individual film performances.