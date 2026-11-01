# A3 — Watching the Machine

A notebook for HCDE 410 Assignment 3, in which **AI is the subject of study, not the author.** I investigated the reliability and reproducibility of large language models (LLMs) through a small mixed-methods study, then reflected on what it means for trustworthy research.

## What this notebook is

`A3_watching_the_machine_starter.ipynb` contains:

1. **Prior practice** — a short written reflection on how I currently used LLMs.
2. **Reproducibility probe** — I gave AI the same prompt **3 times in one model for ChatGPT** and **once in a second model in Claude (Sonnet 5.5)**, and loged every run verbatim in a spreadsheet which includes prompt, model, version, timestamp, output, verified, notes), exported as `a3_runs.csv` and loaded into a pandas DataFrame. A short helper cell summarizes the log (run count, distinct outputs, verification tally).
3. **Observation** — I watched one person do a comparable task with ChatGPT (with permission) by running the same prompt I gave in the reproducibility probe, took timestamped field notes, and grouped them into themes in a second spreadsheet, exported as `a3_codes.csv`.
4. **Synthesis & reflection** — I brought the probe and observation together into one account about trustworthy, reproducible research and what I will change in my own AI use.
5. **Competencies demonstrated:** I demonstrated reproducible analysis by examining the accuracy of AI-generated code in part 2 and understanding the importance of verifying results against the original dataset and documenting the steps needed to reproduce the analysis through observing my participant in part 3.
**AI Statement:** I only used AI to help me write a segment in my AI check (`Checking_AI_Responses.jpynb`) to help me strip the string from my csv file into numerical values. Other than that, the use of AI was strictly used based on the assignment requirements.



## How to run

Open `A3_watching_the_machine_starter.ipynb` and run the cells. The only dependency is:

- `pandas`

The notebook does not fetch external data. It loads two CSV files you create from your own runs and field notes: `a3_runs.csv` and `a3_codes.csv`. Header-only templates of both are included in this folder; open them in Google Sheets or Excel, fill them in, download as CSV, and upload them here with the same names.


Open `Checking_AI_Responses.ipynb` and run the cells. The only dependency is:

- `pandas`

The notebook does not fetch external data. It loads two CSV files from "My Datasets" folder: `World_Bank_CO2_RawData.tsv` and `World_Bank_CO2_Cleaned.tsv`. 

### Datasets:
**Data from: DataBank World CO2 Emissions**
- `World_Bank_CO2_RawData.tsv` : This dataset contains raw data from the source
- `World_Bank_CO2_Cleaned.tsv`: This dataset contains cleaned data from the source
- 
**Source:** This data was taken from [the dataset from DataBank World CO2 Emissions](https://databank.worldbank.org/metadataglossary/millennium-development-goals/series/EN.ATM.CO2E.KT)
**License / terms of use:** Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)
**How I cleaned the data:** For `World_Bank_CO2_Cleaned.tsv`, I categorized each country in the dataset to a region in the world and examined CO2 Emissions from 1960 to 2010

### Files in My Datasets Folder:
Outside of `World_Bank_CO2_RawData.tsv` and `World_Bank_CO2_Cleaned.tsv`, I included outputs that the AI had written in the code. These files are purely for reference to see what the AI wrote and *not used in my analysis or for the A3 notebook*.


# Responses 

## 1. Your prior practice

*How do you currently use LLMs in your own work, and what do you assume about their reliability? A few sentences.*

I currently use LLMs to help with getting resources, such as for coding assignments, and also asking it questions about things I am confused about, such as reflecting on topics (for example, philosophy). For code, I assume that the responses they use will work or are accurate but sometimes the code it generates can be wrong and not what I want it to do. For questions, I don't believe it is reliable but helps me find information quicker than a search. I do try to identify in the output any parts that might not be true and fact checking it, but there may be times that I am not able to identify just by looking at the wording if what it said was true.

## 2. Reproducibility Probe

### Prompt for the LLMs:
I want you to give me the full code that uses pandas (assuming I have it set up the file name to be World_Bank_CO2_RawData.tsv) to help me compute the CO2 (kt) emissions by region (grouping countries in the dataset by region first) in the year 2010 in a table, including percentages and also give me code for a bar chart showcasing this.
The dataset does NOT contain a Region column. Create one in the code by assigning each country to its appropriate World Bank geographic region, the lists these fall under are Country Name and Country Code This data is from the World Bank Database on Carbon Emissions if you need reference: https://databank.worldbank.org/source/millennium-development-goals/Series/EN.ATM.CO2E.KT 

**What varied, and what held up?** *Summarize the divergence across runs and models, and how you verified each answer against ground truth.*

To verify each run, I wrote my own code that shows a table and also a bar graph which uses a dataset that I cleaned up prior and then checked each value against the AI's response. 

For run 1 and 3 with ChatGPT, it had the same exact outcome where it included an aggregates category which messed up the calculation for percentages and also had a 170k different for Middle East and North Africa when I verified it against my own data. 

For run 2 with ChatGPT, I couldn't run it at all because it threw an error which meant I couldn't check. 

For run 4 with Claude, it had the exact same percentage calculations as my own answer when I went to verify and basically the same sum for CO2 (kt). Based on this, what varied across runs was accuracy of the code and calculating the data and what held up was identifying and writing down each region in the table.

## 3. Observation

I tested with one participant who used ChatGPT (Unknown version) who input the same exact prompt used in part 2.

### Field notes
- **10:38** _Input the prompt, ChatGPT (Unknown Version) took 19 seconds, they said the output looks good_
- **10:40** _After testing the code, they realized it didn't work so they went back to ask "the code doesn't seem to be working, could you revise it?", which took 12 seconds_
- **10:41** _After asking if they trust the code, they said they do because the response at the end says "if this code doesn't work try this and run the output"_
- **10:43** _They decided to test out the output test lines given by the AI by feeding it back into ChatGPT ("Could you run these three lines seperately tell if it looks good?")_
- **10:43** _ChatGPT couldn't run it because it doesn't have the actual TSV file in the prompt_
- **10:45** _They finally decided to check the actual code, realizing there was another error_
- **10:45** _They pasted the error directly from the terminal and asked "I plugged this into Jupyter and it gave me an error? What's up with that"_
- **10:46** _ChatGPT responded saying "no worries!" to reassure them but the output doesn't tell them why and they still don't understand why they are having errors_
- **10:48** _I realized I had messed up the prompt file location and helped fix it so it ran the output_
- **10:50** _After seeing the output, they were confused why the graph was showing a bar for aggregates and asked ChatGPT to specify "why aggregates is seperate from other regions?"_
- **10:51** _After 11 seconds, ChatGPT gave a new output explaining it as combined statistics from the file but they were still confused what it meant_
- **10:53** _They looked back at the original prompt to remind themselves what they're supposed to look for in the output as they felt they were doing something wrong instead of ChatGPT_
- **10:56** _They finally asked ChatGPT "Can you not include aggregates and just do it by regions?", and the output took 20 seconds_
- **10:56** _They immediately trusted the code without verifying at first but then realized the formatting was wrong and decided to ask ChatGPT to turn the output into .txt but the output included extra headers instead. They said this was not what they wanted_
- **11:03** _After troubleshooting, they told ChatGPT that they wanted the original revised code from earlier again_
- **11:05** _The code given by ChatGPT was still having an issue passing the code, and they began to actually read the code to see what was happening but couldn't fully understand_
- **11:07** _They made a typo during the prompt_
- **11:12** _They gave ChatGPT the whole error given and asked it to revise, they were feeling confident that the code was going to work_
- **11:13** _After pasting the new code, they noticed that South America, North Africa, and other important regions were missing_
- **11:16** _They asked ChatGPT "Can you include the missing regions? Like South America and Africa or Australia"_
- **11:16** _ChatGPT gave an explanation of the regions and proposed 12 regions to include in the code, which they asked ChatGPT to include_
- **11:17** _They said they were getting frustrated with the AI and after 30 seconds, ChatGPT gave a new code output_
- **11:18** _They looked at the result and said they were happy and looks acceptable, I asked if they trusted it and they decided to ask ChatGPT to check and verify with sources"_
- **11:18** _It took ChatGPT 35 seconds and said it was correct, so they felt they trusted the output_
- **11:20** _After running the code, they didn't see any errors by checking the categories but didn't actually check to compare the values were correct_
- **11:21** _They felt that ChatGPT made it feel easy to make the code and told me that ChatGPT could do my initial code to verify the outputs faster_
- **11:22** _They compared my bar chart's layout to their output and felt that they AI layout one was easier to digest for them._

I coded these observations into themes in `a3_codes.csv`, such as prompt repair, over-trust, checking, skipped verification, confusion, and frustration.

## 4. Synthesis & reflection

*Bring the probe and the observation together into one account. What does this mean for trustworthy, reproducible research — and what will you change about how you use and verify AI in your own work?*

_After doing both the probe and observation, I learned that AI, particularly ChatGPT, was not very good at generating accurate code for my prompt on calculating and visualizing CO2 emissions by geographical region in 2010. ChatGPT was inaccurate for each of my three runs, giving me wrong calculations and code that didn't work. My participant, who also used ChatGPT, needed seven prompt repairs before they felt the result was correct, and reported feeling confused and frustrated during the observation. This shows that that the AI output should not automatically be considered trustworthy, even when it seems correct because the accuracy of the results needs to be verified manually._

_For trustworthy and reproducible research, researchers should not rely entirely on AI or blindly trust its output. They need to understand the task, verify the results against the original data, and document their process with using AI so that others can follow and reproduce their work. Although AI can be helpful for smaller tasks, I learned that relying on it to generate everything from my prompt produced inaccurate results and required additional work and time to check and repair them. I believe that writing the code manually might have been more efficient for me in this case._

_In the future, I will ask AI to identify the sources and reasoning behind its answers, then independently verify its output against the original dataset. I will also pay closer attention to documenting my prompts and changes so that I can explain how I reached my results for reproducibility. I believe it is my responsiblility to transparently show the process of my work to uphold trustworthy and reproducible research, even when AI is helping me._

# Checking_AI_Response.jpynb

This notebook was created to check if the responses AI gave me were correct based on the World_Bank_CO2_Cleaned.tsv file. Each AI code runs the World_Bank_CO2_RawData.tsv file. This notebook includes my original code to verify all runs and the AI runs from part 2 to verify the responses and runs from part 3 that my participant got outputs for.

# Usage of AI

# 2 - 3
AI was used only based on the prompt guidelines.

## Checking_AI_Response.jpynb

**AI prompt**: How do I make a data frame in panda only resspond to a year and then format the value from 'CO2 (kt)' to not be a string and instead a number

**AI Response**:
```
# Filter for 2010
df_2010 = df[df["Year"] == "2010"].copy()

# Convert CO2 values from strings to numbers
df_2010["CO2 (kt)"] = pd.to_numeric(
    df_2010["CO2 (kt)"].str.replace(",", ""),
    errors="coerce"
)
```
**What I did:** I used this code to help me change the values from the CO2 (kt) column from strings to numerical values so that I could sum it later. This was used to help me verify the code from the runs in part 2.


## License

Released under the MIT License — see [`LICENSE`](./LICENSE).
