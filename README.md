# Automobile-Price-Fuel-Economy-Analysis

# Automobile Price & Fuel Economy Analysis

A data analysis project in Python (Pandas) using the UCI Automobile dataset of 1985 imported cars. I built it for my BTA 522 course at Portland State University.

**Tools:** Python, Pandas, Seaborn, Matplotlib, Google Colab

---

## Goal

I wanted to see how price and fuel economy change with a car's engine, fuel type, body style, and drive type. I picked this dataset because it has a good mix of categorical and continuous variables. I think car enthusiasts and people interested in classic cars or automotive history would find it interesting, since it shows how 1985 imports were priced. [Add one sentence in your own words about why this matters to that audience.]

**Questions I started with**
1. Does an engine with more cylinders or more horsepower tend to cost more?
2. Do diesel cars get better mileage than gas cars, and do they cost more?
3. How does price differ by body style and drive wheels?

## The data

- **Source:** UCI Machine Learning Repository, Automobile dataset (1985 Ward's Automotive Yearbook). I downloaded it from Kaggle (`toramky/automobile-dataset`).
- **Size:** 205 cars and 26 columns. I used 8 of the columns.
- **Missing values:** the raw file uses "?" for missing.

| Variable | Meaning | Type |
|---|---|---|
| price | Price of the car (USD) | continuous |
| horsepower | Engine horsepower | continuous |
| city_mpg | City miles per gallon | continuous |
| highway_mpg | Highway miles per gallon | continuous |
| num_of_cylinders | Number of cylinders (two to twelve) | categorical, ordinal |
| fuel_type | gas or diesel | categorical |
| body_style | convertible, hardtop, hatchback, sedan, wagon | categorical |
| drive_wheels | fwd, rwd, or 4wd | categorical |

## What I did, step by step

**1. Goal and questions.** I wrote down what I wanted to find out and who it was for (see above).

**2. Describing the data and codebook.** I wrote a short description of the dataset and a codebook for my 8 variables, with each variable's label, type, storage type, and category codes.

**3. Project setup.** I made a `data` folder for the cleaned file and a `figures` folder for charts.

**4. Reading the data.** I read the CSV with `pd.read_csv` and told Pandas that "?" means missing (`na_values="?"`). I replaced the hyphens in the column names with underscores so I could use them in code. Then I checked the storage type of each variable. Price and horsepower are continuous but stored as `float64`, and the mpg columns are `int64`. The text columns are stored as strings until I convert them.

**5. Cleaning.** I made bar charts of the four categorical variables to check for inconsistent labels, and the categories were already clean. The missing values were the real cleaning issue:
- `price` was missing in 4 rows and `horsepower` in 2, so I dropped those 6 rows and kept 199 cars.
- `normalized_losses` was missing in 41 of 205 rows (20%), and the missing values were clustered by make. My questions don't use it, so I left it out of the analysis instead of filling in guesses.

**6. Category type.** I converted the four categorical variables to the Pandas `category` type. I made `num_of_cylinders` an ordered category from two to twelve.

**7. Transformations.** [I changed the price of vehicles to decimals where I divided each price point by thousands of dollars like one car being $13,495 dollars divide it by 1000 you get 13.495 making it easier, to read, then I also did a transformation dividing into price groups, from small, medium, large most vehicles averaged out to medium group.]

**8. Subsetting.** I kept only my 8 variables of interest.

**9. Feather file.** I saved the cleaned data to `data/auto_clean.feather` and read it back in, then checked that the shape and the category types came through.

**10. Splitting and merging.** I created a `car_id` and split the data into two tables, one with engine and mileage columns and one with price and car-type columns. Then I merged them back together on `car_id`, as if the data had come from two files.

**11. Charts.** I made histograms of price, horsepower, and city and highway mpg, and bar charts of cylinders, body style, and fuel type. Price and horsepower are right-skewed, meaning most cars are cheaper and less powerful with a few expensive, high-power ones. Four-cylinder cars, sedans, and gas cars make up most of the data.

**12. Aggregations.** I grouped the data to answer my questions.

| Group | Cars | Average price |
|---|---|---|
| 4 cylinders | 155 | $10,312 |
| 6 cylinders | 24 | $23,672 |
| 8 cylinders | 4 | $38,900 |
| Hatchback | 67 | $9,958 |
| Sedan | 94 | $14,460 |
| Hardtop | 8 | $22,209 |
| Convertible | 6 | $21,891 |
| Front-wheel drive | 116 | $9,239 |
| Rear-wheel drive | 75 | $19,758 |

- Price and horsepower have a correlation of about 0.81.
- Diesel cars had better average mileage than gas cars and a somewhat higher average price, but there are only 20 diesel cars.
- Rear-wheel-drive cars averaged about twice the price of front-wheel-drive cars.

[Add your own interpretation of these results in a sentence or two.]

.**Step 13: As part of iterative EDA, use Data Analysis I & II insights to fine-tune your original 2-3 questions, and frame 2 questions that are the next steps that you would look into and why they matter. No new coding is expected for these questions.

Part 1: Fine-tuning the original questions. Describe each question as it was, then how it should change.

Does an engine with more cylinders or more horsepower tend to cost more? (price, num_of_cylinders, horsepower), (from my analysis It is evident the more cylinders a car has the more cost in price shoots up, so I could focus my question around cylinders and engine type cause price to change?)

Do diesel cars get better mileage than gas cars and do they cost more? (city_mpg, highway_mpg, fuel_type, price) (from this analysis I did find that diesel cars have hihgher cost in miles per gallon in the city and the highway, what can be changed is adding horsepower to the question, does the use or wear on the engine cause the certain cars to cost more?

How does price differ by body style and drive wheels? (price, body_style, drive_wheels). (Hardtop cars have are the most expensive bodystyle in a car, while rear wheel drive cars are the most the most expensive in (rear wheel drive cars are the most expensive across all body styles.)

## Limitations

- Some groups are very small (one three-cylinder car, one twelve-cylinder car, 20 diesel cars, 8 hardtops, 6 convertibles, 8 four-wheel-drive cars), so their averages aren't reliable.
- These results show association, not cause. A car can have a high price and more cylinders for the same reason, such as being larger or more luxurious.
- The data covers 1985 imports, so it doesn't describe today's cars.

## Use of AI

I used Claude (Anthropic) during this project for explanations, code help, and troubleshooting, and I used a generative AI tool to evaluate my analysis, as the assignment required. I made the choices about the dataset, how to handle missing data, and my questions myself. [Edit this to match what you did.]

## How to run it

```bash
pip install pandas seaborn matplotlib pyarrow kagglehub
```

Open the notebook and run the cells from top to bottom. The data downloads from Kaggle in the notebook.

## Data credit

Automobile dataset, UCI Machine Learning Repository: https://archive.ics.uci.edu/dataset/10/automobile
https://www.kaggle.com/datasets/toramky/automobile-dataset
