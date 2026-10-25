# HCDE410 Lina Lo

# A2 - Exploring sources of bias in data

### Datasets:
- **Toxicity dataset and Toxicity Annotation dataset:** [data](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973) (Note: this is 35Mb!), [documentation](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release#Toxicity), [questionnaire shown to crowdworkers](https://github.com/ewulczyn/wiki-detox/blob/master/src/modeling/toxicity_question.png)
- **Aggression dataset:** [data](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Aggression/4267550) (Note: this is 74Mb!), [documentation](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release#Aggression), [questionnaire shown to crowdworkers](https://github.com/ewulczyn/wiki-detox/blob/master/src/modeling/aggression_question.png)
- **Personal attacks dataset:** [data](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Personal_Attacks/4054689) (this is only 92k), [documentation](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release#Personal_Attacksv), [questionnaire shown to crowdworkers](https://github.com/ewulczyn/wiki-detox/blob/master/src/modeling/attack_question.png)

**Source:** https://meta.wikimedia.org/wiki/Research:Detox/Data_Release
**License / terms of use:** CC0 1.0 Universal (Public Domain)

**AI Statement:** 
- I used AI for Q5-6. The detailed responses (including prompt, output, what I changed) are found below each corresponding answer.


## 2.1 Questions and Answers (Descriptive Statistics)

**Q1. What is the gender distribution of these workers?**

Male was the most commonly reported gender, representing 3676 workers (63.59%), followed by female, representing 2103 workers (36.38%). The least commonly reported gender was "Other", representing only 2 workers (0.03%).

**Q2. What is the distribution of the workers by first language?**

4713 workers (81.53%) reported English as their first language, while 1068 workers (18.47%) did not. 

**Q3. What is the distribution of these workers by age group?**

The largest age group reported was 18–30, with 2,911 workers (50.35%), followed by ages 30–45 with 2,078 (35.95%), ages 45–60 with 514 (8.89%), and under 18 with 116 (2.01%). The smallest age group reported was over-60, with 50 workers (0.86%). 112 workers (1.94%) also had a blank age-group value.

**Q4. What is the distribution of these workers by education level?**

The most common education level reported was a bachelor's degree, representing 2,303 workers (39.84%), followed by high school with 1,657 (28.66%), master's degrees with 931 (16.10%), professional degrees with 684 (11.83%), some education with 141 (2.44%), and doctorate degrees with 61 (1.06%). The least common category reported was “none,” with 4 workers (0.07%), indicating no education level.

**Q5.** Analyze all_annotators in Sheets or Jupyter: Do any of the fields in this dataset have missing data? If so, which fields, and what % of the rows contain missing values?

The dataset contains a missing field in the age group category, where 112 workers have a missing age group value (1.94% of the rows). Earlier, I wasn't sure what this missing field meant, even when discussing the distribution in Q3. Missing field information like that can affect the analysis of the annotator distribution because it can skew the percentage and make the analysis inaccurate.

- **AI prompt:** Use the Python pandas library to create a table that could show missing values or empty cells in a dataset. This is supposed to help answer "Do any of the fields in this dataset have missing data? If so, which fields, and what % of the rows contain missing values?" For reference, this is how one of the tables is being formatted:
```
by_gender = df.groupby("gender").size()

gender_percentage = (by_gender / by_gender.sum() * 100).round(2)

gender_data = {
    "Number of Workers": by_gender,
    "Percentage %": gender_percentage
}

gender_table = pd.DataFrame(data=gender_data)
display(gender_table)
```

- **AI Output:**
```
#Treat empty cells as missing values
df_check = df.replace(r'^\s*$', pd.NA, regex=True)

#Calculate missing values and percentages
missing_table = pd.DataFrame({
    "Field Name": df_check.columns,
    "Number of Missing Values": df_check.isna().sum().values,
    "Percentage of Rows with Missing Values (%)": (
        df_check.isna().sum().values / len(df_check) * 100
    ).round(2)
})

display(missing_table)
```

- **What I changed:** For this question, I wasn't sure how to code how to check empty cells so I didn't change the code that the AI gave me as it already worked as intended. From this, I was able to identify any missing fields the dataset had.


**Q6.** Build a version of the all_annotators dataset *without removing duplicates*, then re-run the summary statistics from questions 1-4. How have these summary statistics changed?

Including both the aggression and attack workers changed the percentage values of the distribution, as workers' demographic data are counted and represented twice in the annotator dataset. The all_annotators dataset originally contained only 5,781 workers but has now increased to 7,971 workers. As a result, some percentages slightly changed, such as women going from 36.38% to 36.92%. Although these changes were very slight, this new dataset could still be misleading, as the distribution of the overall annotator population is inaccurate and shows how duplicated data could skew descriptive statistics, leading someone to make incorrect conclusions.


- **AI Prompt:** Help me figure out how I could create a dataset that contains all toxicity_annotators, attack_annotators, and aggression_annotators in one dataset. Each of them contain a dataset reference that corresponds to each worker/annotator, and I need to figure out how I can create an all_annotators list that keeps duplicates based on this code: 
```
def finalize_dataset(list1, list2):
    
    #combine the two lists into a new one
    combined_list = list1 + list2
    
    #initialize our counter variable
    new_id = 1
    
    for w in combined_list:
        #add the new sequential id field, and populate with the current value of 'counter'
        w.update({"unique_id" : str(new_id)})
        
        #increment the counter variable by 1, so that the next ID will be one number higher
        new_id = new_id + 1
        
    return combined_list

#create our new combined list with sequential IDs
all_annotators = finalize_dataset(toxicity_annotators, attack_aggro_annotators)

#print the list length and a sample, for sanity-checking purposes
print(len(all_annotators))
print(all_annotators[0])

```

- **AI Output:**

```
datasets_with_duplicates = [
    ("toxicity", toxicity_annotators),
    ("attack", attack_annotators),
    ("aggression", aggression_annotators)
]

rows_with_duplicates = []

for dataset_name, records in datasets_with_duplicates:
    for record in records:
        row = record.copy()
        row["dataset"] = dataset_name
        rows_with_duplicates.append(row)

df_duplicates = pd.DataFrame(rows_with_duplicates)

print("Original dataset rows:", len(df))
print("Dataset rows with duplicates:", len(df_duplicates))
```
- **What I changed:** I changed the name of some of the variables so I could better understand what it meant.


*Exercises and assignments for HCDE410: Human Data Interaction. Everything here is a work in progress unless otherwise noted :)*
