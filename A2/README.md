# HCDE410 Lina Lo

# A2 - Exploring sources of bias in data

### Datasets:
- **Toxicity dataset and Toxicity Annotation dataset:** [data](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973) (Note: this is 35Mb!), [documentation](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release#Toxicity), [questionnaire shown to crowdworkers](https://github.com/ewulczyn/wiki-detox/blob/master/src/modeling/toxicity_question.png)
- **Aggression dataset:** [data](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Aggression/4267550) (Note: this is 74Mb!), [documentation](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release#Aggression), [questionnaire shown to crowdworkers](https://github.com/ewulczyn/wiki-detox/blob/master/src/modeling/aggression_question.png)
- **Personal attacks dataset:** [data](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Personal_Attacks/4054689) (this is only 92k), [documentation](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release#Personal_Attacksv), [questionnaire shown to crowdworkers](https://github.com/ewulczyn/wiki-detox/blob/master/src/modeling/attack_question.png)

**Source:** https://meta.wikimedia.org/wiki/Research:Detox/Data_Release
**License / terms of use:** CC0 1.0 Universal (Public Domain)

**AI Statement:** 
- I did use AI to help with coding this assignment. Check the 'Usage of AI' section below for a more detailed report

## 2.1 Questions and Answers (Descriptive Statistics)


**Q1. What is the gender distribution of these workers?**
Male was the most commonly reported gender, representing 3676 workers (63.59%), followed by female, representing 2103 workers (36.38%). The least commonly reported gender was "Other", representing only 2 workers (0.03%).

**Q2. What is the distribution of the workers by first language?**
1068 workers (18.47%)reported English as their first language, while 4713 workers (81.53%) did not. 

**Q3. What is the distribution of these workers by age group?**
The largest age group reported was 18–30, with 2,911 workers (50.35%), followed by ages 30–45 with 2,078 (35.95%), ages 45–60 with 514 (8.89%), and under 18 with 116 (2.01%). The smallest age group reported was over-60, with 50 workers (0.86%). 112 workers (1.94%) also had a blank age group value.

**Q4. What is the distribution of these workers by education level?**
The most common education level reported was a bachelor's degree, representing 2,303 workers (39.84%), followed by high school with 1,657 (28.66%), master's degrees with 931 (16.10%), professional degrees with 684 (11.83%), some education with 141 (2.44%), and doctorate degrees with 61 (1.06%). The least common category reported was “none,” with 4 workers (0.07%), indicating no education level.


## 2.2 

**Q5** 
The age_group field has 112 missing values, which represents 1.94% of the rows. Earlier, I wasn't sure what this missing field meant in the bar chart, even when discussing the distribution in Q3. This means this dataset has **incomplete data**, which could affect the analysis of the annotator distribution because it can skew the percentage and make the analysis inaccurate.


**Q6**
Including both the aggression and attack workers changed the percentage values of the distribution, as workers' demographic data are counted and represented twice in the annotator dataset, which is an example of **duplicated data**. The all_annotators dataset originally contained only 5,781 workers but has now increased to 7,971 workers. As a result, some percentages slightly changed, such as women going from 36.38% to 36.92% or the age group of 18-30 going from 50.35% to 49.68%. Although these changes were very slight, this new dataset could still be misleading, as the distribution of the overall annotator population is now distorted and shows how duplicated data could skew descriptive statistics, leading someone to make incorrect conclusions.


**Q7**
I believe that the demographics of the annotators do not fully represent English-speaking internet users overall, which could relate to **unrepresentative data**. [Statistica](https://www.statista.com/chart/26884/most-spoken-languages-online-offline/?srsltid=AYCX9vIjS0PpfV6O0S05G9qWuK-vcdXdM4srElkStTpXWKt-6Z8wBy-N) reported that English accounts for 51.2% of the language used online, but the majority of the annotators (~80%) reported as not their English as their first language. This matters because it could imply that this dataset has less representation of people whose first language is English than the actual population online, which may make this dataset less accurate in evaluating English because the annotators may not be as familiar with hostile speech in English, but this is only an assumption since we don't know if this necessarily makes their annotations less accurate or how fluent they are in English.


**Q8**
I believe that if these datasets were used to train a machine learning-driven "hostile speech detector" for different websites and platforms, the model might not accurately identify hostile speech in languages other than English. Because this dataset was looking at only English Wikipedia and the majority of annotators reported English as not their first language, their judgments and evaluation of hostile speech in English may not fully be accurate or reflect how hostility is expressed or interpreted in other languages and cultural contexts. This would be concerning as it could make the detector less reliable and unfair to users from underrepresented languages that were not evaluated equally in the dataset or if annotators interpreted hostile speech from their own cultural context onto English.






## 3.1

#### Code questions




**Q9. What % of workers who labelled the toxicity dataset do we have demographic data for?**

We have the demographic data for 83.49% of workers who labelled the toxicity dataset, which means that not all the workers who annotated the dataset are represented in the toxicity_worker_demographic.tsv and is an example of **incomplete data**.

**Q10. What % of the comments in the toxicity dataset were labelled by male vs. female-identified workers?**

66.02% of the comments in the toxicity dataset were labelled by male-identified workers and 33.95% of the comments were labelled by female-identified workers. This means more comments were labelled by male-identified workers than female-identified workers.

**Q11. What % of the comments in the toxicity dataset were labelled by people for whom English is NOT their first language?**

82.64% of the comments in the toxicity dataset were labelled by people for whom English is not their first language. This means that comments received from workers whose first language is not English were the majority than from those whose first language is English.


**Q12. Based on your findings from questions 9-11, how might this dataset present a biased view of "toxicity"? How would you expect such biases to impact how the Perspective API performs?**

Based on my findings for 9-11, I would say that this dataset may have a biased view of "toxicity" and could be considered **unrepresentative data**, as it may not accurately represent everyone's perspectives equally. Since male-identified workers labelled the majority of the comments, their perspectives might influence more what is considered toxic, while female perspectives may influence the dataset less. For example, different annotators may interpret subtle or passive-aggressive remarks differently. And since only a majority of comments were labelled by people whose first language is not English, the dataset may not fully represent how people from different languages interpret toxicity or if the hostile speech they identified is fully accurate, which I discussed in Q7-8. Finally, since we only have the demographic data for 83.49% of workers who annotated the toxicity dataset, this may limit our ability to understand if the demographics of the annotators are accurately representing the population it is intended to model, as it has incomplete data. These potential biases could impact how the Perspective API performs because a model trained on these annotations might not accurately classify comments as toxic and could fail to recognize toxicity in others, like if there are toxic comments from other languages or could be considered toxic for someone who is female or speaks English as a first language.

## Usage of AI:
### Q1-Q4 AI Statement:
I reused code generated from AI in Q7 and adjusted it to add bar graphs. Originally, there were only tables. Then I used the prompt below to make the bar graphs better to read

**AI Prompt:** How do I sort data on a bar chart? Also how to the bar chart horizontal?

**AI Output**

You can use .sort_values() to sort the bars and .plot.barh() to make the chart horizontal.
1. Sort bars from highest to lowest
Add .sort_values(ascending=False) before plotting:

```
language_sorted = langugage_table.sort_values(
    by="Number of Workers",
    ascending=False
)

ax = language_sorted["Number of Workers"].plot.bar(
    xlabel="English First Language",
    ylabel="Number of Workers",
    legend=False
)

plt.title("Workers by Language")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

```
2. Make the bar chart horizontal
Change .plot.bar() to .plot.barh():
```
ax = language_sorted["Number of Workers"].plot.barh(
    xlabel="Number of Workers",
    ylabel="English First Language",
    legend=False
)

plt.title("Workers by Language")
plt.tight_layout()
plt.show()
```
3. Add percentages to horizontal bars
Since the bars are horizontal, percentages go at the right end of each bar.
```
ax = language_sorted["Number of Workers"].plot.barh(
    xlabel="Number of Workers",
    ylabel="English First Language",
    legend=False
)

for i, percentage in enumerate(language_sorted["Percentage (%)"]):
    ax.text(
        language_sorted["Number of Workers"].iloc[i],
        i,
        f"{percentage}%",
        va="center",
        ha="left"
    )

plt.title("Workers by language")
plt.tight_layout()
plt.show()
```

**What I changed** A big mistake I ran into with this code was that I believed that 0 was equal to English as first language and 1 was equal to English as not first language because of the code ChatGPT gave me. This made my analysis wrong at first, until I swapped the values.

### Q5 - AI Statement:
**AI prompt:** Use the Python pandas library to create a table that could show missing values or empty cells in a dataset. This is supposed to help answer "Do any of the fields in this dataset have missing data? If so, which fields, and what % of the rows contain missing values?" For reference, this is how one of the tables is being formatted:
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
**AI Output:**
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
**What I changed:** For this question, I wasn't sure how to code how to check empty cells so I didn't change the code that the AI gave me as it already worked as intended. From this, I was able to identify any missing fields the dataset had.


### Q6 - AI Statement:

**AI Prompt:** Help me figure out how I could create a dataset that contains all toxicity_annotators, attack_annotators, and aggression_annotators in one dataset. Each of them contain a dataset reference that corresponds to each worker/annotator, and I need to figure out how I can create an all_annotators list that keeps duplicates based on this code: 
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
**AI Output:**
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
**What I changed:** I changed the name of some of the variables so I could better understand what it meant.


### Q7 - AI Statement:

**AI Prompt:** How to show percentages on top of the bars and how to label each bar? This is how I am formatting the table:
```
by_language = df.groupby("english_first_language").size()

language_percentage = (by_language / by_language.sum() * 100).round(2)

language_data = {
    "Number of Workers": by_language,
    "Percentage %": language_percentage
}
language_table = pd.DataFrame(data= language_data)
display(language_table)
```

**AI Output:** 
```
# Calculate worker counts and percentages
by_language = df.groupby("english_first_language").size()
language_percentage = (by_language / by_language.sum() * 100).round(2)

# Rename categories
language_table = pd.DataFrame({
    "Number of Workers": by_language,
    "Percentage (%)": language_percentage
})

language_table.index = language_table.index.map({
    "0": "Not First Language",
    "1": "First Language"
})

# Create bar chart
ax = language_table["Number of Workers"].plot.bar(
    xlabel="English First Language",
    ylabel="Number of Workers",
    legend=False
)

# Add percentages above bars
for i, percentage in enumerate(language_table["Percentage (%)"]):
    ax.text(
        i,
        language_table["Number of Workers"].iloc[i],
        f"{percentage}%",
        ha="center",
        va="bottom"
    )

plt.title("Workers by First Language")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```
**What I changed** I used this code later for Q1-Q4 to guide my analysis, where I accidentally interpreted 0 as English and 1 as not English.

### 3.1 AI Statement: 

**AI Prompt:**
This is format of toxicity_annotations:
{'rev_id': '2232.0', 'worker_id': '723', 'toxicity': '0', 'toxicity_score': '0.0'}

I need all_annotators to merge and match the toxicity annotations with workers that are in the dataset: toxicity and like this new format that appends all the annotations that match worker_id to the all_annotators:
{'worker_id': '85', 'gender': 'female', 'english_first_language': '0', 'age_group': '18-30', 'education': 'bachelors', 'dataset': 'toxicity', 'unique_id': '1', 'annotation': {'rev_id': '2232.0', 'toxicity': '0', 'toxicity_score': '0.0'}}
**AI Output:**

```
for annotation in toxicity_labels:
    worker_id = annotation["worker_id"]

    # Store annotation fields without duplicating worker_id
    annotation_data = {
        "rev_id": annotation["rev_id"],
        "toxicity": annotation["toxicity"],
        "toxicity_score": annotation["toxicity_score"]
    }

    toxicity_by_worker.setdefault(worker_id, []).append(annotation_data)

# Merge annotations into all_annotators
for annotator in all_annotators:
    if annotator["dataset"] == "toxicity":
        annotator["annotation"] = toxicity_by_worker.get(
            annotator["worker_id"], []
        )


# Count all annotations attached to workers
total_matched = sum(
    len(annotator.get("annotation", []))
    for annotator in all_annotators
    if annotator["dataset"] == "toxicity"
)
```


**What I changed** I had to change the calculation so that it would accurate calculate the percentage.


## How to re-run
Open `hcde410-a2.ipynb` and run all cells (needs `requests`, `pandas`, `matplotlib`).

*Exercises and assignments for HCDE410: Human Data Interaction.*