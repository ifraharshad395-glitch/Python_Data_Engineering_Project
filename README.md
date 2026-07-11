# The Analysis  

## 1. What are the skills most in demand for the top 3 most popular data roles?  

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.  

View my notebook with detailed steps here: [2_Skills_Demand.ipynb](2_Project/2_Skills_Demand.ipynb)  

### Visualize Data  

```python 
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    #df_plot.plot(kind='barh', x = 'job_skills', y = 'skill_pct', ax=ax[i], title = job_title)
    sns.barplot(data=df_plot, x = 'skill_pct', y = 'job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_ylabel(' ')
    ax[i].legend().set_visible(False)

fig.suptitle('Likelihood of Skills Requested in USA Job Postings', fontsize=15)
fig.tight_layout()
plt.show()  
```  

### Results  

![Visualization](2_Project\Images\likelihood_image.png)  

### Insights  

- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.  

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).  

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).  


## 2. How are in-demand skills trending for Data Analysts?  
  
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.  

View my notebook with detailed steps here: [2_Skills_Demand.ipynb](2_Project/3_Skills_Trend.ipynb) 

### Visualize Data  

```python  
from matplotlib.ticker import PercentFormatter

df_plot = df_DA_USA_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')
sns.set_theme(style='ticks')
sns.despine() # remove top and right spines

plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

# annotate the plot with the top 5 skills using plt.text()
for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i], color='black')

plt.show()
```  

### Results  

![Visualization](2_Project\Images\trend.png)   