# HCDE410

# A1 — Working with Open Data

**Dataset:** Burke-Gilman Trail counter north of NE 70th St

**Source:** https://data.seattle.gov/Transportation/Burke-Gilman-Trail-north-of-NE-70th-St-Bicycle-Cou/2z5v-ecg8/about_data  *(pulled 2026-10-13)*

**License / terms of use:** Public Domain

**AI Statement (Detailed Notes under Answers):** 
- **Q1:** I had help with AI to figure out how to plot 4 different lines and a specific range of time onto the graph.
- **Q2:** I had help with AI to make 4 subplots that could show both cyclist and pedestrian activity.
- **Q3:** I had help with AI to create a graph that could separate weekdays from weekends and show activity for cyclists and pedestrians.
- **Q4**: I did not use AI

---

## Questions I asked

### **Q1. When is the trail busiest, and when is it quietest?**

-Decide what *busy* means to you first — a single hour? a stretch of the day? bikes and peds together, or separately? — and say why you chose that.

### **My Q1 answer:**

- *I divided the day into four six-hour periods to compare total traffic at different times of day and combined bike and pedestrian counts because both contribute to overall traffic use. Based on the graph, the afternoon (12pm-5pm) has the highest total traffic, while dawn(12 AM-5AM) has the lowest. I believe this makes sense in context because most people are sleeping at dawn, so they would not be on the trail, and most people would already be outside during the afternoon when the sun is still up, making it a more convenient time to use the trail in comparison to the morning or evening.*

***AI Prompt**: How do I show 6-hour intervals on a plot using panda for jupyter notebook if I have by_hour = df.groundpy("hour")["people"].sum() Should I use a bar chart to better interpret this?* 

***AI Original Output:***

```
df["people"] = df["bikes"] + df["peds"]

by_hour = df.groupby("hour")["people"].sum()

by_period = pd.DataFrame({
    "Dawn (12am–5am)": by_hour.loc[0:5].values,
    "Morning (6am–11am)": by_hour.loc[6:11].values,
    "Afternoon (12pm–5pm)": by_hour.loc[12:17].values,
    "Evening (6pm–11pm)": by_hour.loc[18:23].values
}, index=range(1, 7))

by_period.plot(figsize=(11, 5))

plt.title("Burke-Gilman Traffic by 6-Hour Interval (2019)")
plt.xlabel("Hour within each 6-hour interval (1–6)")
plt.ylabel("Total count")
plt.xticks(range(1, 7))
plt.show()
```

Yeah, I think a bar chart is better for Q1 if your goal is to identify which six-hour period has the most total trail traffic. It directly compares the total counts across the four periods, whereas your original line graph shows hourly patterns within each period

```
df["people"] = df["bikes"] + df["peds"]

by_hour = df.groupby("hour")["people"].sum()

periods = {
    "Dawn (12 AM–5 AM)": (0, 5),
    "Morning (6 AM–11 AM)": (6, 11),
    "Afternoon (12 PM–5 PM)": (12, 17),
    "Evening (6 PM–11 PM)": (18, 23)
}

period_totals = {
    name: by_hour.loc[start:end].sum()
    for name, (start, end) in periods.items()
}

pd.Series(period_totals).plot(kind="bar", figsize=(10, 5))
plt.title("Total Burke-Gilman Trail Traffic by Time of Day (2019)")
plt.xlabel("Time of Day")
plt.ylabel("Total Bike and Pedestrian Count")
plt.xticks(rotation=0)
plt.show()
```

***What I changed:** I changed this graph two times, from a line chart to a bar chart to better show the timeframe with most traffic. I originally labeled the intervals to show the corresponding hours so that it would be easier to understand the time the intervals take place in and then for the second version I labeled the y-axis to show that it was a total count*

---
### **Q2. Do cyclists and pedestrians use the trail at different times of day?**

- Compare their hourly patterns. If they differ, what might explain it?

### **My Q2 answer:**

- *The graphs show differences in the hourly patterns of cyclists and pedestrians, where cyclists have higher recorded counts than pedestrians. Cyclist counts decrease during the morning and continue to rise into the evening, while pedestrian counts increase in the morning and decline during the afternoon. One possible explanation for this pattern could be that cyclists and pedestrians use the trail for different purposes; for example, pedestrians may only use the trail in the morning, but use other routes to get home later in the day. However, the data alone can't exactly show why these patterns occur.*

***AI Prompt:** Based on previous prompt, show me how I could split these periods for "bike" vs "peds" to make 4 plots and show each interval of time. How can I make the x ticks correlate with the hour? How do I make the y-axis start from 0?*

***AI Original Output:***
```
# Group bikes and pedestrians by hour
by_bikes = df.groupby("hour")["bikes"].sum()
by_peds = df.groupby("hour")["peds"].sum()

# Split into four 6-hour intervals
periods = {
    "Dawn (12 AM–5 AM)": (by_bikes.loc[0:5], by_peds.loc[0:5]),
    "Morning (6 AM–11 AM)": (by_bikes.loc[6:11], by_peds.loc[6:11]),
    "Afternoon (12 PM–5 PM)": (by_bikes.loc[12:17], by_peds.loc[12:17]),
    "Evening (6 PM–11 PM)": (by_bikes.loc[18:23], by_peds.loc[18:23])
}

# Create four plots in a 2x2 grid
fig, axes = plt.subplots(2, 2, figsize=(12, 8))

for ax, (title, (bikes, peds)) in zip(axes.flat, periods.items()):
    # Use positions 1–6 for each interval
    ax.plot(range(1, 7), bikes.values, label="Bikes")
    ax.plot(range(1, 7), peds.values, label="Pedestrians")

    ax.set_title(title)
    ax.set_xlabel("Hour within 6-hour interval (1–6)")
    ax.set_ylabel("Total count in 2019")
    ax.set_ylim(bottom=0)
    ax.set_xticks(range(1, 7))
    ax.legend()

fig.suptitle("Burke-Gilman Bike vs. Pedestrian Traffic (2019)")
plt.tight_layout()
plt.show()
```

***What I changed:** I adjusted the titles to accurately describe each line in the chart and also added the correct hours to the x-axis to show the range. I also added the upper range of the data to give it a better range.*

---
### **Q3. Commuting or recreation?**

- Is there evidence people use the Burke-Gilman to *commute*, not just for fun? Compare **weekdays vs. weekends**, and maybe morning vs. evening. Define what a "commuting pattern" would look like in the data, then say whether you see it.

### **My Q3 answer:**

- *To define a "commuting pattern", I looked at morning and evening peaks on weekdays for cyclists and lower amount of traffic from pedestrians as possible evidence of commuting to work. Higher, sustained daytime traffic on weekends for cyclists and a morning peak for pedestrians may suggest recreational use as more traffic is recorded. These "commuting" patterns could indicate that people use the trail for different purposes throughout the week, and I hypothesize that higher activity is correlated with more available free time, making recreational use more likely, while lower sustained activity on weekdays shows how people use the trail during their workdays. However, this is only a hypothesis because the dataset doesn't record why people use the trail or where they're going.*

***AI Prompt:** How could I compare bikes and pedestrians by weekday vs. weekends by hour? There is a weekday variable that shows strings of the week.*

***AI Original Output:***
```
# Separate weekdays and weekends
weekdays = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
weekends = ["Saturday", "Sunday"]

weekday_data = df[df["weekday"].isin(weekdays)]
weekend_data = df[df["weekday"].isin(weekends)]

# Group by hour and calculate average traffic per day of the week
bikes_weekday = weekday_data.groupby(["weekday", "hour"])["bikes"].sum().groupby("hour").mean()
bikes_weekend = weekend_data.groupby(["weekday", "hour"])["bikes"].sum().groupby("hour").mean()

peds_weekday = weekday_data.groupby(["weekday", "hour"])["peds"].sum().groupby("hour").mean()
peds_weekend = weekend_data.groupby(["weekday", "hour"])["peds"].sum().groupby("hour").mean()

# Create two plots
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

axes[0].plot(bikes_weekday.index, bikes_weekday.values, marker="o", label="Weekdays")
axes[0].plot(bikes_weekend.index, bikes_weekend.values, marker="o", label="Weekends")
axes[0].set_title("Bike Traffic by Hour")
axes[0].set_xlabel("Hour of Day")
axes[0].set_ylabel("Average Count")
axes[0].set_xticks(range(24))
axes[0].legend()

axes[1].plot(peds_weekday.index, peds_weekday.values, marker="o", label="Weekdays")
axes[1].plot(peds_weekend.index, peds_weekend.values, marker="o", label="Weekends")
axes[1].set_title("Pedestrian Traffic by Hour")
axes[1].set_xlabel("Hour of Day")
axes[1].set_ylabel("Average Count")
axes[1].set_xticks(range(24))
axes[1].legend()

fig.suptitle("Average Bike and Pedestrian Traffic by Hour: Weekdays vs. Weekends (2019)")
plt.tight_layout()
plt.show()
```
***What I changed:** I adjusted the titles for the graphs to be more accurate and specific to what data is being shown in each plot so that it was easier to understand what is being graphed. It originally only wrote "Bike/Pedestrian Traffic by Hour" and didn't specify the year or the range of hours in the axes titles. I also corrected the code to accurately calculate the mean as the AI wrote it wrong*

---
### **Q4. Direction and flow.**

- The counter records **north vs. south** separately. Are mornings mostly one direction and evenings the other? What would that tell you about who's using the trail and where they're heading?

### **My Q4 answer:**

- *Some patterns that emerged from the graphs are that, on weekdays, most traffic comes from cyclists, who appear to travel north in the morning and south in the evening. On weekends, cyclist traffic in both directions appears to be distributed throughout the day, while pedestrian traffic in both directions peaks in the morning which are consistent with some of the differences in trail use I observed in Q3. When looking at the map of the Burke-Gilman Trail, the southern section is near the University of Washington, while the trail extends north toward Bothell, where there are workplace buildings. Based on this context, I hypothesize that some cyclists may use the trail to commute to work on weekdays, with the direction of travel potentially reflecting their commute and on weekends, pedestrians may be using these paths for morning recreational walks. These hypotheses are consistent with my previous observations in Q1–Q3, but the data does not explicitly show or tell where people are going or why they use the trail and if my assumptions from the map match up.*


***AI Prompt**: No AI prompt was used for this question, I rewrote the code from previous questions to better fit the question here*

---
### **Limitations or bias of the data**

- *One bias this dataset is that the counters only record passages near the cameras rather than individuals. This could mislead someone if people using the trail went back and forth multiple times. This could affect the interpretations of the data, particularly trail use and busiest hours, making counts of cyclists or pedestrians higher than they were in reality and would mislead my hypothesis about more cyclists using the trail on the weekends than weekdays. Another limitation this dataset has is that it does not record the purposes of travel, so the motivation behind traffic can only be predicted by the patterns rather than insights*

---
## How to re-run
Open `A1.ipynb` and run all cells (needs `requests`, `pandas`, `matplotlib`).