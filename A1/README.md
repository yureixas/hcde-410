#HCDE410
Files for HCDE410 - Assignment A1

Adapted from # cdsw-2020 https://wiki.communitydata.science/Seattle_open_data

# A1 — Working with Open Data

**Dataset:** Burke-Gilman Trail counter north of NE 70th St

**Source:** https://data.seattle.gov/Transportation/Burke-Gilman-Trail-north-of-NE-70th-St-Bicycle-Cou/2z5v-ecg8/about_data  *(pulled 2026-10-13)*

**License / terms of use:** Public Domain

**AI Statement (Detailed Notes under Answers):** 
- For Q1, I had help with AI to figure out how to plot 4 different lines and a specific range of time onto the graph.
- For Q2, I had help with AI to make 4 subplots that could show both cyclist and pedestrian activity.
- For Q3, I had help with AI to create a graph that could separate weekdays from weekends and show activity for cyclists and pedestrians.
- For Q4, I did not use AI

---

## Questions I asked

### **Q1. When is the trail busiest, and when is it quietest?**

- Decide what *busy* means to you first — a single hour? a stretch of the day? bikes and peds together, or separately? — and say why you chose that.

### **My Q1 answer:**

-*I decided to model when the trail is busiest by using four stretches of a day in 6-hour intervals to identify which stretch of the day is busiest. I combined bikes and pedestrians because they both contribute to how busy or how much traffic the trail has at a certain hour. With the graph, the hour when traffic is busiest is during the afternoon from 12pm-5pm, and when it is quietest during dawn from 0am-5am. This makes sense in context, because most people are sleeping from 0am-5am so they would not be on the trail, and most people would already be outside 12pm-5pm when the sun is still up, making it the busiest time to use the trail in comparison to the morning or evening.*

***AI Prompt**: How do I show 6-hour intervals on a plot using panda for jupyter notebook if I have by_hour = df.groundpy("hour")["people"].sum()*

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

***What I changed:** I labeled the intervals to show the corresponding hours so that it would be easier to understand the time the intervals take place in*

---
### **Q2. Do cyclists and pedestrians use the trail at different times of day?**

- Compare their hourly patterns. If they differ, what might explain it?

### **My Q2 answer:**

- *I split it up into 4 subplots to help visualize the comparisons of cyclists vs. pedestrians for each stretch of time and it seems there are a lot more cyclists using the trail throughout the day than pedestrians. There is an increase during the morning for cyclists, which continues to increase until the evening, while pedestrians increase during the morning but start to slightly decrease in the afternoon. My hypothesis on why they differ is that the Burke-Gillman trail is primarily used by cyclists throughout the day, and that some pedestrians only use the trail in the morning, but there could be other routes pedestrians are using to get home later in the day.*

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

- *Based on the graph, there is more traffic on the weekend compared to weekdays. The "commuting pattern" tells us that many cyclists use the trail for commuting on weekdays, due to the peak in activity during the morning and evening, with few pedestrians who use the trail for commuting. Additionally, the "commuting pattern" shows that more cyclists use the trail for fun on the weekends compared to weekdays because of the amount of sustained traffic in the afternoon, and pedestrian traffic also shows that pedestrians are using the trail for morning walks while cyclists tend to use it throughout the day. This would mean that the Burke-Gilman Trail is more popular among cyclists for recreational use on the weekends and is primarily used for commuting on the weekdays, while pedestrians use it recreationally only in the morning on weekends and barely use it on the weekdays.*

***AI Prompt:** How could I compare bikes and pedestrians by weekday vs. weekends by hour? There is a weekday variable that shows strings of the week *

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
***What I changed:** I adjusted the titles for the graphs to be more accurate and specific to what data is being shown in each plot so that it was easier to understand what is being graphed. It originally only wrote "Bike/Pedestrian Traffic by Hour" and didn't specify the year or the range of hours in the axes titles. I also removed the dots on each hour to make it look cleaner.* 

---
### **Q4. Direction and flow.**

- The counter records **north vs. south** separately. Are mornings mostly one direction and evenings the other? What would that tell you about who's using the trail and where they're heading?

### **My Q4 answer:**

- *Based on the graphs, on weekdays, a majority of traffic comes from cyclists using the trail to travel north in the morning and travel south in the evening, while pedestrians travel both directions in the morning and evening. On weekends, both directions of activity match up with Q3, where cyclists use it throughout the day, and pedestrians use it in the morning. The map of the Burke-Gilman trail shows that the south is near the University of Washington and the north goes all the way to Bothell, where there are more workplace buildings. I hypothesize that cyclists who live near the University of Washington are the majority using the trail to commute to work, with few pedestrians using the trail on weekdays, while many cyclists in general use the trail for fun throughout the day, with pedestrians using the trail for morning walks on the weekends; this is also supported by my previous answers to Q1-Q3.*

***AI Prompt**: No AI prompt was used for this question, I rewrote the code from previous questions to better fit the question here*

---
### **Limitations or bias of the data**

- *One bias this dataset could have that could mislead someone is if the people on the trail went back and forth on the trail multiple times. This could skew the data, making counts of cyclists or pedestrians higher than they were in reality. This would mislead my hypothesis about more cyclists using the trail on the weekends than weekdays.*

---
## How to re-run
Open `A1.ipynb` and run all cells (needs `requests`, `pandas`, `matplotlib`).