# Dashboard_Payroll_Increase

## Table of Contents

- [Project Overview](#project-overview)
- [Deliverables](#deliverables)
- [Data Sources](#data-sources)
- [Data Cleaning](#data-cleaning)
- [Initial Analysis](#initial-analysis)
- [Further Analysis](#further-analysis)
- [Dashboard – Initial Steps](#dashboard--initial-steps)
- [Slices](#Slices)
- [Final Dashboard](#final-dashboard)
- [Final Results](#final-reuslts)

## Project Overview 

- The aim of this practice is to refine key concepts of data analysis such as: Analysing Business Requests, Transforming Data, Cleaning Data, Using Business Logic to bring Value, Storytelling, Dashboard Design, among others.

### Case Study
You are a payroll analyst working for Gran Empresa de TI, SA de CV, a global technology company with a presence around the world. You specialize exclusively in the payroll for Mexico.

Currently, salary increases for next year are being analyzed, and there are two differing opinions on how they should be applied.

The local managers in Mexico want to create an egalitarian plan, assigning equal raises to all employees because that’s the way it has always been done. The Vice Presidents in the United States, however, have been studying the raise practices of a competitor, MacroHard INC, where low-performing employees are terminated and high-performing employees receive higher raises.

The main reason why low-performing employees are not terminated in the Mexican division of Gran Empresa de TI is that Mexican Labor Law requires very costly severance payments for dismissed employees. For this reason, managers prefer to keep a low-level employee rather than justify the massive severance payment.

The company evaluates employees on a scale from 1 to 5, with 1 being the rating for the worst employees and 5 being the highest rating. The American plan involves firing all employees with a rating of 1 and giving double the proposed raise to employees rated 4 and 5. The Mexican plan involves not firing anyone and giving the same raise to everyone.

Your task is to provide the numbers for the decision by calculating the costs of both scenarios and presenting them in a dashboard format.

## Deliverables

Create a dashboard that shows the following:
  - Total current payroll expense (all components)
  - Cost of implementing the American plan, in dollars and percentage
  - Cost of implementing the Mexican plan, in dollars and percentage
  - Chart of current costs by performance rating
  - Table of current costs by department, in dollars and percentage
  - Two additional slicers (by grade and by department)

Your report should incorporate all the necessary data so that managers have a clear picture of the situation. You should clean the data if necessary. The report must be dynamic and include new data as it becomes available.

There is no single correct answer. You will be evaluated based on how versatile your file is, the quality of your analysis, and the clarity of your presentation.

## Data Sources
  - Princial - Base Datos - Data for all employees currently on the payroll
  - Documento 1 - Salary increases
  - Documento 2 - Errors
  - Documento 3 - Article 50 (Severance pay under the Federal Labor Law)

## Data Cleaning
Data cleaninng consisted on gathering all tables into a main normalized Table. We also fixed grammar errors with Search and Replace, Date Formatting, and removed extra blank spaces on text columns.

## Initial Analysis
First of all, we needed to determine the Mexican and American Salary Raise, in order to do such we added the following columns:
  - Total Slary Base before raise: The sum of all the payment categories of every employee. =SUM(Data[@[Salary Base]:[General Bonus]])
  - Mexican Salary Raise: By multiplying each value category payment of every employee with the corresponding % increase given on the pdf file. =SUMPRODUCT(Data[@[Salary Base]:[General Bonus]],Table2)
  - American Salary Raise: By multiplying Mexican Salary Raise*2, since the American Raise considers increasing twice the Mexican proposed increase but only to employees with score 4 o 5 and firing employuees with score 1. We later apply this filter during Pivot process. =[@[Mexican Salary Raise]]*2


## Further Analysis
In order to understand and compare how convinient is implementing the American plan (consisting on layoff employees which means paying "Indemnización" or Layoff Cost), we have to calculate how much Layoff bonus would employees receive if they had to go. For such analysis, we had to read the pdf given. The pdf file mentions the layoff cost consist on paying 3 months of salary + 20 days of salary for each year working year to the employee. Thus the calculation went as follows:
  - 3 Month Salary: =[@[Total Salary Before]]*3
  - Employee working hours: Calculated taking date base first working day of the next year 2018 which is Jan 2nd, 2018 less the date each employee were hired divided by the 365 days.   =(43102-[@[Hiring Date]])/365 
  - Daily Salary: Taken dividing total salary by 30 days =[@[Total Salary Before]]/30
  - 20 Days per Year Layoff Bonus: The main data we are interested. Taken by multiplying Daily Salary * 20 * Employee Years. =[@[Daily Salary]]*20*[@[Employee Working Years]]
<img width="450" height="731" alt="image" src="https://github.com/user-attachments/assets/a728d528-44ef-40cb-a915-ee7aa49124ba" />



Once we have the complete normalized table we can now work with Pivots to get the main data we will need for the Dashboard. 

 - Total current payroll expense (all components)
   
    <img width="177" height="62" alt="image" src="https://github.com/user-attachments/assets/25724d10-5f43-41d5-b509-259b8d57422b" />

- Cost of implementing the American plan, in dollars and percentage
  
    <img width="751" height="86" alt="image" src="https://github.com/user-attachments/assets/06a58e39-bca6-46bc-a165-49e8c77d505e" />

- Cost of implementing the Mexican plan, in dollars and percentage
  
    <img width="414" height="83" alt="image" src="https://github.com/user-attachments/assets/64e065b0-3a74-4bd2-81d4-d2c4b4623b77" />

 - Chart of current costs by performance rating
   
    <img width="394" height="128" alt="image" src="https://github.com/user-attachments/assets/0fd77a26-7c04-4ebb-a155-665a3ed3149a" />

- Table of current costs by department, in dollars and percentage
  
    <img width="387" height="211" alt="image" src="https://github.com/user-attachments/assets/d63cdce2-0d64-420b-b4f2-35dcee2cac0e" />
