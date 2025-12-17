# One-Way ANOVA and Post Hoc Tests: Weightlifting Example

This guide explains how to perform a one-way ANOVA by hand, followed by post hoc tests (Fisher's LSD, Scheffé, Tukey, and Bonferroni) if the ANOVA is significant. We'll use a theme of weightlifting in kg. Imagine we have three groups of weightlifters (n=5 per group) using different training programs:  
- Group A (basic strength)  
- Group B (powerlifting focus)  
- Group C (Olympic lifting focus)  

The data represents maximum squat lifts in kg.

## Sample Data

- Group A: 100, 105, 110, 115, 120  
- Group B: 110, 115, 120, 125, 130  
- Group C: 120, 125, 130, 135, 140  

### Group Means
- Mean_A = (100 + 105 + 110 + 115 + 120) / 5 = 550 / 5 = **110 kg**  
- Mean_B = (110 + 115 + 120 + 125 + 130) / 5 = 600 / 5 = **120 kg**  
- Mean_C = (120 + 125 + 130 + 135 + 140) / 5 = 650 / 5 = **130 kg**  

### Grand Mean (Overall Mean)
Total sum = 550 + 600 + 650 = 1800  
Grand mean = 1800 / 15 = **120 kg**

## Step 1: Perform One-Way ANOVA by Hand

ANOVA tests if there's a significant difference between group means.

### Key Formulas
- Total Sum of Squares (SST) = ∑(each value − grand mean)² for all data  
- Between-Groups Sum of Squares (SSB) = ∑ n_i × (mean_i − grand mean)² for each group  
- Within-Groups Sum of Squares (SSW) = SST − SSB (or ∑(each value − group mean)² per group)  
- Degrees of Freedom:  
  - df_between = k − 1 (k = 3 groups → 2)  
  - df_within = N − k (N = 15 → 12)  
  - df_total = N − 1 = 14  
- Mean Square Between (MSB) = SSB / df_between  
- Mean Square Within (MSW) = SSW / df_within  
- F-statistic = MSB / MSW  

Compare F to critical F (α = 0.05, df = 2,12 ≈ 3.89).

### Calculations

#### SSB (Between-Groups)
- Group A: 5 × (110 − 120)² = 5 × 100 = 500  
- Group B: 5 × (120 − 120)² = 0  
- Group C: 5 × (130 − 120)² = 5 × 100 = 500  
- **SSB = 1000**

#### SSW (Within-Groups)
- Group A: (100−110)² + (105−110)² + (110−110)² + (115−110)² + (120−110)² = 100 + 25 + 0 + 25 + 100 = 250  
- Group B: 250 (same pattern)  
- Group C: 250 (same pattern)  
- **SSW = 750**

SST = SSB + SSW = 1750  

MSB = 1000 / 2 = **500**  
MSW = 750 / 12 = **62.5**  
F = 500 / 62.5 = **8**  

Since 8 > 3.89, the ANOVA is **significant**. Proceed to post hoc tests (pairwise comparisons: A vs B, A vs C, B vs C).  
All tests use α = 0.05 and equal group sizes (n = 5).

## Step 2: Fisher's Least Significant Difference (LSD)

### Formula
LSD = t × √(MSW × (1/n_i + 1/n_j))  
- t (two-tailed, α=0.05, df=12) ≈ 2.179  
- √(62.5 × 0.4) = √25 = 5  
- LSD ≈ 2.179 × 5 ≈ **10.895**

### Comparisons
- A vs B: |110 − 120| = 10 < 10.895 → **not significant**  
- A vs C: |110 − 130| = 20 > 10.895 → **significant**  
- B vs C: |120 − 130| = 10 < 10.895 → **not significant**

## Step 3: Scheffé's Test

### Formula
Threshold = √[(k−1) × F_critical × MSW × (1/n_i + 1/n_j)]  
- F_critical (α=0.05, df=2,12) ≈ 3.89  
- √(2 × 3.89 × 62.5 × 0.4) = √194.5 ≈ **13.946**

### Comparisons
- A vs B: 10 < 13.946 → **not significant**  
- A vs C: 20 > 13.946 → **significant**  
- B vs C: 10 < 13.946 → **not significant**

## Step 4: Tukey's Honestly Significant Difference (HSD)

### Formula (equal n)
HSD = Q × √(MSW / n)  
- Q (α=0.05, k=3, df=12) ≈ 3.77  
- √(62.5 / 5) ≈ 3.536  
- HSD ≈ 3.77 × 3.536 ≈ **13.33**

### Comparisons
- A vs B: 10 < 13.33 → **not significant**  
- A vs C: 20 > 13.33 → **significant**  
- B vs C: 10 < 13.33 → **not significant**

## Step 5: Bonferroni Correction

Adjust α = 0.05 / 3 ≈ 0.0167 (m = 3 pairwise comparisons).  
Standard error = √(62.5 × 0.4) = 5  
Critical t (two-tailed, α≈0.0167, df=12) ≈ 2.68  
Threshold difference ≈ 2.68 × 5 ≈ **13.4**

### Comparisons (using t-statistics)
- A vs B: t = 10 / 5 = 2 < 2.68 → **not significant**  
- A vs C: t = 20 / 5 = 4 > 2.68 → **significant**  
- B vs C: t = 10 / 5 = 2 < 2.68 → **not significant**

## Summary

All post hoc tests reach the same conclusion:  
- Group A differs significantly from Group C.  
- No significant difference between A and B, or between B and C.  

Conservativeness order: LSD (least conservative, smallest threshold) → Bonferroni → Tukey → Scheffé (most conservative, largest threshold).  

Choose the test based on your experimental needs (e.g., LSD for more power, Scheffé for protection against all possible contrasts). For unequal group sizes or more groups, adjust formulas accordingly. Critical values are approximate—consult exact statistical tables for precision.

Last Updated: December 2025  
License: The Evil Math Cat  
Contributions: Gimme me cat food damn it.
