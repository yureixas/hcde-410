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

4713 workers (81.53%) reported English as their first language, while 1068 workers (18.47%) did not. 

**Q3. What is the distribution of these workers by age group?**

The largest age group reported was 18–30, with 2,911 workers (50.35%), followed by ages 30–45 with 2,078 (35.95%), ages 45–60 with 514 (8.89%), and under 18 with 116 (2.01%). The smallest age group reported was over-60, with 50 workers (0.86%). 112 workers (1.94%) also had a blank age-group value.

**Q4. What is the distribution of these workers by education level?**

The most common education level reported was a bachelor's degree, representing 2,303 workers (39.84%), followed by high school with 1,657 (28.66%), master's degrees with 931 (16.10%), professional degrees with 684 (11.83%), some education with 141 (2.44%), and doctorate degrees with 61 (1.06%). The least common category reported was “none,” with 4 workers (0.07%), indicating no education level.

## 2.2 

**Q5.** Analyze all_annotators in Sheets or Jupyter: Do any of the fields in this dataset have missing data? If so, which fields, and what % of the rows contain missing values?

- The dataset contains a missing field in the age group category, where 112 workers have a missing age group value (1.94% of the rows). Earlier, I wasn't sure what this missing field meant, even when discussing the distribution in Q3. Missing field information like that can affect the analysis of the annotator distribution because it can skew the percentage and make the analysis inaccurate.

**Q6.** Build a version of the all_annotators dataset *without removing duplicates*, then re-run the summary statistics from questions 1-4. How have these summary statistics changed?

- Including both the aggression and attack workers changed the percentage values of the distribution, as workers' demographic data are counted and represented twice in the annotator dataset. The all_annotators dataset originally contained only 5,781 workers but has now increased to 7,971 workers. As a result, some percentages slightly changed, such as women going from 36.38% to 36.92% or the age group of 18-30 going from 50.35% to 49.68%. Although these changes were very slight, this new dataset could still be misleading, as the distribution of the overall annotator population is inaccurate and shows how duplicated data could skew descriptive statistics, leading someone to make incorrect conclusions.


**Q7.** In general, how do the demographics of these workers compare to those of English-speaking internet users overall? Why would it matter if the worker demographics don't match the demographics of the intended end users of the Perspective API?

- I believe that the demographics of the annotators do not fully represent English-speaking internet users overall. [Statistica](https://www.statista.com/chart/26884/most-spoken-languages-online-offline/?srsltid=AYCX9vIjS0PpfV6O0S05G9qWuK-vcdXdM4srElkStTpXWKt-6Z8wBy-N) reported that English accounts for 51.2% of the language used online, but the majority of the annotators (~80%) reported English as their first language. This matters because it could imply that this dataset has more representation of English content than actual content online from other languages, making this dataset less accurate in evaluating languages other than English, as the annotators possibly evaluated English hostile speech more than any other language. If this dataset is intended to detect hostile speech across the internet, the training data should incorporate more data from different languages, otherwise, this dataset underrepresents languages other than English when evaluating hostile speech.


**Q8.** Given what you now know about the Wikipedia Talk Corpus, what issues might arise if it was used to train a machine learning-driven "hostile speech detector" that could be used on any website or social media platform?

- I believe that if these datasets were used to train a machine learning-driven "hostile speech detector" for different websites and platforms, the model might not accurately identify hostile speech in languages other than English. Because the majority of annotators reported English as their first language, their judgments and evaluation of hostile speech may not fully reflect or identify how hostility is expressed or interpreted in other languages and cultural contexts. This would be concerning as it could make the detector less reliable and unfair to users from underrepresented languages that were not evaluated equally in the dataset.

## 3.1

#### Code questions
- **Q9.** What % of *workers* who labelled the toxicity dataset do we have demographic data for?
- **Q10.** What % of the *comments* in the toxicity dataset were labelled by male vs. female-identified workers?
- **Q11.** What % of the *comments* in the toxicity dataset were labelled by people for whom English is NOT their first language?
- **Q12.** Based on your findings from questions 9-11, how might this dataset present a biased view of "toxicity"? How would you expect such biases to impact how the Perspective API performs? 


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

**What I changed** I adjusted this code so that it could be used for each bar chart when necessary (Like if there are more than 5 categories, I would make the bar chart horizontal)

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

**What I changed** I adjusted this code to correctly label the bar chart, as 0 as not English wasn't accurate. I also tweaked the code for that it was showing both the table and bar chart.

*Exercises and assignments for HCDE410: Human Data Interaction. Everything here is a work in progress unless otherwise noted :)*
