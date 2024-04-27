# World Cup Matches Data Cleansing
The dataset comprises information about FIFA World Cup matches, containing details such as the year of the tournament, date and time of the match, stage of the tournament, stadium and city where the match took place, home and away team names, goals scored by each team, attendance, halftime scores, referee details, round ID, match ID, and initials of the home and away teams.

This dataset serves as the basis for analyzing FIFA World Cup matches, allowing for insights into various aspects of the tournament, such as team performances, match outcomes, and attendance trends. Before conducting any analysis, it's essential to perform data cleaning and preprocessing to ensure the dataset's quality and integrity.

## Python Libraries Import


## Load Data Set

Display the data set that has been loaded


## Data Cleansing
Data cleansing is the process of identifying and correcting errors, inconsistencies, and inaccuracies in a dataset to improve its quality and reliability for analysis. It involves various tasks aimed at ensuring that the data is accurate, complete, and consistent.
### Check Data Condition


From the description, we can see that some columns have fewer non-null values than the total entries, indicating the presence of null or empty values in the DataFrame. Additionally, we can also observe the data types of each column, where there are columns whose data types are not yet appropriate.
## Check and remove duplicate rows from theData Frame
### keep
- {‘first’, ‘last’, False}, default ‘first’
- Determines which duplicates (if any) to mark.
- first : Mark duplicates as True except for the first occurrence.
- last : Mark duplicates as True except for the last occurrence.
- False : Mark all duplicates as True.

Due to the presence of numerous NaN values, our first step will be to drop rows containing NaN values.

Once we have confirmed that the duplicated data is indeed redundant, we can proceed to delete the duplicates.


## Convert Dtype
"Convert Dtype" refers to the process of converting the data type of a column in a dataset. This process is often necessary to ensure that the data is in the appropriate format for analysis or visualization.

For example, if a column contains numerical data but is stored as a string, it may be necessary to convert it to a numerical data type (e.g., int or float) to perform mathematical operations or statistical analysis.

Similarly, if a column contains dates or times but is stored as a string or integer, it may be necessary to convert it to a datetime data type to perform date-based analysis or visualization.

In summary, converting data types ensures that the data is in the correct format for analysis and allows for more efficient and accurate data processing.
### Year 


### Datetime


### Home Team Goals, Away Team Goals, Attendance, Half-time Home Goals, Half-time Away Goals, RoundID, MatchID


## Check Percentage Missing Values
"Check Percentage Missing Values" refers to the process of calculating and determining the percentage of missing values in each column of a dataset. This step is essential in data preprocessing and quality assurance, as missing values can impact the accuracy and reliability of analytical results.

To perform this task, the dataset is inspected column by column, and the number of missing values in each column is counted. Then, the percentage of missing values is calculated by dividing the number of missing values by the total number of observations in the dataset and multiplying by 100.

Understanding the percentage of missing values in each column helps data analysts or scientists develop appropriate strategies for handling missing data. Depending on the nature of the missing values and their impact on the analysis, strategies such as imputation (replacing missing values with estimated ones), deletion of rows or columns with missing values, or specialized modeling techniques may be employed to address missing data issues effectively.

In summary, checking the percentage of missing values provides valuable insights into the data quality and guides decision-making regarding data preprocessing and analysis strategies.

It turns out that only the 'Datetime' column has missing values. Although the number of missing values is not significant, considering that 'Datetime' is a crucial column for analysis, we have decided to retain the missing values in the 'Datetime' column.


#### Insights and Considerations
- All columns have missing values, with 'Attendance' having the highest number of missing values, totaling 3722.
- Assuming we want to analyze "team performance in matches," some unimportant columns can be dropped.
##### Extremely Important Columns
- Year: The year of the match.
- Home Team Name: The name of the home team.
- Away Team Name: The name of the away team.
- Home Team Goals: The score of the match and the performance of the home team in scoring goals.
- Away Team Goals: The score of the match and the performance of the away team in scoring goals.
- Attendance: The number of spectators in the match.
- Datetime: The date and time of the match. (to be manipulated later)
##### Possibly Important Columns
- Half-time Home Goals: The number of goals scored by the home team in the first half.
- Half-time Away Goals: The number of goals scored by the away team in the first half.
- City: The city where the match took place.
- Stadium: The name of the stadium where the match took place.
- Stage: The stage or phase of the tournament.
- RoundID: The ID of the tournament round.
- MatchID: The ID of the match.
- Win conditions: The conditions for winning the match.
##### Unimportant Columns
- Referee: The name of the match referee.
- Assistant 1: The name of the first assistant referee.
- Assistant 2: The name of the second assistant referee.
- Home Team Initials: The initials of the home team.
- Away Team Initials: The initials of the away team.

## Data Manipulation
Data manipulation involves making changes to the dataset to prepare it for analysis or to extract valuable insights. This process includes tasks such as cleaning the data, transforming its structure, creating new features, and aggregating information.
### Drop Non-Essential Columns
This step involves removing columns from the dataset that are deemed non-essential for the analysis. Non-essential columns are those that do not contribute significantly to the analysis or do not align with the research objectives. By dropping these columns, we can streamline the dataset and focus only on the most relevant features.


We drop columns such as 'Referee', 'Assistant 1', 'Assistant 2', 'Home Team Initials', and 'Away Team Initials' as they are not critical for the analysis at hand.

Show dataset info to see if the date and country columns are missing.


### Make Column Draw, Date, and Time
We will perform data manipulation here. Manipulation here does not involve altering data values but rather restructuring the data to make it easier for machines to read.
To determine whether a match ended in a draw or not, we can use the "Home Team Goals" and "Away Team Goals" columns.


Split Datetime into 'Date' and 'Time'


## Visualization
### Home Team Goals vs Away Team Goals 
Analyze the relationship between the number of goals scored by the home team and the number of goals scored by the away team.

Using value_counts() to count how many times each value of home team goals appears in the data, only in matches where the away team scored a goal.


### Win Conditions vs Home Team Goals
Looking at how victory conditions are based on home team goals
<div align="center"><img src="https://github.com/Shabiyyahzlf/Data-Visualization-1/assets/89763971/d70a3821-2e78-4f2f-9fd4-bc4b23edd906" /></div>
There are 48 entries in the DataFrame that have 5 or more goals scored by the home team but do not have any information in the 'win conditions' column.


### Number of Matches by Year
- The groupby() function is used to group the rows of data based on the same value in the column used as the grouping criterion, in this case, the 'Year' column.
- The size() method counts the number of rows in each group. In this context, each year group will have the same number of rows as the number of matches in that year.


### Year vs Draw
Count of matches that ended in a draw for matches from the year 2000 onwards.


## Pivot
Pivoting is a process used to reorganize and reshape data, typically for the purpose of analysis or visualization. In pandas, the `pivot_table()` function is commonly used to create a spreadsheet-style pivot table as a DataFrame. This function allows us to specify the index, columns, and values to aggregate, providing flexibility in how the data is arranged.

By pivoting data, we can transform rows into columns and vice versa, aggregating values based on specified criteria. This can help in summarizing and analyzing data in a more structured and intuitive format, facilitating further exploration and interpretation.
### Make_pivot
The `make_pivot` function is a custom utility developed to pivot the data in our dataset. Pivoting is a technique used to reshape data from long to wide format, making it easier to analyze and visualize. This function takes certain parameters such as index, columns, and aggregation functions to create a pivot table from the original dataset.


After observing the bar chart, it seems that visualizing Year vs Draw would be more appropriate using a line graph.


### Slice_pivot
The `slice_pivot` variable is a pivot table generated from a sliced portion of the original dataset. This pivot table provides insights into specific aspects of the data by grouping and aggregating values based on specified index and column criteria.
#### Description:
- `Purpose`: To analyze a subset of the dataset and visualize relationships between different variables.
- `Generated From`: The df_slice DataFrame, which is a subset of the original dataset containing selected columns.
- `Parameters`: The pivot table is created using the pivot_table function, with parameters specifying index, columns, and aggregation functions.

#### How many `Draws` based on the `Year`


#### How many `Draws` occur in each stage of the matches based on the `Year`


## Groupby
The `groupby` operation in pandas is a powerful tool for splitting the data into groups based on some criteria, applying a function to each group independently, and then combining the results into a DataFrame or other data structure.
>

## Crosstab
The `crosstab` function in pandas is used to compute a cross-tabulation of two or more factors, also known as contingency tables. It computes a simple cross-tabulation of two (or more) factors, which can be either categorical or discrete variables.

By default, it calculates the frequency.


## Get Dummies
The `get_dummies` function in pandas is used to convert categorical variables into dummy/indicator variables, also known as one-hot encoding. It creates a new DataFrame with binary indicator variables for each category present in the original categorical variable.


## Sort
Sorting data in pandas allows you to rearrange the rows of a DataFrame or Series based on the values of one or more columns. The `sort_values` method is commonly used for this purpose.


## Rename
Renaming columns in pandas allows you to change the names of one or more columns in a DataFrame to make them more descriptive or suitable for analysis. The `rename` method is commonly used for this purpose.


## Concat
Concatenating DataFrames in pandas involves combining multiple DataFrames along rows or columns. The `concat` function is used for this purpose.



## Merge
Merging DataFrames in pandas involves combining data from different sources based on common columns or indices. The `merge` function is used for this purpose.


