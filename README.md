# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I amtargeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](Final proj\Skill_count.ipynb)


### Visualize data
fig, ax = plt.subplots(len(job_titles), 1, figsize=(10, 5 * len(job_titles)))

if len(job_titles) == 1:
    ax = [ax]

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)

    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], palette='Blues')

    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_title(job_title)
    ax[i].set_xlim(0, 78)
    ax[i].legend().set_visible(False)

    # ✅ This part MUST be inside the above loop:
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f"{v:.1f}%", va='center')  # shift right for visibility
    
    if i!= len(job_titles)-1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Top skills in job postings', fontsize=15)
plt.tight_layout(h_pad=0.5)
plt.show()

![Visualization of top skills for data](Final proj\Screenshot 2025-06-24 011645.png)