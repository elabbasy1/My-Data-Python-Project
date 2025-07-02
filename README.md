# OverView

Welcome to my exploration of the data job market, with a focus on data analyst positions. This project was inspired by a desire to better understand and navigate job opportunities in the field. It examines the highest-paying and most sought-after skills to identify the best career prospects for data analysts.

The data used comes from Luke Barousse’s Python course as well as my python skills that I have developed in university, which serves as the foundation for this analysis and includes detailed insights on job titles, salary ranges, locations, and key skills. Using a collection of Python scripts, I address important questions such as which skills are most in demand, how salaries vary, and how skill demand aligns with compensation in the data analytics space.

## The following questions guide the focus of this project:
1.What are the most in-demand skills for the three most    popular roles in data?

2.How are the most in-demand skills evolving for Data Analyst roles?

3.What is the salary outlook for Data Analyst roles and their associated skills?

4.What are the most valuable skills for data analysts in terms of job demand and pay?


## Tools I used for this python project:

To dive deeper into the data analyst job market, I utilized a range of powerful tools.

Python served as the foundation of my analysis, enabling me to explore the data and uncover key insights. I leveraged several powerful Python libraries throughout the project:

Pandas – Used for data manipulation and analysis.

Matplotlib – Employed to create basic visualizations of the data.

Seaborn – Utilized for producing more advanced and aesthetically appealing charts.

To run my Python code and document my findings, I used:

Jupyter Notebooks – Ideal for combining code, outputs, and notes in a single environment.

Visual Studio Code – My primary editor for writing and executing Python scripts.

For version control and collaboration, I relied on:

Git & GitHub – Essential tools for tracking changes, managing code versions, and sharing my work effectively.


## Data Preprocessing and Cleaning

This section details the process of preparing the data to ensure it is accurate and ready for analysis.

### Import & Clean Up Data using pandas, matplotlib and seaborn
I begin by importing the required libraries and loading the dataset, followed by initial cleaning steps to ensure data quality.


<pre> 
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
</pre>


## Filter Ireland jobs

To tailor my analysis to the Irish job market, I filter the dataset to include only roles located in Ireland


<pre> 

df_IR = df[df['job_country'] == 'Ireland']

 </pre>


 ## My Analysis

 Each Jupyter notebook in this project was designed to explore a specific aspect of the data job market. Here's how I addressed each question:


 ## 1.What are the most in-demand skills for the three most    popular roles in data?

 To identify the most in-demand skills for the top three most common data roles, I filtered the dataset to isolate the most frequently listed job titles. From there, I extracted the top five skills associated with each of these roles. This analysis highlights the most popular job titles and their key skills, helping me understand which competencies to prioritize based on the role I'm aiming for.

View the note book for more details here:
[2_skills_demand.ipynb](mohamed_elabbasy_project\2_skills_demand.ipynb)


## Data Visualization



<pre> 

fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()

 </pre>


 ## Results

 ![Visualization of top skills in Ireland](Images\plot1.png)

A bar chart illustrating the salaries of the top three data roles alongside their five most relevant skills.


## Insights:

For both Data Analysts and Data Engineers, SQL is the most in-demand skill, appearing in more than 50% of job postings. In contrast, Python is the most commonly required skill for Data Scientists, showing up in 53% of listings.

Data Engineers tend to need more specialized technical expertise—such as AWS, Azure, and Spark—whereas Data Analysts and Data Scientists are typically expected to be skilled in broader data analysis and management tools like Excel and Tableau.

Python and SQL are versatile and highly sought-after skills across all three roles, with Python being especially prominent among Data Scientists (53%) as the most adaptable tool as well as SQL for data analayst.

In the context of data-related roles in Ireland, the least frequently requested skills offer insight into niche tool usage and potential areas for differentiation. For Data Analysts, Power BI appears as the least demanded skill, with only 21% of job postings referencing it. This may indicate a preference for broader tools like SQL and Excel in analytical roles.

Among Data Engineers, Apache Spark is the least mentioned, also at 21%. Despite its strength in big data processing, it seems to be a more specialized requirement, with many roles prioritizing foundational technologies like SQL and Python.

For Data Scientists, AWS stands out as the lowest in demand, appearing in just 14% of postings. This suggests that while cloud platforms are valuable, core statistical programming skills such as Python and R take precedence in these roles.



## 2.How are the most valued skills evolving for Data Analysts?

To analyze skill trends for Data Analysts in 2023, I filtered job postings specific to data analyst roles and organized the listed skills by month. This approach revealed the top five skills per month, highlighting how their popularity shifted over the course of the year.


You can view more details here:
[3_skills_trending](mohamed_elabbasy_project\3_skills_trending.ipynb)

##  Data Visualization


<pre> 

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

 </pre>

 # Results

 ![Visualization for treding skills](Images\plot2.png)

 Bar graph showing the top trending skills among Data Analysts in Ireland during 2023.

 ## Insights:

 1. SQL continues to be the most consistently sought-after skill over the year, despite a slight decline in demand.

 2. Starting in September, Excel saw a notable rise in demand, eventually overtaking both Python and Tableau by year-end.

 3. Excel experienced a noticeable drop in demand beginning in September, yet still ended the year ahead of both Python and Tableau.

4. Python and Tableau maintained relatively steady demand throughout the year, with minor fluctuations, and continue to be key skills for data analysts. While Power BI was less in demand compared to the other tools, it showed a modest upward trend toward the end of the year. Notably, Tableau experienced a brief increase in June but quickly returned to its previous levels.


## 3. How are salaries influenced by skills and job types for Data Analysts?


To determine which roles and skills offer the highest pay, I focused exclusively on jobs based in Ireland and analyzed their median salaries. Before diving into specific skills, I examined the salary distributions of common data roles—such as Data Scientist, Data Engineer, and Data Analyst—to gain insight into which positions tend to command the highest earnings.


You can view more details here: [4_salary_analysis](mohamed_elabbasy_project\4_salary_analysis.ipynb)



##  Data Visualization



<pre> 

sns.boxplot(data=df_IR_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
 </pre>

 ## Results

![Salary for data jobs in Ireland](Images\plot3.png)


Box plot showing salary distributions for the top six data-related job titles.

# Insight: 


1. Among all data roles, Machine Learning Engineers clearly command the highest salaries in Ireland. The entire interquartile range (middle 50% of salaries) is significantly higher than the other roles, and even the lower bound starts above €100K. This suggests a strong demand for advanced AI and ML skills in the market, likely driven by their increasing adoption across industries.
2. Senior Titles Don’t Always Mean Higher Pay
Interestingly, Senior Data Engineers and Senior Data Scientists have narrower salary ranges compared to other roles, and their upper salary levels don’t surpass those of Machine Learning Engineers. This indicates that while senior roles suggest experience and responsibility, the niche skillset of ML Engineers is valued more highly — a reflection of market scarcity and specialization.


3. Data Analysts Have the Widest Pay Range at the Lower End
Data Analysts show the broadest salary distribution, especially on the lower end of the spectrum, with a wide interquartile range and several outliers. This could suggest that analyst roles are more accessible to early-career professionals, with pay increasing substantially with experience or industry, but also suffering from inconsistency in pay scales.


4. Outliers Hint at Exceptional Opportunities
Roles like Data Analyst and Data Scientist show a few outliers well above the interquartile range, indicating that while most professionals earn within a predictable band, some individuals are securing much higher salaries. These outliers may represent niche industry sectors, highly experienced individuals, or companies with aggressive compensation strategies to attract top talent.


5. Moderate Range for Data Engineers Suggests Stability
The salary distribution for Data Engineers is relatively stable and well-contained, with a solid interquartile range and fewer extreme values. This could reflect the maturing nature of this role in the industry — it’s in high demand, but employers have developed more consistent pay benchmarks over time.


## Top-Paying and Most In-Demand Skills for Data Analysts

Next, I refined my analysis to focus specifically on data analyst roles. I examined both the top-paying skills and the most sought-after ones, presenting the findings using two bar charts.


##  Data Visualization

<pre> 

fig, ax = plt.subplots(2, 1)  

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analystsr')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()
 </pre>


 ## Results

 This is a breakdown of the top-paying and most in-demand skills for data analysts in Ireland.



![Heighst paid skills](Images\plot4.png)


## Insight:

1. Git: The Unexpected Goldmine
Git tops the chart as the highest-paid skill for data analysts, with salaries nearing €200K. While Git is typically viewed as a developer tool, its dominance here shows how essential version control and collaboration are even in data roles. Analysts fluent in Git are likely involved in more technical, code-heavy projects—hence the premium pay.

2. Snowflake Reigns Supreme in Demand
Snowflake appears in both charts—it's not only among the top-paying skills but also ranks as the most in-demand. This dual presence suggests a booming market for cloud-based data warehousing. If you're a data analyst eyeing future-proof skills, Snowflake might be your smartest bet.

3. Linux and Oracle Signal Legacy + Power
Linux and Oracle sit high on the salary chart, reflecting their importance in larger, possibly older enterprise systems. These tools may not be as trendy as Python or Tableau, but companies still pay top euro for analysts who can navigate legacy tech while delivering powerful insights.

4. The Python Paradox
Python is a staple in the data analyst toolkit and ranks second in demand—but it’s noticeably absent from the highest-paid skills list. This suggests that while Python is essential and widely used, its ubiquity might lower its “scarcity premium,” unlike niche skills like Git or Unify.

5. The BI Tool Salary Gap
Tableau, Power BI, and Excel appear in the most in-demand list but not in the top-paid list. This shows a disconnect: these tools are popular and often required, yet they don’t command high salaries. Analysts wanting to boost their earnings might consider pairing BI tools with more technical, backend-oriented skills like Snowflake or Airflow.


## 4. Which skills are the most valuable for Data Analysts to learn?"

To determine the most optimal skills for data analysts to learn—those that are both highly paid and in high demand—I calculated each skill’s demand percentage and its median salary. This approach makes it easier to pinpoint which skills offer the best value for career growth.

You can view more details here: [5_optimal_skills](mohamed_elabbasy_project\5_optimal_skills.ipynb)



##  Data Visualization

<pre> 
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()

 </pre>


 ## Results

 This is a breakdown of the top-paying and most in-demand skills for data analysts in Ireland.



![Most optimal skills](Images\plot5.png)


## Insight:

1. Git and Linux: High Pay, Low Popularity
Git and Linux stand out in the top-left corner—offering some of the highest median salaries (~€200K) but appearing in only a small share of job postings. These technical skills may not be required in every role, but when they are, they command premium pay—likely due to their importance in data engineering and DevOps-heavy analyst positions.

2. SQL: Ubiquitous and Reliable
SQL appears on the far right, used in nearly 60% of data analyst job listings, making it by far the most in-demand skill. While it doesn't offer the highest salary (~€90K), its essential nature and near-universal requirement make it an absolute must-have for any aspiring or practicing data analyst.

3. Snowflake: A Balanced Winner
Snowflake is a sweet spot on the graph—offering both high salary (~€150K) and moderate demand (~20%). Its rising popularity in cloud-based analytics makes it a smart investment for analysts who want to boost both their employability and earning potential.

4. BI Tools Lag Behind in Pay
Despite being widely used—like Tableau, Power BI, and Excel—these business intelligence tools offer below-average salaries. This suggests they are often considered entry-level or generalist tools. Pairing them with more technical skills like SQL, Snowflake, or Python could significantly improve salary prospects.

5. Python and R: Popular and Well-Paid
Python and R both sit in a high-demand, mid-to-high salary range. These languages are foundational for data analysis and machine learning, and they strike a strong balance between broad applicability and competitive compensation—making them essential skills for analysts aiming to grow technically.

## A Visualization of Various Technologies

We'll also include a visualization of the different technologies in the graph, using color labels to represent each category (e.g., {Programming: Python})




##  Data Visualization


<pre> 
from matplotlib.ticker import PercentFormatter

# Create a scatter plot
scatter = sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology',  # Color by technology
    palette='bright',  # Use a bright palette for distinct colors
    legend='full'  # Ensure the legend is shown
)
plt.show()

 </pre>


# Results



![Most optimal skills 2](Images\plot6.png)


A scatter plot illustrating the most valuable skills for data analysts in the US—those with high pay and high demand—using color-coded labels to represent different technologies.



# Insight:

1.
The scatter plot reveals that most programming-related skills (shown in blue) are concentrated around higher salary ranges. This suggests that having strong programming abilities can lead to better-paying opportunities within the data analytics profession.

2.
Database technologies (represented in orange), like Oracle and SQL Server, are linked to some of the top-paying roles for data analysts. This reflects a strong industry need and high value placed on skills in data handling and database management.

3.
Analyst tools (highlighted in green), such as Tableau and Power BI, appear frequently in job listings and come with solid salaries. This demonstrates that data visualization and analysis platforms are essential in today’s data analyst roles, offering both good compensation and adaptability across various tasks.



# What I have learned from this project?

Throughout this project, I gained deeper insight into the data analyst job landscape while sharpening my technical abilities in Python—particularly in data wrangling and visualization. Below are some of the key lessons I took away:

Advanced Python Application:
Working with libraries like Pandas for data manipulation and Seaborn and Matplotlib for visualization allowed me to handle complex analysis tasks more effectively. These tools enhanced my efficiency and expanded my analytical capabilities.

Value of Data Cleaning:
I discovered that meticulous data cleaning and preparation are essential steps before diving into analysis. Ensuring data quality upfront is critical for generating accurate and meaningful insights.

Skill Strategy Matters:
This project highlighted how crucial it is to align your skillset with industry needs. By understanding how skill demand correlates with salary and job opportunities, I realized how important strategic upskilling is for long-term success in the tech world.



# Insights:

This project offered several key insights into the data analyst job market:

Connection Between Skill Demand and Salary:
A strong link exists between how in-demand a skill is and the salary it can earn. Specialized, advanced skills like Python and Oracle are often associated with higher pay, reflecting their value in the industry.

Evolving Market Trends:
The demand for certain skills is constantly shifting, emphasizing how fast-paced and dynamic the data job landscape is. Staying current with these changes is crucial for continued career advancement in analytics.

Economic Impact of Skill Choices:
Recognizing which skills offer both strong demand and high compensation can help data analysts prioritize what to learn next. This approach supports smarter upskilling and maximizes professional and financial growth.



# Challanges that faced me

This project came with its challenges, but it also offered valuable learning experiences:

Handling Data Inconsistencies:
Dealing with missing or inconsistent data required thoughtful approaches and robust data-cleaning methods to maintain the reliability and accuracy of the analysis.

Designing Complex Visuals:
Creating clear and impactful visualizations for intricate datasets was demanding, but essential for effectively communicating key insights and patterns.

Balancing Detail and Overview:
Striking the right balance between deep exploration and a broad perspective was a continual challenge, requiring careful judgment to ensure the analysis remained both thorough and focused.



# Overall Conclusion

This deep dive into the data analyst job market has been highly insightful, shedding light on the key skills and trends driving this dynamic field. The insights gained have not only deepened my understanding but also offer practical direction for anyone aiming to grow their career in data analytics. As the industry continues to evolve, ongoing analysis will be vital to staying competitive. This project serves as a strong starting point for further exploration and reinforces the importance of continuous learning and adaptability in the world of data







































