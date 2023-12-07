H1-B-VISA-APPROVAL-DATASET-2019
H1-B Visa is the most sought-after non-immigrant visa that allows foreign workers to work in United States in specialty occupation. In 2019, more than 1 million applicants applied to get an H-1B visa including new applications, renewals and transfer of H1-B to another company. There were more than 180,000 new applicants for H1-B, however, only 80,000 applications were picked up in the lottery process for taking it further to USCIS for approval.

The uncertainty in getting an H1-B visa creates employment and legal status uncertainties for a job application and high legal and visa processing fees for the organization over the period of employment. We plan to use the anonymized dataset for 2019 that United Status Department of Labor publishes publicly and apply data science techniques to improve predictability of approval.

Features
Dataset and Features Parsing the 2019 excel data into, we found 589,414 cases for H1-B applications. The dataset contains features that gives information about employer and visa applicant.

CASE_STATUS: Excluding the Withdrawn and Certified-Withdrawn, Certified decision is considered as 1 outcome in the resulting dataset and Denied as 0. This is used to model the outcome. VISA_CLASS: Only H1-B visa class is being modeled in this paper which contributes to the majority of datapoints, we exclude the records for other work visas such as E-3 Australian, H-1B1 Chile and H-1B1 Singapore. EMPLOYER_NAME: The employer name submitting the visa application. We believe employer name is one of the important features to profile the visa application. As per NY times, some companies are manipulating the visa process by flooding the system .

SECONDARY_ENTITY: Whether the applicant will be places in a secondary location. This feature is assumed to be helpful since majority of Consultancy companies that are believed to outsource software services which have reputation to flood the visa processing . AGENT_REPRESENTING_EMPLOYER: If another firm is representing the employer and its application. We plan to model this feature to see if an agency has high rejection rates as compared to another.

JOB_TITLE, SOC_NAME: Job title and SOC name have details about the position, occupation field and seniority of the applicant. SOC_CODE, NAICS_CODE: They are standard categories of a job.

CONTINUED_EMPLOYMENT: If this is a re-new visa application

CHANGE_PREVIOUS_EMPLOYMENT: If an application will continue without changes in job duties

NEW_CONCURRENT_EMPLOYMENT: If the applicant will have an additional employer

CHANGE_EMPLOYER: If applicant will get the visa with a new employer

AMENDED_PETITION: If an applicant will work with the same employer with changes in duties FULL_TIME_POSITION: If this application is for full-time position

H-1B_DEPENDENT: If an employer is categorized to be H1-B dependent. SUPPORT_H1B: If this application will be used in the future to file for H1-B petitions

WILLFUL_VIOLATOR: If an employer has violated H1-B rules in the past.

WAGE_RATE_OF_PAY_FROM: Employer’s proposed wage rate

WAGE_UNIT_OF_PAY: Paycheck frequency.

TOTAL_WORKER: Total amount of workers in the company filing the application.

EXPLORATORY DATA ANALYSIS
In this phase we will analyze the data to find out:

Missing Values
All the Continuous Varibles
Distribution of the continuos variables
*Select the relevant features:

to_select = ['CASE_NUMBER', 'CASE_STATUS', 'EMPLOYER_NAME', 'SECONDARY_ENTITY_1', 'AGENT_REPRESENTING_EMPLOYER', 'PERIOD_OF_EMPLOYMENT_START_DATE', 'JOB_TITLE', 'SOC_TITLE', 'SOC_CODE', 'NAICS_CODE', 'FULL_TIME_POSITION', 'NEW_CONCURRENT_EMPLOYMENT', 'PREVAILING_WAGE_1', 'CONTINUED_EMPLOYMENT','CHANGE_PREVIOUS_EMPLOYMENT', 'CHANGE_EMPLOYER', 'AMENDED_PETITION', 'H-1B_DEPENDENT', 'SUPPORT_H1B', 'WILLFUL_VIOLATOR', 'WAGE_RATE_OF_PAY_FROM_1', 'WAGE_UNIT_OF_PAY_1', 'TOTAL_WORKER_POSITIONS']

We analyzed the data by calculating following factors-

*DISTRIBUTION OF VISA CASES WITH THE COMPANIES :

Screenshot (189)

*PIE chart showing different cases of CASE-STATUS :Screenshot (190)

What are the top OCCUPATIONS of the H1-B's being filed by the employers ?
Screenshot (192)

Which employers file the most petitions ?
Screenshot (193)

WAGE DISTRIBUTION -
Screenshot (194)

Number of Applications made for full time position:
Screenshot (195)

Correlation between different variables:
Screenshot (196)

Feature Engineering
Now for the feature Engineering part we have converted the values of "FULL_TIME_POSITION","AGENT_REPRESENTING_EMPLOYER","SECONDARY_ENTITY_1","H-1B_DEPENDENT","WILLFUL_VIOLATOR" from "Y" to 1 and from "N" to 0 and then fill out all the null values by using mode also we convertred the values of "NEW_CONCURRENT_EMPLOYMENT" , "CHANGE_PREVIOUS_EMPLOYMENT" , "CONTINUED_EMPLOYMENT", "AMENDED_PETITION" , "CHANGE_EMPLOYMER" and "TOTAL_WORKER_POSITIONS" as there are more than two unique values so we coverted all the values greater than one(1) to >1.

WORKING WITH FEATURES HAVING LOTS OF UNIQUE Values
The features that have lots of unique values we have to merge the values into some common values and convert them into less unique values the first we converted the SOC_TITLE to 12 unique features that are:

Computer Occupations
Others
Architecture & Engineering
Financial Occupation
Medical Occupations
Management Occupation
Advance Sciences
Education Occupations
Administrative Occupation
Business Occupation
Mathematical Occupations
Marketing Occupation
Then JOB_TITLE to 14 unique features that are:

IT & SOFTWARE ENGINEERS
SENIOR TEAM
others
Manager & DIRECTORS
BUSINESS TEAM
DATABASE & SCIENTISTS
MECHANICAL & CIVIL ENGINEER
EDUCATIONAL ORGANISATION
ARCHITECT
ELECTRONICS & ELECTRONICS ENGINEERS TEAM
MEDICAL TEAM
MARKETING TEAM
FINANCE TEAM
LAW TEAM
EMPLOYER_BRANCH(EMPLOYER_NAME) to 12 unique features:

TECH SOLUTIONS
others
CONSULTING COMPANIES
TOP TECH
FINANCE AND MEDICAL SOLUTIONS
ELECTRONIC & LOGISTICS SERVICES
RESEARCH LABS & NETWORK
AUTOMOTIVE & ELECTRICAL
BANKING COMPANIES
PRODUCT &ENTERPRISE COMPANIES
UNIVERSITY
BUSINESS SOLUTIONS
All selected categorical features were one-hot encoded using get_dummies function from pandas. Although this significantly increases the number of features, it is the only option since label-encoding would introduce incorrect rank between categorical variables
