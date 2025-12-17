# One-Way ANOVA and Post Hoc Tests: Weightlifting Example

This guide explains how to perform a one-way ANOVA by hand, followed by post hoc tests (Fisher's LSD, Scheffé, Tukey, and Bonferroni) if the ANOVA is significant. We'll use a theme of weightlifting in kg. Imagine we have three groups of weightlifters (n=5 per group) using different training programs: Group A (basic strength), Group B (powerlifting focus), and Group C (Olympic lifting focus). The data represents maximum squat lifts in kg.

## Sample Data

- Group A: 100, 105, 110, 115, 120  
- Group B: 110, 115, 120, 125, 130  
- Group C: 120, 125, 130, 135, 140  

Group means:  
- Mean_A = (100 + 105 + 110 + 115 + 120) / 5 = 550 / 5 = 110 kg  
- Mean_B = (110 + 115 + 120 + 125 + 130) / 5 = 600 / 5 = 120 kg  
- Mean_C = (120 + 125 + 130 + 135 + 140) / 5 = 650 / 5 = 130 kg  

Grand mean (overall mean):  
Total sum = 550 + 600 + 650 = 1800  
Grand mean = 1800 / 15 = 120 kg  

## Step 1: Perform One-Way ANOVA by Hand

ANOVA tests if there's a significant difference between group means. Formulas:  

- Total Sum of Squares (SST) = sum of (each value - grand mean)^2 for all data  
- Between-Groups Sum of Squares (SSB) = sum of n_i * (mean_i - grand mean)^2 for each group  
- Within-Groups Sum of Squares (SSW) = SST - SSB (or sum of (each value - group mean)^2 per group)  
- Degrees of Freedom: df_between = k - 1 (k=groups=3, so 2), df_within = N - k (N=15, so 12), df_total = N - 1 = 14  
- Mean Square Between (MSB) = SSB / df_between  
- Mean Square Within (MSW) = SSW / df_within (this is the error variance)  
- F-statistic = MSB / MSW  
- Compare F to critical F from table (e.g., for alpha=0.05, df=2,12, critical F≈3.89)  

### Calculations

First, SSB:  
- Group A: 5 * (110 - 120)^2 = 5 * (-10)^2 = 5 * 100 = 500  
- Group B: 5 * (120 - 120)^2 = 5 * 0 = 0  
- Group C: 5 * (130 - 120)^2 = 5 * 10^2 = 5 * 100 = 500  
- SSB = 500 + 0 + 500 = 1000  

Now, SSW (within each group):  
- Group A: (100-110)^2 + (105-110)^2 + (110-110)^2 + (115-110)^2 + (120-110)^2 = 100 + 25 + 0 + 25 + 100 = 250  
- Group B: (110-120)^2 + (115-120)^2 + (120-120)^2 + (125-120)^2 + (130-120)^2 = 100 + 25 + 0 + 25 + 100 = 250  
- Group C: (120-130)^2 + (125-130)^2 + (130-130)^2 + (135-130)^2 + (140-130)^2 = 100 + 25 + 0 + 25 + 100 = 250  
- SSW = 250 + 250 + 250 = 750  

SST = SSB + SSW = 1000 + 750 = 1750 (verify: sum of all (x - 120)^2 = same)  

MSB = 1000 / 2 = 500  
MSW = 750 / 12 = 62.5  
F = 500 / 62.5 = 8  

Critical F (alpha=0.05, df=2,12) ≈ 3.89. Since 8 > 3.89, ANOVA is significant. Proceed to post hoc tests to compare pairs: A vs B, A vs C, B vs C.

Assume equal n=5 per group, alpha=0.05 for all tests.

## Step 2: Fisher's Least Significant Difference (LSD)

LSD uses t-tests with pooled error from ANOVA. For each pair:  

- Difference = |mean_i - mean_j|  
- LSD threshold = t * sqrt(MSW * (1/n_i + 1/n_j))  
  - t from t-table (two-tailed, alpha=0.05, df=df_within=12) ≈ 2.179  
  - Here, sqrt(62.5 * (1/5 + 1/5)) = sqrt(62.5 * 0.4) = sqrt(25) = 5  
  - LSD = 2.179 * 5 ≈ 10.895  

Compare:  
- A vs B: |110-120| = 10 < 10.895 → not significant  
- A vs C: |110-130| = 20 > 10.895 → significant  
- B vs C: |120-130| = 10 < 10.895 → not significant  

## Step 3: Scheffé's Test

More conservative for all contrasts. Threshold:  

- Scheffé critical value = sqrt( (k-1) * F_critical * MSW * (1/n_i + 1/n_j) )  
  - F_critical (alpha=0.05, df=2,12) ≈ 3.89  
  - (k-1)=2  
  - sqrt(2 * 3.89 * 62.5 * 0.4) = sqrt(7.78 * 25) = sqrt(194.5) ≈ 13.946  

Compare differences to 13.946:  
- A vs B: 10 < 13.946 → not significant  
- A vs C: 20 > 13.946 → significant  
- B vs C: 10 < 13.946 → not significant  

## Step 4: Tukey's Honestly Significant Difference (HSD)

Uses studentized range statistic (Q). For equal n:  

- HSD = Q * sqrt(MSW / n)  
  - Q from Q-table (alpha=0.05, k=3, df_within=12) ≈ 3.77  
  - sqrt(62.5 / 5) = sqrt(12.5) ≈ 3.536  
  - HSD = 3.77 * 3.536 ≈ 13.33  

Compare differences to 13.33:  
- A vs B: 10 < 13.33 → not significant  
- A vs C: 20 > 13.33 → significant  
- B vs C: 10 < 13.33 → not significant  

## Step 5: Bonferroni Correction

Perform multiple t-tests, adjust alpha = 0.05 / m (m=number of pairs=3, so alpha=0.0167).  

For each pair: t = (mean_i - mean_j) / sqrt(MSW * (1/n_i + 1/n_j))  
- Standard error = sqrt(62.5 * 0.4) = 5  
- Critical t (two-tailed, alpha=0.0167, df=12) ≈ 2.68 (interpolate from t-table)  

- Threshold difference = 2.68 * 5 ≈ 13.4  

Or compute t for each:  
- A vs B: t = 10 / 5 = 2 < 2.68 → not significant  
- A vs C: t = 20 / 5 = 4 > 2.68 → significant  
- B vs C: t = 10 / 5 = 2 < 2.68 → not significant  

## Summary

In this weightlifting example, all tests agree: Group A differs significantly from Group C, but not from B, and B not from C. LSD is least conservative (smaller threshold), Scheffé most conservative (largest). Use based on experiment needs. For unequal n or more groups, adjust formulas accordingly. Critical values from statistical tables (not provided here; look up in a stats book).
