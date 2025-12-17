POST-HOC TESTS & ASSUMPTION CHECKS FOR ANOVAs (By Hand)
🏋️‍♂️ SCENARIO

You tested 3 different pre-workout supplements (A, B, C) on squat max increase (kg) after 8 weeks.
You did a one-way ANOVA by hand (good job).
Results:
Group	n	Mean increase (kg)	Variance
A	5	12.4	4.3
B	5	15.2	5.1
C	5	9.8	3.8

ANOVA results:

    MSbetween=58.0MSbetween​=58.0

    MSwithin=4.4MSwithin​=4.4 (this is MSerrorMSerror​)

    F=13.18F=13.18, Fcrit(2,12)=3.89Fcrit​(2,12)=3.89 → SIGNIFICANT

    dferror=12dferror​=12, total N = 15

Now we spot the differences.
🥊 POST-HOC TEST 1: TUKEY'S HSD (THE ALL-ROUNDER)

When: All pairwise comparisons, equal sample sizes.

Step-by-step:

    Get the q-value from Studentized Range Table

        k=3k=3 groups, dferror=12dferror​=12, α=0.05α=0.05

        Table gives q=3.77q=3.77

    Formula:

HSD=q×MSerrorn
HSD=q×nMSerror​​
​
HSD=3.77×4.45
HSD=3.77×54.4​
​
HSD=3.77×0.88=3.77×0.938=3.54
HSD=3.77×0.88
​=3.77×0.938=3.54

    Compare mean differences:

Pair	Difference	> 3.54?	Significant?
B vs A	15.2-12.4=2.8	No	✗
B vs C	15.2-9.8=5.4	Yes	✓
A vs C	12.4-9.8=2.6	No	✗

Conclusion: Only B vs C is significantly different.
🥊 POST-HOC TEST 2: BONFERRONI (THE CONSERVATIVE LIFTER)

When: Fewer comparisons, or you want to be extra safe.

Step-by-step:

    Number of comparisons:

m=k(k−1)2=3×22=3
m=2k(k−1)​=23×2​=3

    New alpha per comparison:

αnew=0.053=0.0167
αnew​=30.05​=0.0167

    Do t-test for each pair:

    t formula:

t=Xˉi−XˉjMSerror(1ni+1nj)
t=MSerror​(ni​1​+nj​1​)
​Xˉi​−Xˉj​​

For B vs C:
t=15.2−9.84.4(15+15)=5.44.4×0.4
t=4.4(51​+51​)
​15.2−9.8​=4.4×0.4
​5.4​
t=5.41.76=5.41.326=4.07
t=1.76
​5.4​=1.3265.4​=4.07

    Critical t from t-table:
    df=12df=12, two-tailed, α=0.0167α=0.0167 → look up α/2=0.0083α/2=0.0083 in tail.
    Approx tcrit≈2.78tcrit​≈2.78 (exact needs interpolation).

    Compare: ∣t∣>tcrit∣t∣>tcrit​ → significant.

Pair	t	> 2.78?	Significant?
B vs C	4.07	Yes	✓
B vs A	2.11	No	✗
A vs C	1.96	No	✗

Same result as Tukey here.
🥊 POST-HOC TEST 3: SCHEFFÉ (THE OVERKILL)

When: Any contrasts, including complex ones.

Step-by-step:

    Get F critical for original ANOVA:
    Fcrit(2,12)=3.89Fcrit​(2,12)=3.89

    Formula for any pairwise comparison:

S=(k−1)×Fcrit×MSerror×(1ni+1nj)
S=(k−1)×Fcrit​×MSerror​×(ni​1​+nj​1​)
​

For B vs C:
S=2×3.89×4.4×0.4
S=2×3.89×4.4×0.4
​
S=2×3.89×1.76=13.6928=3.70
S=2×3.89×1.76
​=13.6928
​=3.70

    Compare mean difference to S:

        B vs C difference = 5.4 > 3.70 → ✓ significant

        Others less than 3.70 → ✗ not significant

Most conservative, still finds B vs C different here.
🥊 POST-HOC TEST 4: FISHER'S LSD (THE AGGRESSIVE LIFTER)

When: Only after significant F, equal n, exploratory.

Step-by-step:

    Get t critical for original dferrordferror​ at α=0.05α=0.05:
    tcrit(12)=2.179tcrit​(12)=2.179 (two-tailed)

    LSD formula:

LSD=tcrit×MSerror(1ni+1nj)
LSD=tcrit​×MSerror​(ni​1​+nj​1​)
​
LSD=2.179×4.4×0.4=2.179×1.76=2.179×1.326=2.89
LSD=2.179×4.4×0.4
​=2.179×1.76
​=2.179×1.326=2.89

    Compare mean differences:

        B vs C: 5.4 > 2.89 → ✓

        B vs A: 2.8 > 2.89? NO → ✗ (barely misses!)

        A vs C: 2.6 < 2.89 → ✗

Fisher's LSD is least conservative, but here still only B vs C significant.
📊 ASSUMPTION CHECKS (THE WARM-UP)
1. Normality of Residuals

What to do:

    List all 15 residuals (actual score minus group mean)

    Sort them smallest to largest

    Get normal scores from table (or roughly: z=Φ−1((rank−0.375)/(N+0.25))z=Φ−1((rank−0.375)/(N+0.25)) )

    Plot residuals vs normal scores → if straight line, good.

Quick check:

    Find max residual = ?

    If data roughly symmetric, median residual near 0.

2. Homogeneity of Variance

Levene’s Test by hand:

    Compute median for each group

    New variable: d=∣score−group median∣d=∣score−group median∣

    Run one-way ANOVA on d:

        If F not significant → variances equal

        Our example: variances (4.3, 5.1, 3.8) close, likely OK.

Rule of thumb: largest variance ≤ 4× smallest variance → OK.
Here: 5.1 / 3.8 = 1.34 → fine.
3. Independence

    Data collected independently? (different lifters per group)

    No repeated measures → OK.

🎯 SUMMARY TABLE FOR OUR DATA
Post-hoc test	Critical value	B vs A	B vs C	A vs C
Tukey HSD	3.54	✗	✓	✗
Bonferroni	t ≈ 2.78	✗	✓	✗
Scheffé	3.70	✗	✓	✗
Fisher’s LSD	2.89	✗	✓	✗

Conclusion for coach: Only Supplement B beats C in squat gains. A is intermediate.
📌 CHEAT SHEET

    ANOVA significant? → proceed.

    Equal n? → Use Tukey for all pairs, Fisher if exploratory.

    Unequal n? → Use Bonferroni or Scheffé.

    Conservative? → Scheffé or Bonferroni.

    Check assumptions:

        Normality: Q-Q plot of residuals

        Equal variance: Levene’s test (ANOVA on absolute deviations from median)

        Independence: Design-based.