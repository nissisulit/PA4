# PA#4

## Name: Nissi Aleichem B. Sulit
## Section: 2ECE-B
## Date Submitted: September 17, 2026

This Program Assignment demonstrates the use of Pandas for data wrangling and Matplotlib for data visualization. The ECE Board Exam 2 dataset was used to filter specific group of students, calculate average scores, summarize data by categories, and visualize the results using bar charts. The board2.xlsx was used for this Program Assignment.


```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the dataset
df = pd.read_excel("board2.xlsx")

# Calculate the Average of the four subjects
df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)

```

## Problem A. VISAYAS COMMUNICATION DATAFRAME
This program creates a DataFrame named VisComm containing students whose:

- ## Hometown is Visayas
- ## Track is Communication

The program retains only the Name, Gender, Math, Electronics, and Average. The resulting DataFrame and number of rows are then displayed. The VisComm DataFrame contains 5 students.
```python
VisComm = df[
 (df["Hometown"] == "Visayas") &
 (df["Track"] == "Communication")
][["Name", "Gender", "Math", "Electronics", "Average"]]

print("VISAYAS COMMUNICATION DATAFRAME")
display(VisComm)

print("Number of rows:", len(VisComm))
```

## Problem B. VISAYAS FEMALE DATAFRAME
The program creates a DataFrame named VisFemale containing students whose:

- ## Hometown is Visayas
- ## Gender is Female

The following columns are retained, but the GEAS is added, and the gender is now at the DataFrame. The program then displays only students whose average is at least 60 without changing the original VisFemale DataFrame.

```python
VisFemale = df[
   (df["Hometown"] == "Visayas") &
   (df["Gender"] == "Female")
][["Name", "Track", "GEAS", "Electronics", "Average"]]

print("\nVISAYAS FEMALE DATAFRAME")
display(VisFemale)

print("\nVISAYAS FEMALE WITH AVERAGE >= 60")
display(VisFemale[VisFemale["Average"] >= 60])

```

## Problem C. Category-Average Visualization
The program calculates the mean Average for each category of:

- ## Track
- ## Gender
- ## Hometown
The program also creates one figure containing three bar charts comparing the mean Average according to Track, Gender, and Hometown.
## a-b.
```python
# Mean Average by Track
track_mean = df.groupby("Track")["Average"].mean().reset_index()

# Mean Average by Gender
gender_mean = df.groupby("Gender")["Average"].mean().reset_index()

# Mean Average by Hometown
hometown_mean = df.groupby("Hometown")["Average"].mean().reset_index()

print("Mean Average by Track:")
display(track_mean)

print("Mean Average by Gender:")
display(gender_mean)

print("Mean Average by Hometown:")
display(hometown_mean)

```
## c.
```python
fig, axes = plt.subplots (1, 3, figsize=(15,5))

#The Mean Average by Track
axes[0].bar(track_mean['Track'], track_mean['Average'])
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average')
axes[0].tick_params(axis='x', rotation=30)

#The Mean Average by Gender
axes[1].bar(gender_mean['Gender'], gender_mean['Average'])
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average')

#The Mean Average by Hometown
axes[2].bar(hometown_mean['Hometown'], hometown_mean['Average'])
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average')

plt.tight_layout()
plt.show

```

## d. Interpretation

Based on the observed sample means:

- ## Track: Communication has the highest sample mean Average at 67.97.
- ## Gender: Male students have the highest sample mean Average at 67.18.
- ## Hometown: Luzon has the highest sample mean Average at 68.08.

These statements describe the observed dataset only. Differences in group means do not, by themselves, establish that a category causes higher board-exam scores.
