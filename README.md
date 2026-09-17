# ECE2112 - Experiment 4

This repository contains my solution for **Experiment 4** in ECE2112 - Advanced Computer Programming and Algorithms.

The activity focuses on using **Pandas** for filtering and analyzing student data, and **Matplotlib** for visualizing the average grades based on different categories.

## Files

* `SAMOY_PA4.ipynb` - Jupyter Notebook containing the Python codes
* `board2.xlsx` - Dataset used in the activity
* `README.md` - Documentation of the program

---

## Importing Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
```

`pandas` is imported as `pd` for handling and analyzing the dataset, while `matplotlib.pyplot` is imported as `plt` for creating graphs.

---

## Loading the Dataset

```python
df = pd.read_excel('board2.xlsx')
df
```

`pd.read_excel()` reads the Excel file `board2.xlsx` and stores it in the DataFrame `df`.

---

## Computing the Average Grade

```python
df['Average'] = df[['Math', 'GEAS', 'Electronics', 'Communication']].mean(axis=1)
```

A new column called `Average` is created.

`.mean(axis=1)` calculates the average of the **Math, GEAS, Electronics, and Communication** grades for each student.

---

## A. Visayas Communication DataFrame

```python
visayas_comm = df.loc[
    (df['Hometown'] == 'Visayas') &
    (df['Track'] == 'Communication')
]
```

`.loc[]` is used to filter students who:

* are from **Visayas**
* belong to the **Communication** track

The `&` operator means that both conditions must be true.

```python
VisComm = pd.DataFrame(
    visayas_comm,
    columns=['Name', 'Gender', 'Math', 'Electronics', 'Average']
)
```

A new DataFrame called `VisComm` is created containing only the required columns.

```python
print("Number of rows:", len(VisComm))
```

`len()` determines how many students are included in the filtered DataFrame.

---

## B. Visayas Female DataFrame

```python
visayas_female = df.loc[
    (df['Hometown'] == 'Visayas') &
    (df['Gender'] == 'Female')
]
```

This filters the dataset to include only **female students from Visayas**.

```python
VisFemale = pd.DataFrame(
    visayas_female,
    columns=['Name', 'Track', 'GEAS', 'Electronics', 'Average']
)
```

`VisFemale` contains only the selected columns required for the activity.

### Filtering Average Grades

```python
visfemale_60 = VisFemale.loc[VisFemale['Average'] >= 60]
```

This selects only students whose average grade is **60 or higher**.

The `>=` operator means **greater than or equal to**.

---

## C. Category-Average Visualization

### Average per Track

```python
track_average = df.pivot_table(
    index=['Track'],
    values='Average'
).reset_index()
```

`pivot_table()` groups the students according to their track and calculates the mean of their `Average` grades.

`.reset_index()` converts the grouped index back into a regular column.

The same process is used for gender and hometown:

```python
gender_average = df.pivot_table(
    index=['Gender'],
    values='Average'
).reset_index()
```

```python
hometown_average = df.pivot_table(
    index=['Hometown'],
    values='Average'
).reset_index()
```

These calculate the average grades based on **Gender** and **Hometown**.

---

## Creating the Bar Graphs

```python
plt.figure(figsize=(20,5))
```

This creates the main figure and sets its size.

```python
plt.subplot(1,3,1)
```

`subplot()` divides the figure into **1 row and 3 columns**, allowing three graphs to be displayed side by side.

The graphs compare:

1. Average Grades per Track
2. Average Grades per Gender
3. Average Grades per Hometown

```python
plt.bar(track_average['Track'], track_average['Average'])
```

`plt.bar()` creates a bar graph using the category as the x-axis and its mean average grade as the y-axis.

```python
plt.title()
plt.xlabel()
plt.ylabel()
```

These functions add the graph title and axis labels.

```python
plt.tight_layout()
plt.show()
```

`plt.tight_layout()` adjusts the spacing between the graphs, while `plt.show()` displays the final visualization.

---

## Finding the Highest Averages

```python
highest_track = track_average.loc[[track_average['Average'].idxmax()]]
```

`.idxmax()` finds the index of the highest value in the `Average` column.

`.loc[]` then retrieves the corresponding row.

The same method is used to determine the:

```python
highest_gender
highest_hometown
```

Finally, the results are displayed using `print()`.

---

## Concepts Used

The activity uses the following Python concepts:

* `pd.read_excel()`
* Pandas DataFrames
* `.mean()`
* `.loc[]`
* Conditional filtering
* `pd.DataFrame()`
* `pivot_table()`
* `.reset_index()`
* `.idxmax()`
* Matplotlib
* Bar graphs
* Subplots

---

## Requirements

The program requires:

```text
Python
Pandas
Matplotlib
Jupyter Notebook
```

The required libraries can be installed using:

```bash
pip install pandas matplotlib openpyxl
```

The `board2.xlsx` file should also be in the same directory as the notebook.

---

## Summary

Experiment 4 demonstrates the use of Pandas for filtering and analyzing student grade data. It also uses Matplotlib to compare the mean average grades according to track, gender, and hometown and identifies which category has the highest average.
