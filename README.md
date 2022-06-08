# Lending Club Case Study
To be able to identify risky loan applicants, such loans can be reduced thereby reducing the risk of loss.<br />
The aim is to identify patterns which indicate if a person is likely to default, which may be used for taking actions such as <br /><br />
	-Denying the loan<br />
	-Reducing the amount of loan,<br />
	-Lending (to risky applicants) at a higher interest rate, etc.<br />


## Table of Contents<br />
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)

<!-- You can include any other section that is pertinent to your problem -->

## General Information<br />
### Data Handling and Cleaning:<br />
No missing values or incorrect data types before we proceed to the analysis stage: <br /><br />
**Column wise:**<br />
• All null value column has been removed.<br />
• Dropped the columns which has customer behavior and will not be available for new customers. There is no point of analyzing those column where data will not be available for new customers<br />
• Dropped the columns, if all values on column is same.<br />
• Dropped column which has NA and 0 which will not be useful for analysis<br />
• Removed desc column as NLP is not part of this project.<br />
• Removed url column<br /><br />
**Correcting Incorrect Data Types:**<br />
• Removed months string from terms<br />
• Removed % from int rates<br />
• Removed all special char from emp_length<br />
• Replace verification_status "source verified" value with verified<br /><br />
**Imputing Missing Values:**<br />
• Replacing emp length NA or empty with 0 value<br />
• Replace home_ownership None value with Others<br /><br />
**Row wise:**<br />
• Dropped current loan status as this is will not add value. Interested on 
charged off and fully paid loans.<br />
• Checked id and member Id are unique. There is no duplicate rows because 
id and member_id rows as same as no of rows.<br />
• Checked the no of rows which has missing NA or null. There are no empty 
rows in dataset.<br /><br />
**Sanity Checks:**<br />
• All numeric data should be positive. Confirmed all are positive integers<br /><br />
**Derived Column:**<br />
• Extracted month and year from issue_d. <br /><br />
**Outliers Removal:**<br />
• All numeric data has been distributed well except annual_inc. So removing outlier on annual_inc. Data kept till 98 percentile<br /><br />

## Conclusions
### Analysis Approach – Univariate Analysis<br />
• Distribution of loan_amnt , funded_amnt and funded_amnt_inv looks similar.<br /><br />
**Continuous data observation:**<br />
• Most of the Loan amounts are between 5000 15000<br />
• Most of the funded amount are between 5000 15000<br />
• Most of the interest rates between 8 to 14%<br />
• Most of the installments are between 200 400<br />
• Most of the DTI are between 1218<br />
• Most of the Annual income is in the range of 30,000 and 60,000<br /><br />

**Categorical data observation:** <br />
• 76% of loans are 36 months term and 24% loans are 60 months term<br />
• Loan applicants contribution are Grade A (30%), Grade B(26%), Grade C (20%)<br /> 
• 22% of employees are 10+ years and 20% employees are 1 year.<br />
• 49% of loan applicants has rented home and 43% is mortgage<br />
• 56% of source has been verified and 44% is not verified<br />
• 85% of loan is fullu paid and 15% of loan is charged off.<br />
• 47% of purpose is dept consolidation and 13% is for credit card<br />
• Given data set, 53% of loan provided on year 2011 and 30% of loan provided on 2010<br />
• No of load applied is slightly high on Oct, Nov and Dec<br /><br />

### Analysis Approach – Segmented univariate analysis<br />
**Segmented variate analysis Observation:**<br />
• 60 months term charged off is 25% compare with 36 months term which is 11%. Prefer term is 36 months.<br />
• Lower grade charge off rate is way high than higher grade.Charge off for Grade E (27%), F (33%) and G(35%) , how ever Grade A (6%), B(12%), C(17%), D (22%)<br />
• Sub grade: sub grade is aligning with Grade behaviour. Charge off percentage is in ascending order from A1 to F5. Slight diffrence behaviour on G1 to G5 grade.However number of records contributed to G subgrade is way lower than other grades. we can ignore subgrade G*.<br />
• Not much variant in charge_off percentage based on Emp_length<br />
• Not much variant in charge_off percentage based on home_ownership<br />
• verification status verified is just 3% higher than non_verified no major variance<br />
• purpose High charge off percentage. small_business (28%). renewable_energy (19%) educational (17%)<br />
• addr_state NE state has high charge off rate 60%. However only 5 records contributed. So Ignoring.<br />
• pub_rec_bankruptcies 2 , charge off is 40% which is high . pub_rec_bankruptcies 1 is 22% <br />
• pub_rec_bankruptcies 0 is 14%<br />
• No of loans applied on sep, Oct, nov, dev month is high compare to other months. <br /><br />

### Analysis Approach – Bivariate Analysis:<br />
**Bivariate Analysis Observation**<br />
**Prerequisite:**<br />
Converted numical variable in to categorical dti, funded_amt, Interested_rate and income. Analyzed 
all possible combination of 
'emp_length','grade','home_ownership','pub_rec_bankruptcies','term','purpose','verification_status
','month','dti_slab','funded_amnt_slab','int_rate_slab','income_slab' where chargedoff rate is more 
than 30%. this has been achived via loop.<br />
**Observations:** <br />
• funded_amnt_slab (30000.0, 35000.0], emp_len = 6 years and charged off is 35%<br />
• [20.0, 24.0] interest slab has highest charged off rate<br />
• lower grade has high charged off percentage<br />
• Grade D and E charged off percentage is high for all months along with Grade F & G.<br />
• pub_rec_bankruptcies = 1 and home_ownership is OTHER and charge off percentage is 67%<br />
• int_rate slab (20.0, 24.0), home_ownership = OWN, RENT, charge off is very high 50%, 40%<br />
• funded_amnt_slab (5000.0, 10000.0], pub_rec_bankruptcies = 2.0, charge off is 50%<br />
• funded_amnt_slab 30000.0, 35000.0 pub_rec_bankruptcies = 2.0, charge off is 67%<br />
• dti_slab 10.0, 15.0 and purpose = renewable_energy, charge off percentage is 35. <br />
• dti_slab 25.0, 30.0 and purpose = renewable_energy, charge off percentage is 50. <br />
• Purpose = small_business and funded_amnt_slab is [10000.0, 15000.0], [15000.0, 20000.0] [20000.0, 25000.0] charged off is 30+ %<br />
• purpose = vacation, funded_amnt_slab = [15000.0, 20000.0], charged off = 42%<br />
• purpose = medical, funded_amnt_slab =(15000.0, 20000.0], charged_off = 50%, funded_amnt_slab = (30000.0, 35000.0] charged_off = 67%<br />
• purpose = small_business funded_amnt_slab = (30000.0, 35000.0] , charged_off = 46%, <br />
• int_rate_slab (15.0, 20.0] and (20.0, 24.0], purpose = small_business , educational , house , medical, moving , charge off percentage is more than 35% <br />
• funded_amnt_slab (30000.0, 35000.0] , november and december, charge off is more than 35% <br />
• int_rate_slab is 20.0, 24.0, from 7th month to 12th month, charge off is more than 35% <br />
• funded_amnt_slab (30000.0, 35000.0], dti_slab (25.0, 30.0], (15.0, 20.0] (20.0, 25.0] , charge off is more than 30%<br />
• int_rate_slab (20.0, 24.0], all dti slab, charge off rate is more than 40%<br /><br />

## Business Insights<br />
• Most of the Loan amounts are between 5000 15000<br />
• Most of the interest rates between 8 to 14%<br />
• Most of the Annual income is in the range of 30,000 and 60,000<br />
• 76% of loans are 36 months term and 24% loans are 60 months term<br />
• 85% of loan is fully paid and 15% of loan is charged off.<br />
• 60 months term charged off is 25% compare with 36 months term which is 11%. Prefer term is 36 months.<br />
• Lower grade charged off rate is way high than higher grade.<br />
• High charged off percentage purpose are small_business (28%). renewable_energy (19%)<br />
• No of loans applied on Sep, Oct, Nov, Dec month is high compare to other months.<br />
• Grade D and E charged off percentage is high for all months along with Grade F & G.<br />
• int_rate slab (20.0, 24.0), home_ownership = OWN, RENT, charged off is very high 50%, 40%<br />
• Small business has more than 30% of charged off for most of the income slab.<br />
• Lower income slab, Medical purpose has 30% of charged off.<br />
• 5 to 10% interest rates, charged off percentage is low across all income slabs.<br />
• When income increases charged off decreases for 5 to 10% interest rates.<br />
• 10k to 15kof funded amount , bankrupcy = 2.0, charged off percentage is 90+ 08/06/22 educational (17%)<br />
• High interest slab charged off rate is high. lending club are on track to identify person is likely to default and provided higher interest rates.<br />
• purpose medical, funded_amt = 30k to 35k, charged off rate is >65%<br />
• purpose medical, funded_amt = 25k to 30k, charged off rate is >45%<br />
• purpose wedding , charged off rate is more than 30% for 30k to 35k fund amount.<br />
• purpose vacation, charged off rate is more than 30% for 15k to 20k fund amount<br />

## Technologies Used
jupyter notebook<br />
python<br />
numpy<br />
pandas<br />
matplotlib<br />
seaborn<br />

## Acknowledgements


## Contact
Created by @shangardevi


