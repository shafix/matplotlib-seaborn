# matplotlib-seaborn
Some graph examples of mathplotlib and seaborn

# Matplotlib - Bar Chart with Error
```
from matplotlib import pyplot as plt

past_years_averages = [82, 84, 83, 86, 74, 84, 90] # Y values
years_range = range(len(years)) # X range
years = [2000, 2001, 2002, 2003, 2004, 2005, 2006] # X labels
error = [1.5, 2.1, 1.2, 3.2, 2.3, 1.7, 2.4] # Error sizes for each bar
# error = 2 # Error can also be static for all bars!

plt.figure(figsize=(10, 8)) # 10x8 figure

plt.bar(
  years_range,         # X
  past_years_averages, # Y
  yerr = error,        # Assign the error bar heights
  capsize = 5 )        # Error cap size

# Zoom in view
plt.axis([-0.5, 6.5, 70, 95]) # Xmin, Xmax, Ymin, Ymax

# Creating axes object for assigning tick data
ax = plt.subplot()
ax.set_xticks(range(len(years)))
ax.set_xticklabels(years, rotation=30)

# Labeling the axes and the graph itself
plt.xlabel('Year')
plt.ylabel('Test average')
plt.title('Final Exam Averages')

# Show the graph
plt.show()

# Save the graph to a file
plt.savefig('my_bar_chart.png')
```

# Matplotlib - Side By Side Bars (barchart)
```
from matplotlib import pyplot as plt

# Data
unit_topics = ['Limits', 'Derivatives', 'Integrals', 'Diff Eq', 'Applications'] # X Labels
middle_school_a = [80, 85, 84, 83, 86] # Y values for 1st bar
middle_school_b = [73, 78, 77, 82, 86] # Y values for 2nd bar

# Function for determining the bar positions
def create_x(t, n, d, w):
    return [t*x + w*n for x in range(d)]
# t - Number of datasets (ex 2)
# n - Nr of this data set (ex 1st out of 2)
# d - Number of sets of bars
# w - Width of each bar

school_a_x = create_x(2, 1, 5, 0.8) # X positions for 1st bar
school_b_x = create_x(2, 2, 5, 0.8) # X positions for 2nd bar

plt.figure(figsize=(10, 8)) # 10x8 figure

# Plot the bars
plt.bar(
  school_a_x,              # X 
  middle_school_a,         # Y
  label='Middle School A') # Label for legend
plt.bar(
  school_b_x,              # X  
  middle_school_b,         # Y 
  label='Middle School B') # Label for legend

# Calculate the X tick positions on the X axis (between the bars)
middle_x = [ (a + b) / 2.0 for a, b in zip(school_a_x, school_b_x)]

# Create axes object for putting ticks
ax = plt.subplot()
ax.set_xticks(middle_x) # Put X ticks between bars
ax.set_xticklabels(unit_topics, rotation=30) # Label the X ticks and turn 30 degrees

plt.legend() # Show the legend

# Graph and axis labesl
plt.xlabel('Unit')
plt.ylabel('Test Average')
plt.title('Test Averages on Different Units')

# Show the graph
plt.show()

# Save figure/graph to file
plt.savefig('my_side_by_side.png')
```

# Matplotlib - Stacked Bars (barchart)
```
from matplotlib import pyplot as plt
import numpy as np

# Data
unit_topics = ['Limits', 'Derivatives', 'Integrals', 'Diff Eq', 'Applications'] # X labels
x = range(len(unit_topics)) # X range
As = [6, 3, 4, 3, 5] # Y section 1 (lowest)
Bs = [8, 12, 8, 9, 10] # Y section 2
Cs = [13, 12, 15, 13, 14] # Y section 3
Ds = [2, 3, 3, 2, 1] # Y section 4
Fs = [1, 0, 0, 3, 0] # Y section 5 (highest)

# Calculate the bottoms of each section of the bar
b_bottom = As
c_bottom = np.add(As, Bs)
d_bottom = np.add(c_bottom, Cs)
f_bottom = np.add(d_bottom, Ds)

# 10x8 figure
plt.figure(figsize=(10, 8)) 

# Plot section 1
plt.bar(
  x, 
  As,            
  label = 'A') 

# Plot section 2
plt.bar(
  x, 
  Bs,            
  label = 'B',
  bottom=b_bottom)

# Plot section 3
plt.bar(
  x, 
  Cs,            
  label = 'C',
  bottom=c_bottom)

# Plot section 4
plt.bar(
  x, 
  Ds,            
  label = 'D',
  bottom=d_bottom)

# Plot section 5
plt.bar(
  x, 
  Fs,            
  label = 'F',
  bottom=f_bottom)

# Grab axes and set ticks
ax = plt.subplot()
ax.set_xticks(range(len(unit_topics))) # X tick positions
ax.set_xticklabels(unit_topics, rotation=30) # X tick labels

# Graph and exis labels
plt.xlabel('Unit')
plt.ylabel('Number of Students')
plt.title('Grade distribution')

# Show graph
plt.show()

# Save graph/figure to file
plt.savefig('my_stacked_bar.png')
```

# Matplotlib - Two Histograms on a Plot
```
from matplotlib import pyplot as plt

# Data
exam_scores1 = [62.58, 67.63, 81.37, 52.53, 62.98, 72.15, 59.05, 73.85, 97.24, 76.81, 89.34, 74.44, 68.52, 85.13, 90.75, 70.29, 75.62, 85.38, 77.82, 98.31, 79.08, 61.72, 71.33, 80.77, 80.31, 78.16, 61.15, 64.99, 72.67, 78.94]
exam_scores2 = [72.38, 71.28, 79.24, 83.86, 84.42, 79.38, 75.51, 76.63, 81.48,78.81,79.23,74.38,79.27,81.07,75.42,90.35,82.93,86.74,81.33,95.1,86.57,83.66,85.58,81.87,92.14,72.15,91.64,74.21,89.04,76.54,81.9,96.5,80.05,74.77,72.26,73.23,92.6,66.22,70.09,77.2]

# 10x8 figure
plt.figure(figsize=(10, 8)) 

# Plot the graphs on top of each other
plt.hist(
  exam_scores1,           # values
  bins=12,                # nr of bins
  alpha=0.5,              # transparency
  normed=True,            # normalization
  histtype = 'step',      # histogram type
  linewidth=2,            # line width
  label='1st Yr Teaching')# label

plt.hist(
  exam_scores2,           # values
  bins=12,                # nr of bins
  alpha=0.5,              # transparency
  normed=True,            # normalization
  histtype = 'step',      # histogram type
  linewidth=2,            # line width
  label='2nd Yr Teaching')# label  

# Show label legend
plt.legend()

# Graph and axis labels
plt.xlabel('Percentage')
plt.ylabel('Frequency')
plt.title('Final Exam Score Distribution')

# show graph
plt.show()

# Save graph/figure to file
plt.savefig('my_histogram.png')
```

# Maptlotlib -Labeled Pie Chart
```
from matplotlib import pyplot as plt

unit_topics = ['Limits', 'Derivatives', 'Integrals', 'Diff Eq', 'Applications'] # Labels
num_hardest_reported = [1, 3, 10, 15, 1] # Values

plt.figure(figsize=(10, 8)) # 10x8 figure

plt.pie(
  num_hardest_reported, # Values
  labels=unit_topics,   # Show labels near the slices
  autopct='%d%%')       # Show percentages on the slices

plt.axis('equal') # Make the pie "flat"

plt.title('Hardest Topics') # Title the graph

plt.show() # Show the graph

plt.savefig('my_pie_chart.png') # Save graph to file
```

# Matplotlib - Line with shaded error margin
```
from matplotlib import pyplot as plt

# Data
hours_reported =[3, 2.5, 2.75, 2.5, 2.75, 3.0, 3.5, 3.25, 3.25,  3.5, 3.5, 3.75, 3.75,4, 4.0, 3.75,  4.0, 4.25, 4.25, 4.5, 4.5, 5.0, 5.25, 5, 5.25, 5.5, 5.5, 5.75, 5.25, 4.75]
exam_scores = [52.53, 59.05, 61.15, 61.72, 62.58, 62.98, 64.99, 67.63, 68.52, 70.29, 71.33, 72.15, 72.67, 73.85, 74.44, 75.62, 76.81, 77.82, 78.16, 78.94, 79.08, 80.31, 80.77, 81.37, 85.13, 85.38, 89.34, 90.75, 97.24, 98.31]

# 10x8 figure
plt.figure(figsize=(10, 8)) 

# Setting the bounds of the error margin (20% in this case)
hours_lower_bound = [i - (i*0.20) for i in hours_reported] 
hours_upper_bound = [i + (i*0.20) for i in hours_reported] 

# Filling the shaded error margin
plt.fill_between(exam_scores, hours_lower_bound, hours_upper_bound, alpha=0.2)

# Filling the line itself
plt.plot(exam_scores, hours_reported, linewidth=2)

# Labels
plt.xlabel('Score')
plt.ylabel('Hours studying (self-reported)')
plt.title('Time spent studying vs final exam scores')

# Show figure/grahp
plt.show()

# Save figure/grahp to file
plt.savefig('my_line_graph.png')
```
