# Heart_dataset_Power_BI

# Heart Disease Risk Dashboard (Power BI)

## Overview
An interactive Power BI dashboard analyzing 918 patients to show which symptoms, 
test results, and demographics are linked to a heart disease diagnosis. The data was 
cleaned in Power Query, and the key rates are calculated with DAX measures.

## Business Questions
1. What share of patients have heart disease?
2. Which chest pain types, symptoms, and demographics are most linked to it?
3. How do patients with and without heart disease differ on age, heart rate, and cholesterol?

## Dataset
Public heart disease dataset (`heart.csv`), 918 patients and 12 columns: age, sex, 
chest pain type, resting blood pressure, cholesterol, fasting blood sugar, resting ECG, 
max heart rate, exercise-induced angina, ST depression (Oldpeak), ST slope, and 
heart disease (yes/no).

## Data Cleaning (Power Query)
- Set the correct data types for every column.
- Checked for duplicate rows, blanks, and stray spaces: none found.
- **Replaced impossible zero values with null:** 172 patients (18.7%) had cholesterol 
  recorded as 0, and 1 patient had a resting blood pressure of 0.
- **Kept those patients instead of deleting them.** 88% of the zero-cholesterol 
  patients had heart disease, compared with 48% of the rest, so deleting them would 
  have removed most of the disease cases and understated the disease rate.
- Left 13 negative Oldpeak values unchanged, since I can't confirm they are errors.

## DAX Measures
| Measure | Formula | Purpose |
|---|---|---|
| Total Patients | `COUNTROWS(heart)` | Patient count |
| Patients with Disease | `CALCULATE(COUNTROWS(heart), heart[HeartDisease] = 1)` | Count with a diagnosis |
| Disease Rate | `DIVIDE([Patients with Disease], [Total Patients], 0)` | Share with a diagnosis |
| Avg Cholesterol | `AVERAGE(heart[Cholesterol])` | Ignores the nulls |
| Avg Max HR | `AVERAGE(heart[MaxHR])` | Average peak heart rate |
| Exercise Angina Disease Rate | `CALCULATE([Disease Rate], heart[ExerciseAngina] = "Y")` | Rate among patients with exercise angina |

## Dashboard Contents
| Visual | Question answered |
|---|---|
| KPI cards | Total patients, patients with disease, disease rate, average cholesterol |
| Disease Rate by Chest Pain Type | Which symptom pattern is most linked to disease |
| Disease Rate by Sex | How the rate differs between men and women |
| Disease Rate by Exercise Angina | Whether exercise-induced chest pain matters |
| Age Distribution by Disease Status | How disease is spread across ages |
| Avg Cholesterol & Max HR by Disease Status | How patients with and without disease differ |

Slicers (Sex, Chest Pain Type, ST Slope) filter every visual at once.

## Key Findings
- **508 of 918 patients (55.3%) have heart disease.**
- **Exercise-induced angina was the strongest signal.** 85.2% of patients with it had 
  heart disease (316 of 371), compared with 35.1% of those without (192 of 547).
- **Patients with no chest pain symptoms had the highest rate by chest pain type:** 
  79.0% (392 of 496), vs 43.5% for typical angina, 35.5% for non-anginal pain, and 
  13.9% for atypical angina. They are also over half of all patients (54%).
- **Men had a much higher rate than women** (63.2% vs 25.9%), but the data is 79% male, 
  so the comparison rests on only 193 women.
- **Patients with heart disease were older,** averaging 55.9 years vs 50.6.
- **They also had a lower max heart rate:** 127.7 vs 148.2 bpm, about 20 bpm lower.
- **Cholesterol separated the groups far less than symptoms did:** 251.1 for patients 
  with disease vs 238.8 for those without.

## Recommendations
- **Don't screen on chest pain symptoms alone.** The group reporting no chest pain had 
  the highest disease rate, so a symptom-only approach would miss many cases.
- **Give exercise test results heavy weight in risk reviews.** Exercise-induced angina 
  was the clearest signal in the data.
- **Collect more balanced data before drawing conclusions about sex.** The sample is 
  79% male, so the gap between men and women may not be reliable.
- **Improve how cholesterol is recorded.** Nearly one in five values was 0, and the 
  missing values were not random.
- **Follow up with a statistical model** (for example logistic regression) to separate 
  the effects of age, sex, and symptoms, which overlap in this data.

## Limitations
- This is a snapshot of patients, so the findings are associations, not causes.
- It is an analysis exercise and not medical advice or a diagnostic tool.
- Sex is imbalanced, and 18.7% of cholesterol values were missing.

## Skills Demonstrated
Data cleaning in Power Query, DAX measures (CALCULATE, DIVIDE), interactive 
visuals and slicers, and communicating findings and limitations.

## How to View
- **PDF:** The Pdfs show the dashboard, slicer prevews and DAX measures is a static copy of the report.
- **Interactive version:** download Heart_Disease_Dashboard.pbix and open it in 
  Power BI Desktop (Windows).


## Tools Used
Microsoft Power BI Desktop (Power Query, DAX)
