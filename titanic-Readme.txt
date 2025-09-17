TIANIC SURVIVAL ANALYSIS 
objective:- Analyze the titanic dataset to understand *who survived and why*, using pandas,numpy, and matplotlib.   
            ill took at demograohics (age,sex), travel class, family size, and embarkation port, then summmarize the 
            patterns and draw conclusions. 

            2) Dataset overview (what’s inside)

Rows × Columns: 891 × 12

Key columns: Survived (target), Pclass, Sex, Age, SibSp, Parch, Fare, Embarked, plus identifiers like PassengerId, Name, Ticket, Cabin.

Data quality at a glance

Missing Age: 177 rows

Missing Cabin: ~77.1% (!!)

Embarked: a few missing (very small)

Ticket has 681 unique values (many repeats → multiple passengers under same ticket).

Takeaway: Age is incomplete but usable; Cabin is basically a black box — not reliable for modeling without heavy feature engineering.

3) Quick descriptive stats (NumPy & Pandas)

Age: mean ≈ 29.7, median ≈ 28.0, std ≈ 14.52 (wide spread → very young to very old on board)

Fare is heavily right-skewed (skew ≈ 4.79) → a few very expensive tickets pull the average up

4) Survival snapshot

Overall survival rate: 38.38%

By sex:

Female: 74.20%

Male: 18.89%
→ This is the strongest single pattern. “Women and children first” was not just a line.

By class (Pclass):

1st: 62.96%

2nd: 47.28%

3rd: 24.24%
→ Class mattered a lot (access to lifeboats, proximity to decks, etc.).

By embarkation port:

Cherbourg (C): 55.36%

Queenstown (Q): 38.96%

Southampton (S): 33.70%
→ Likely tied to class composition at each port (C had more 1st-class passengers).

5) Age patterns (who actually got saved?)

I binned age to make it human-readable:

Child (0–12): 57.97% survived

Teen (13–18): 42.86%

Young Adult (19–30): 35.56%

Adult (31–45): 42.57%

Middle Age (46–60): 40.74%

Senior (60+): 22.73%

Children had higher survival; seniors struggled. Interestingly, 31–45 did a bit better than 19–30 — probably confounded by sex/class.

Mean age by outcome:

Survived: 28.34

Didn’t survive: 30.63
Age matters, but not as much as sex and class.

6) Family size effect (because nobody sails alone, right?)

I created FamilySize = SibSp + Parch + 1 and grouped it:

Small (2–4): 57.88% survived

Solo (1): 30.35%

Large (5+): 16.13%

Being with a small group helped coordination and getting to lifeboats; very large groups struggled to stay together; solo travelers had fewer helping hands.

7) Fares and money talk

Average fare by class:

1st class: 84.15

2nd class: 20.66

3rd class: 13.68

This lines up with survival by class. Higher fare → more likely in 1st class → better survival odds. But fare itself is noisy (heavy skew and shared tickets).

8) Correlations (numeric only, just to sanity-check)

Top relationships with Survived (direction + strength):

Sex (female coded) → strong positive

Pclass → moderate negative (higher class number = worse outcome)

Fare → weak/moderate positive

Age → slight negative

SibSp / Parch → very small effects individually; combined as FamilySize tells a clearer story.

TL;DR: Sex and Class dominate. Age and Fare contribute but are secondary.

9) Visuals I plotted (what they showed)

Bar: Survival by Gender → Massive gap (females ~74%, males ~19%).

Bar: Survival by Class → 1st ≫ 2nd ≫ 3rd.

Histogram: Age → Many in 20s–30s; survivors slightly skew younger.

Bar: Average Fare by Class → 1st class far higher (no surprise).

Bar: Survival by Embarked → Cherbourg best; likely because more 1st-class.

(These are in your notebook/outputs. If you want, I can export PNGs and drop them in a report doc.)

10) Key insights (straight, no chasers)

Gender is the #1 factor: Females had ~4× the survival rate of males.

Class is #2: First class had ~2.6× the survival of third class.

Children did better than seniors; adults 31–45 slightly better than 19–30, but that’s entangled with sex/class.

Small families win: Small groups survived best; large families suffered the most.

Embarked is a proxy: Port differences mostly mirror class mix.

Data gaps: Cabin is basically unusable as-is (77% missing). Age needs imputation if we build models.

(11) Limitations (what I wouldn’t bet my life on)

Missing data (especially Cabin) limits cabin-deck analysis.

Survival is historical + social policy–driven (lifeboat policy), so correlations ≠ pure causality.

Fare is distorted by group tickets and outliers.

Age missingness could bias simple averages if not imputed properly.

(12) What I’d do next (if turning this into a proper ML project)

Feature engineering

Title extraction from Name (Mr, Mrs, Miss, Master) → strong proxy for sex/age/social status.

FamilySize (done) + IsAlone (FamilySize==1).

Ticket frequency (group size), Cabin deck (first letter) where available.

Impute Age smartly (median by Title + Pclass + Sex).

Modeling: Start with logistic regression (interpretable), then tree-based (Random Forest / XGBoost) to capture non-linearities.

Evaluation: Stratified CV, confusion matrix, ROC-AUC; check fairness across sex/class (don’t blindly maximize accuracy).

(13) Conclusion (the elevator pitch)

The data confirms a clear hierarchy of survival on the Titanic:

Women and 1st-class passengers had the highest chances.

Children did better than most adults; seniors had the worst outcomes.

Small families outperformed solo travelers and large groups.

Money/class and social rules of the time strongly shaped outcomes.

From a data science standpoint, the dataset is small but rich. With a bit of feature engineering and careful handling of missing values, it’s perfect for a clean, interpretable predictive model — and a great teaching case for how real-world context explains the stats.