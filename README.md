# Goibibo Flight-Price-Analysis-Project


## Overview

This project focuses on analyzing flight prices from a dataset obtained from Goibibo, with two primary analyses: **Best Time to Fly (Price vs. Time Analysis)** and **Airline Comparison and Performance Analysis**. The goal of these analyses is to provide insights into how flight prices vary based on time and airline performance, helping users make informed decisions when booking flights.

### 1. Best Time to Fly (Price vs. Time Analysis)
**Objective**: Identify the best time to book flights for the lowest prices by analyzing historical data.
- Grouped flight data by different time periods (month, day of the week) to understand price variations.
- Analyzed the impact of **departure** and **arrival times** on flight prices to determine if flights at certain times of the day are generally cheaper or more expensive.

### 2. Airline Comparison and Performance Analysis
**Objective**: Compare different airlines based on pricing, flight duration, and number of stops to determine which airline offers the best value.
- Compared multiple airlines on factors like price, duration, and stops to find the best value-for-money airline options.
- Conducted performance analysis based on pricing trends across different airlines.

### Tools & Technologies:
- **Python** for data analysis and visualization.
- **Pandas** for data manipulation and cleaning.
- **Matplotlib** and **Seaborn** for visualizing trends and patterns.
- **Jupyter Notebook** for executing and documenting the analysis.
  
# Questions Answered
# 1. Best Time to Fly (Price vs. Time Analysis)

Objective: Identify the best time to book flights for the lowest prices by analyzing historical flight data.

Approach:

Grouped flight data by various time periods such as month, day of the week, and time of day to examine how prices vary.
Analyzed the impact of departure and arrival times on flight prices to determine whether certain times of the day tend to have cheaper or more expensive flights.
Provided insights to help users identify cost-effective booking strategies.

Key Findings:
1. Grouping data by month and calculateing the average price
```
monthly_price = data.groupby('month')['price'].mean().reset_index()
plt.figure(figsize=(10, 6))
sns.lineplot(data=monthly_price, x='month', y='price', marker='o')
plt.title('Average Flight Prices by Month')
plt.xlabel('Month')
plt.ylabel('Average Price')
plt.show()
```

![image](https://github.com/user-attachments/assets/196a3344-2536-458d-bf51-b2ca49098072)

2. Grouping data by day of the week and calculating the average price
```
weekly_price = data.groupby('day_of_week')['price'].mean().reset_index()
plt.figure(figsize=(10,6))
sns.lineplot(x='day_of_week', y='price', data=weekly_price)
plt.title('Average Flight Prices by Day of the Week')
plt.xlabel('Day of the Week (0=Monday, 6=Sunday)')
plt.ylabel('Average Price')
plt.show()
```
![image](https://github.com/user-attachments/assets/c3e8d80d-8a90-4fa2-9e30-e4e723e79ae3)

3. Grouping data by depature hour and calculateing the average price
```
avg_price_by_dep_hour = df.groupby('dep_hour')['price'].mean().sort_index()
plt.figure(figsize=(10,6))
plt.plot(avg_price_by_dep_hour.index, avg_price_by_dep_hour.values, marker='o', linestyle='-')
plt.title('Average Flight Prices by Departure Hour')
plt.xlabel('Departure Hour')
plt.ylabel('Average Price')
plt.grid(True)
plt.show()
```
![image](https://github.com/user-attachments/assets/5a878a20-2929-4a29-8f1b-595c7aa91046)

5. Grouping data by arrival hour and calculateing the average price
```
avg_price_by_arr_hour = df.groupby('arr_hour')['price'].mean().sort_index()
plt.figure(figsize=(10,6))
plt.plot(avg_price_by_arr_hour.index, avg_price_by_arr_hour.values, marker='o', linestyle='-')
plt.title('Average Flight Prices by Arrival Hour')
plt.xlabel('Arrival Hour')
plt.ylabel('Average Price')
plt.grid(True)
plt.show()
```
![image](https://github.com/user-attachments/assets/43b55fd6-3504-4cc7-97e5-fa3b25744885)

# 2. Airline Comparison and Performance Analysis

Objective: Compare airlines based on pricing, flight duration to determine which airline offers the best overall value.

Approach:

Compared pricing trends across different airlines.
Evaluated the impact of flight duration on overall flight cost.
Determined which airlines offer the best balance between price, flight duration.

Key Findings: 
1. Calculating average price and duration for each airline
```
airline_comparison = df.groupby('airline').agg(
    avg_price=('price', 'mean'),
    avg_duration=('duration_minutes', 'mean')
).reset_index()

print(airline_comparison)
```
![image](https://github.com/user-attachments/assets/ca6ff15e-29a4-4225-8ec6-c2e6ef4646e4)

2. Evaluating each attribute to score best Airline
```
airline_comparison['total_score'] = airline_comparison[['avg_price', 'avg_duration']].mean(axis=1)

airline_comparison = airline_comparison.sort_values('total_score')

print(airline_comparison[['airline', 'total_score']])
```
![image](https://github.com/user-attachments/assets/12d0a54e-9769-4b87-89e8-7b0cea2acc66)

3. Plotting average price by airline
```
plt.figure(figsize=(10,6))
airline_comparison.plot(kind='bar', x='airline', y='avg_price', color='skyblue')
plt.title('Average Flight Prices by Airline')
plt.xlabel('Airline')
plt.ylabel('Average Price')
plt.xticks(rotation=45)
plt.show()
```
![image](https://github.com/user-attachments/assets/8b4fb0d0-dcd4-4d4f-a569-5aee423d706a)

4. Plot average duration by airline
```
plt.figure(figsize=(10,6))
airline_comparison.plot(kind='bar', x='airline', y='avg_duration', color='lightgreen')
plt.title('Average Flight Duration by Airline (in minutes)')
plt.xlabel('Airline')
plt.ylabel('Average Duration (minutes)')
plt.xticks(rotation=45)
plt.show()
```
![image](https://github.com/user-attachments/assets/3486e489-112a-40b1-a24a-e265c0daa1f5)


