## Cleaning data for credit scoring. Creditworthiness analysis
### Task:
Clean a set of banking data and make assumptions about how different features impact the delinquency rate.

### Tools:
Python, Pandas, Numpy, Matplotlib

### Methods:
- Fixing data type
- Removing duplicates, wrong values
- Fixing structural errors
- Filling missing values with mean and median by categories
- Processing string values, grouping string values into categories 
- Converting continuous variables to categorical variables
- EDA  

### Data description:
The data contain the following information:
children — number of children
days_employed — total work experience in days
dob_years — age
education
education_id
family_status
family_status_id
gender
income_type
debt — (1 / 0)
total_income - monthly income
purpose — purpose for a loan

### Stages:
#### 1. Missing and wrong values processing
- children - we found wrong values(-1 and 20), changed to 1 and 20 respectively, assuming that there were misprints.
- days_employed - We found out that pensioners and the unemployed have positive values, while the others have negative ones. Work experience in those groups is shown in hours. We converted all values into years (years_employed) and filled missing values with median by income_type.
- dob_years. We changed zero values with mean by income_type.
- education, education_id - we converted string values into lower case and decreased the number of unique values to 5.
- family_status, family_status_id - we converted values into lower case.
- gender - we found a misprint and changed it to the most popular gender (F).
- total_income - we filled missing values with median by income_type.
- purpose - we found duplicates to deal with on the next stage.

#### 2. Categorization
- We grouped purpose, total_income, years_employed, and dob_years into categories. It seems to be a correlation between those variables and the delinquency rate.

#### 3. Answering questions
- Children increase the risk of delinquency (there is growth from 7 to 9% between 0 and 1 child). Among borrowers with children, the delinquency rate fluctuates. Families with 3 children are the most reliable borrowers (apart from child-free families).
- The highest risk of not paying off on time is among common-law partners and single borrowers. However, there could be an influence of age: married or divorced people are usually older than unmarried borrowers.
- There is a relationship between the delinquency rate and income: middle and upper-middle levels (120 000 - 160 000) show the highest delinquency rate, while the lowest risk is among high-income borrowers.
- The past-due rate is higher for auto and education loans, whereas mortgages and wedding loans show a lower rate of delinquency.

#### 4. Conclusion
- We can assume a relationship between the number of children and the delinquency rate, having children increases the risk of delinquency.
- Marital status also affects the delinquency rate. Unmarried borrowers have the highest risk, while widowed borrowers show the lowest risk. However, it could be influenced by age (unmarried clients are younger, whereas widowed borrowers are older).
- Income also affects the probability of paying off on time: middle and upper-middle levels show the highest delinquency rate, whereas the borrowers with high income are the most reliable ones.
- Loan purposes also affect the delinquency rate, marriage loans, and mortgages are paid off on time more frequently than education and auto loans.
