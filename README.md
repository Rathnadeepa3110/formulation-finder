# Formulation Finder

LUMORA Formulation Optimizer — Complete Application Description

This is the specification I would use to actually build the application. It follows the RSM/AI components already presented in your Slide 4: Multiple Linear Regression, Random Forest Regressor, Logistic Regression, Multi-Objective Optimization, Python, Pandas, Scikit-learn and RSM.

1. Application Purpose

LUMORA FORMULATION OPTIMIZER

A simple scientific application that helps researchers determine a recommended bio-composite material formulation by:

Material ranges
      ↓
Generate experimental formulations
      ↓
Perform physical experiments
      ↓
Enter measured results
      ↓
Analyze using RSM + ML
      ↓
Visualize relationships
      ↓
Optimize multiple properties
      ↓
Recommend formulation

The application is not intended to replace physical experiments.

The software identifies promising formulations from experimental data, which are then physically validated.

2. Main Application Flow

START
  │
  ▼
MATERIAL INPUT
  │
  ├── Number of materials
  ├── Material name
  ├── Minimum grams
  └── Maximum grams
  │
  ▼
GENERATE EXPERIMENTS
  │
  ▼
10 FORMULATION COMBINATIONS
  │
  ▼
PHYSICAL TESTING
  │
  ▼
ENTER RESULTS
  │
  ├── Hardness
  ├── Break resistance
  ├── Flexibility
  ├── Oil wicking
  ├── Breakdown
  └── Weight balance
  │
  ▼
DATA PROCESSING
  │
  ▼
MODEL ANALYSIS
  │
  ├── RSM
  ├── Multiple Linear Regression
  ├── Random Forest
  └── Classification
  │
  ▼
GRAPHICAL ANALYSIS
  │
  ├── Response surface
  ├── Contour plot
  ├── Actual vs predicted
  └── Performance comparison
  │
  ▼
MULTI-OBJECTIVE OPTIMIZATION
  │
  ▼
RECOMMENDED FORMULATION
  │
  ▼
PHYSICAL VALIDATION

3. SCREEN 1 — Material Input

The first screen should be extremely simple.

Header

LUMORA Formulation Optimizer

RSM-Based Bio-Composite Formulation Analysis

Input

Number of Materials
[ 4 ]

Then dynamically create material cards.

Example

MATERIAL 1

Name
[ Banana Fiber ]

Minimum Quantity
[ 2 ] g

Maximum Quantity
[ 6 ] g

MATERIAL 2

Name
[ Rice Husk ]

Minimum Quantity
[ 1 ] g

Maximum Quantity
[ 4 ] g

MATERIAL 3

Name
[ Binder ]

Minimum Quantity
[ 1 ] g

Maximum Quantity
[ 5 ] g

MATERIAL 4

Name
[ Glycerol ]

Minimum Quantity
[ 0.5 ] g

Maximum Quantity
[ 2 ] g

Button:

GENERATE FORMULATIONS

4. Screen 2 — Experiment Design

The application now generates the formulations.

You want 10 different experimental combinations.

Example:

TrialBanana FiberRice HuskBinderGlycerol12.01.54.01.023.52.03.00.835.01.02.01.544.03.02.50.652.53.53.51.2...............10............

The application should ensure that:

Values stay within minimum/maximum ranges.

Combinations are sufficiently different.

Every material is represented.

The experiment design is reproducible.

RSM option

Give the user:

Experimental Design

○ Generate 10 formulations
○ Central Composite Design
○ Box-Behnken Design

For your first version, Generate 10 formulations can be the default simplified mode.

5. Screen 3 — Experimental Result Entry

This is the most important part.

The software cannot know how the physical plate behaves.

You physically create and test each formulation.

Then enter the results.

Trial 1

FORMULATION #1

Banana Fiber      4.2 g
Rice Husk         2.1 g
Binder            2.8 g
Glycerol          0.9 g

Performance Results

Hardness
[ 85 ] %

Break Resistance
[ 90 ] %

Flexibility
[ 72 ] %

Oil Wicking
[ 80 ] %

Water Breakdown
[ 75 ] %

Weight Balance
[ 92 ] %

Then:

SAVE RESULT

The same structure appears for:

Trial 1
Trial 2
Trial 3
...
Trial 10

Or better, use a single table:

TrialHardnessBreakFlexibilityOil WickingBreakdownWeight185907280759227885808870903919465758295.....................

6. Screen 4 — Data Processing

Click:

ANALYZE DATA

Python processes the table.

Pandas

Used for:

CSV / table
    ↓
DataFrame
    ↓
Cleaning
    ↓
Missing-value checking
    ↓
Numerical processing

The application should show:

DATASET STATUS

Experiments:       10
Completed:         10
Missing values:     0
Factors:            4
Responses:          6

STATUS: READY FOR ANALYSIS

If something is missing:

WARNING

Trial 7 → Oil Wicking value missing.

Please enter the value before analysis.

7. Screen 5 — RSM Analysis

Now the actual RSM engine runs.

Inputs

Factors:
Banana Fiber
Rice Husk
Binder
Glycerol

Responses

Hardness
Break Resistance
Flexibility
Oil Wicking
Breakdown
Weight Balance

The application creates a mathematical relationship:

Material quantities
        ↓
Response

For example:

Banana Fiber ─────┐
Rice Husk ────────┤
Binder ───────────┼──→ Hardness
Glycerol ─────────┘

and:

Banana Fiber ─────┐
Rice Husk ────────┤
Binder ───────────┼──→ Oil Wicking
Glycerol ─────────┘

8. Multiple Linear Regression

This is one of the algorithms mentioned in your PPT.

The application uses it to estimate how material quantities relate to each response.

Conceptually:

Hardness =
β0
+ β1(Banana)
+ β2(Rice Husk)
+ β3(Binder)
+ β4(Glycerol)

The UI can show:

Hardness Model

R² = 0.XX
RMSE = X.XX

And similarly for the other responses.

You don't need to expose the mathematical equation to the normal user unless they click:

View Model Details

9. Random Forest Regressor

Your PPT specifically says Random Forest predicts mechanical strength and oil-wicking efficiency based on material composition.

The application can use:

Material quantities
       ↓
Random Forest
       ↓
Predicted response

Example:

INPUT FORMULATION

Banana Fiber     4.5 g
Rice Husk        2.3 g
Binder           2.2 g
Glycerol         1.0 g

          ↓

RANDOM FOREST

Predicted Hardness      84%
Predicted Oil Wicking   87%

10. Classification

Your PPT mentions Logistic Regression classification for pass/fail key tests.

You can create:

Quality Prediction

Hardness Requirement
       ↓
PASS / FAIL

Oil Wicking Requirement
       ↓
PASS / FAIL

Breakdown Requirement
       ↓
PASS / FAIL

Example:

QUALITY CHECK

Hardness             PASS
Break Resistance     PASS
Oil Wicking          PASS
Breakdown            PASS
Weight Balance       PASS

Overall:
QUALIFIED FOR NEXT TEST

However, this module requires enough labeled pass/fail observations to train a meaningful classifier. Don't fabricate training labels just to make the button work.

11. Graphical Analysis

This is where the application becomes visually impressive.

Graph 1 — 3D Response Surface

Example:

X = Banana Fiber
Y = Rice Husk
Z = Oil Wicking

The user can rotate the 3D graph.

Graph 2 — Contour Plot

Shows regions such as:

          Rice Husk
              ↑
       ┌─────────────┐
       │     HIGH    │
       │   ███████   │
       │ ███████████ │
       │   ███████   │
       │     LOW     │
       └─────────────┘
              → Banana Fiber

Graph 3 — Actual vs Predicted

Actual
  ↑
  │        •
  │      •
  │    •
  │  •
  │ •
  └────────────────→ Predicted

This helps demonstrate model performance.

12. Multi-Objective Optimization

This is the final intelligence layer.

Your user defines what matters.

Example

PropertyObjectiveHardnessMaximizeBreak ResistanceMaximizeFlexibilityMaximizeOil WickingMaximizeBreakdownTargetWeight BalanceTarget

The system searches the allowed formulation space.

Conceptually:

             FORMULATION SPACE

                  100%
                   │
        ┌──────────┼──────────┐
        │          │          │
        │   GOOD   │          │
        │ REGION   │          │
        │    ★     │          │
        │          │          │
        └──────────┴──────────┘
                   │
                  0%

13. Final Recommendation Screen

This should be the main output screen.

Recommended Formulation

┌────────────────────────────────────┐
│       RECOMMENDED FORMULATION      │
├────────────────────────────────────┤
│                                    │
│ Banana Fiber        4.6 g          │
│ Rice Husk           2.4 g          │
│ Binder              2.1 g          │
│ Glycerol            0.9 g          │
│                                    │
├────────────────────────────────────┤
│ Predicted Performance              │
│                                    │
│ Hardness             86%           │
│ Break Resistance     91%           │
│ Flexibility          76%           │
│ Oil Wicking          89%           │
│ Breakdown            74%           │
│ Weight Balance       93%           │
└────────────────────────────────────┘

Then:

Recommended for next physical trial

Not "guaranteed best."

14. Show Top 3 Formulations

This is even better than showing only one.

RANKED CANDIDATE FORMULATIONS

1. Formulation #7     Overall: 88.4%
2. Formulation #4     Overall: 86.9%
3. Formulation #9     Overall: 84.7%

Then:

FORMULATION #7

Banana Fiber       4.6 g
Rice Husk          2.4 g
Binder             2.1 g
Glycerol           0.9 g

This gives you options for physical validation rather than blindly trusting one prediction.

15. Technology Architecture

                 LUMORA WEB APP
                       │
                       ▼
                STREAMLIT UI
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
 MATERIAL INPUT   EXPERIMENT ENTRY   RESULTS
       │               │               │
       └───────────────┼───────────────┘
                       ↓
                    PANDAS
                       │
                       ↓
                  DATA PROCESSING
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
         RSM          MLR       RANDOM FOREST
          │            │            │
          └────────────┼────────────┘
                       ↓
                MODEL PREDICTION
                       │
                       ↓
             MULTI-OBJECTIVE
                OPTIMIZATION
                       │
                       ↓
              PLOTLY / MATPLOTLIB
                       │
                       ↓
              GRAPHS + RESULTS
                       │
                       ↓
              RECOMMENDATION

16. Technology Stack

Core

Python

Data

Pandas
NumPy

Machine Learning

Scikit-learn

Used for:

Multiple Linear Regression

Random Forest Regressor

Logistic Regression

RSM

Python statistical modeling

Use a suitable RSM/DOE implementation for the actual response-surface model.

Optimization

SciPy

Visualization

Plotly
Matplotlib

Frontend

Streamlit

17. What the judge can see in 2–3 minutes

This is the demo sequence I recommend.

1. Enter 4 materials
             ↓
2. Set gram ranges
             ↓
3. Generate 10 formulations
             ↓
4. Show experiment table
             ↓
5. Enter measured results
             ↓
6. Click ANALYZE
             ↓
7. Show RSM response surface
             ↓
8. Show MLR + Random Forest prediction
             ↓
9. Set optimization objectives
             ↓
10. Click OPTIMIZE
             ↓
11. Show Top 3 formulations
             ↓
12. Show recommended formulation

That is enough for a convincing live demonstration.

18. One thing we should NOT do

Don't build the application so that it generates:

"Random 10 formulas → random performance → AI says Formula 7 is best."

That is only a visual demo, not a scientifically meaningful RSM application.

Your actual logic should be:

RSM generates experimental combinations
                ↓
YOU physically test them
                ↓
YOU enter measured results
                ↓
Models learn the relationship
                ↓
Optimization searches for promising formulation
                ↓
YOU physically validate the recommendation

That distinction is important because your PPT describes actual experimental datasets covering material composition, mechanical testing, disintegration, oil-wicking and durability/pipe safety.

Final application concept

Input → Design → Experiment → Measure → Model → Visualize → Optimize → Recommend → Validate

dont need cloud strage , file storage enough and then dont ask q untill complete , u need to make entire application and then only need to get stop

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/03a9c885-413b-43ee-91fe-df79a3d401f7).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
