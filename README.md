# Determinants of Adequate Antenatal Care Attendance in Nigeria
**A Survey-Weighted Analysis Using DHS 2018 Data**

DOI: 10.64898/2026.05.02.26352203

![R](https://img.shields.io/badge/Language-R-276DC3?style=flat&logo=r)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![DHS Status](https://img.shields.io/badge/Data-DHS%202018-blue)
![Survey Weighted](https://img.shields.io/badge/Method-Survey%20Weighted-orange)
![Survival Analysis](https://img.shields.io/badge/Method-Survival%20Analysis-red)

---

## Table of Contents
- [Overview](#overview)
- [Connection to Prior Work](#connection-to-prior-work)
- [Key Findings](#key-findings)
- [Background & Motivation](#background--motivation)
- [Research Questions](#research-questions)
- [Data](#data)
- [Methods](#methods)
- [Results](#results)
- [Visualisations](#visualisations)
- [Limitations](#limitations)
- [References](#references)
- [Contact](#contact)
- [Acknowledgments](#acknowledgments)

---

## Overview

This project analyses **21,465 births** from the 2018 Nigeria Demographic and Health Survey (NDHS) to identify independent predictors of adequate antenatal care attendance (≥4 visits) using **survey-weighted multivariable logistic regression** and **Kaplan-Meier survival analysis** with Cox proportional hazards modelling.

All analyses account for the complex stratified cluster sampling design of the DHS, producing nationally representative estimates.

### Why This Matters

Nigeria accounts for approximately 20% of global maternal deaths (WHO, 2019). Adequate antenatal care is one of the most effective interventions for reducing maternal and newborn mortality, yet 4 in 10 Nigerian women do not meet the WHO minimum standard of 4 visits. Understanding which women are being left behind, and why, is essential for designing effective maternal health programmes.

### What This Analysis Adds

This analysis:
1. **Controls for confounding** to isolate truly independent predictors
2. **Applies DHS survey weights** to produce nationally representative estimates with 95% confidence intervals
3. **Adds a survival analysis dimension**  examining not just whether women attended adequate ANC, but *how long they waited* before their first visit
4. **Quantifies confounding**  showing how much crude associations change after adjustment, revealing which associations are real versus which were explained by correlated factors

---

## Connection to Prior Work

This project is the direct scientific sequel to:

> **[Determinants of Skilled Birth Attendance in Nigeria](https://github.com/Ugoeze-Lucy/-Determinants-of-Skilled-Birth-Attendance-in-Nigeria-A-Population-Based-Analysis-Using-DHS-2018-Data/edit/main/README.md)** (Python, DHS 2018)

That analysis found that attending ≥4 ANC visits was the **strongest modifiable predictor of skilled birth attendance** (aOR = 3.80, 95% CI: 3.51–4.11) more influential than education, wealth, or urban residence after full adjustment.

The question *what determines whether women achieve this level of ANC in the first place?* is precisely what this project addresses.

Together, the two projects form a complete evidence chain:

```
Education + Wealth
        ↓
Earlier ANC initiation [this study — survival analysis]
        ↓
Adequate ANC attendance ≥4 visits [this study — logistic regression]
        ↓
Skilled birth attendance [prior SBA study]
        ↓
Reduced maternal mortality
```

---

## Key Findings

| Finding | Statistic | Interpretation |
|---|---|---|
| National ANC prevalence | **57.8%** (95% CI: 56.2%–59.4%) | 4 in 10 Nigerian women do not meet the WHO minimum standard |
| Strongest predictor | Higher education: **aOR = 5.64** (95% CI: 4.45–7.15) | Nearly 6× the odds vs no education, after full adjustment |
| Wealth gradient | Richest vs Poorest: **aOR = 3.93** (95% CI: 3.11–4.95) | Almost 4× the odds after controlling for education and residence |
| Residence surprise | Urban: **aOR = 1.12, p = 0.113** (not significant) | The large crude urban-rural gap was entirely explained by confounding |
| Regional inequality | South West vs North West: **aOR = 3.31** | 3× the odds within one country: the largest independent regional effect |
| Parity effect | 6+ children: **aOR = 0.59** (95% CI: 0.51–0.68) | High-parity women have 41% lower odds: dose-response pattern |
| Median ANC initiation | **5 months** of pregnancy (95% CI: 4–5) | 2 months later than WHO recommended initiation at month 3 |
| Education on timing | Higher education: **HR = 1.35** | Educated women initiate ANC 35% faster (earlier) in pregnancy |
| Confounding magnitude | Higher education crude OR: 22.49 → adjusted: 5.64 | 74.9% of crude effect was confounding by wealth and residence |

### Policy Implications

- **Immediate intervention:** Target uneducated, high-parity women in North West and North East Nigeria with early ANC outreach - community health workers visiting homes in months 2–3 of pregnancy
- **Geographic prioritisation:** The North West had the lowest weighted prevalence (42.3%) and latest ANC initiation - this zone requires the most intensive programme investment
- **Wealth as a structural barrier:** The Poorest quintile had 30.7% adequate ANC - economic barriers (transport, opportunity cost) must be directly addressed, not assumed away by ANC free-at-point-of-use policies
- **Long-term investment:** Girls' education remains the most powerful upstream driver of maternal health behaviour in Nigeria

---

## Background & Motivation

### The Problem

Despite modest progress, Nigeria remains one of the highest-burden countries for maternal mortality globally:
- **512 deaths per 100,000 live births** (WHO, 2017), among the highest worldwide
- Approximately **67,000 maternal deaths annually**, 19% of global total
- Most deaths are preventable with timely, adequate antenatal and delivery care

### What Adequate ANC Provides

The WHO 2002 guideline defines adequate ANC as ≥4 visits. During these visits, women receive:
- Blood pressure monitoring for pre-eclampsia detection
- Malaria prophylaxis (IPTp) which is critical in Nigeria's endemic setting
- Iron and folic acid supplementation
- HIV testing and PMTCT counselling
- Foetal growth monitoring and complication identification
- Birth planning and danger sign education

Late initiation means compressed time for these interventions. A woman who attends her first visit at 7 months has approximately 6–8 weeks for all of the above. A woman who attends at month 2 has 7 months.

### The Gap

The 2018 NDHS reported significant regional disparities in ANC attendance that aggregate national statistics obscure. Understanding the independent determinants after controlling for the fact that disadvantaged factors cluster together, is critical for targeted policy.

---

## Research Questions

**Primary Question**

What sociodemographic factors independently predict adequate antenatal care attendance among women of reproductive age in Nigeria?

**Specific Questions**

1. What is the weighted prevalence of adequate ANC attendance (≥4 visits) in Nigeria, with confidence intervals accounting for the complex survey design?
2. Which sociodemographic factors education, wealth, residence, region, age, parity are independently associated with adequate ANC after controlling for confounders?
3. How does the effect of each predictor change between unadjusted and adjusted models, and what does this reveal about confounding?
4. What is the median gestational age at first ANC visit, and does this differ significantly by sociodemographic group?
5. Which factors independently predict earlier ANC initiation after accounting for other predictors?

**Objectives**

- ✅ Estimate the weighted national prevalence of adequate ANC attendance with 95% confidence intervals
- ✅ Produce crude (unadjusted) and adjusted odds ratios for all predictors
- ✅ Quantify confounding, measure the change from crude to adjusted ORs for key predictors
- ✅ Generate Kaplan-Meier survival curves for time to first ANC visit by key subgroups
- ✅ Identify independent predictors of earlier ANC initiation using weighted Cox regression

---

## Data

### Source

**Nigeria Demographic and Health Survey (NDHS) 2018**
- Conducted by: National Population Commission (NPC) & ICF
- Sample design: Two-stage stratified cluster sampling
- Nationally representative of women aged 15–49
- 36 states + Federal Capital Territory

### Dataset Details

| Item | Detail |
|---|---|
| File used | Individual Recode (IR) NGIR7BFL.DTA |
| Total records | 41,821 women aged 15–49 |
| Eligible sample | 21,792 women with a birth in the last 5 years |
| Final analytic sample | **21,465** (327 excluded for missing ANC data, 1.5%) |
| Survival analysis sample | **16,084** (women with complete ANC timing data) |

### Key Variables

| Variable | DHS Code | Type | Categories / Notes |
|---|---|---|---|
| **Outcome** | | | |
| Adequate ANC | Derived from m14_1 | Binary | 0 = <4 visits; 1 = ≥4 visits (WHO 2002 standard) |
| Time to first ANC | m13_1 | Continuous | Months pregnant at first visit; 0 = never attended (censored) |
| **Predictors** | | | |
| Education | v106 | Categorical | No education (ref), Primary, Secondary, Higher |
| Wealth index | v190 | Categorical | Poorest (ref), Poorer, Middle, Richer, Richest |
| Residence | v025 | Binary | Rural (ref), Urban |
| Region | v024 | Categorical | North West (ref), North Central, North East, South East, South South, South West |
| Age | v012 | Grouped | 15–19 (ref), 20–24, 25–29, 30–34, 35–39, 40–49 |
| Parity | v201 | Grouped | 1 (ref), 2–3, 4–5, 6+ |
| **Survey Design** | | | |
| Sampling weight | v005 | Continuous | Applied as v005 / 1,000,000 |
| Cluster ID | v001 | Numeric | Primary sampling unit |
| Stratum | v023 | Categorical | 74 strata (state × urban/rural) |

### Data Access

Freely available upon registration at [dhsprogram.com](https://dhsprogram.com). Users must register independently. This repository contains no raw data files in compliance with DHS data use terms.

---

## Methods

### Study Design
Cross-sectional analysis of secondary survey data (2018 NDHS)

### Analytic Approach

#### 1. Data Preparation
- Loaded Stata `.dta` file using `haven::read_dta()`
- Filtered to women with ≥1 birth in the preceding 5 years (`v208 ≥ 1`)
- Recoded DHS sentinel values (98 = "don't know", 99 = missing) to `NA`
- Created binary outcome: `anc_adequate` = 1 if ≥4 visits, 0 if <4 visits
- Recoded all predictors to labelled factors with theoretically appropriate reference categories
- Applied DHS sampling weight: `weight = v005 / 1,000,000`
- Excluded 327 women (1.5%) with missing ANC data

#### 2. Survey Design
Constructed a complex survey design object using `srvyr::as_survey_design()` with:
- **Cluster IDs** (`v001`): accounts for intra-cluster correlation among women in the same enumeration area
- **Strata** (`v023`): 74 state × urban/rural strata, sampled independently
- **Weights** (`weight`): corrects for unequal probability of selection, producing nationally representative estimates
- `nest = TRUE`: accounts for cluster IDs nested within strata

#### 3. Descriptive Analysis
- Unweighted sample characteristics by ANC adequacy status (Table 1) using `gtsummary::tbl_summary()`
- Weighted prevalence of adequate ANC overall and by each predictor using `srvyr::survey_mean()`
- Comparison of weighted vs unweighted estimates to assess sampling correction magnitude

#### 4. Bivariate Analysis
- Unweighted chi-square tests for crude associations (Table 1)
- Survey-weighted cross-tabulations with 95% confidence intervals

#### 5. Logistic Regression
- **Unadjusted models**: each predictor modelled individually using `survey::svyglm()` with `quasibinomial()` family
- **Adjusted model**: all predictors entered simultaneously
- Exponentiated coefficients for odds ratios with 95% confidence intervals
- Confounding assessment: percentage change = ((aOR − crude OR) / crude OR) × 100

#### 6. Survival Analysis
- **Survival object**: `survival::Surv(time = months_pregnant, event = attended_anc)`
- **Kaplan-Meier curves**: `survfit()` overall and by subgroup; plotted with `survminer::ggsurvplot()`
- **Log-rank tests**: `survdiff()` for formal significance testing of group differences
- **Cox proportional hazards model**: `coxph()` with survey weights, all predictors simultaneously; hazard ratios extracted with 95% CIs

#### 7. Software
All analyses conducted in **R version 4.5.3**. Key packages: `tidyverse`, `haven`, `survey`, `srvyr`, `survival`, `survminer`, `gtsummary`, `flextable`.

---

## Results

### 1. Sample Characteristics

**Study population: n = 21,465 women with a birth in the last 5 years**

| Characteristic | n | % |
|---|---|---|
| **Residence** | | |
| Rural | 14,082 | 65.6 |
| Urban | 7,710 | 35.4 |
| **Education** | | |
| No education | 9,527 | 44.4 |
| Primary | 3,410 | 15.9 |
| Secondary | 7,064 | 32.9 |
| Higher | 1,791 | 8.3 |
| **Wealth Index** | | |
| Poorest | 5,025 | 23.4 |
| Poorer | 4,905 | 22.8 |
| Middle | 4,586 | 21.4 |
| Richer | 4,025 | 18.7 |
| Richest | 3,251 | 15.1 |
| **Region** | | |
| North West | 6,309 | 29.4 |
| North East | 4,506 | 21.0 |
| North Central | 3,875 | 18.0 |
| South West | 2,563 | 11.9 |
| South East | 2,365 | 11.0 |
| South South | 2,174 | 10.1 |

### 2. Weighted Prevalence of Adequate ANC

**National weighted prevalence: 57.8% (95% CI: 56.2%–59.4%)**

| Variable | Weighted % | 95% CI |
|---|---|---|
| **Overall** | **57.8** | 56.2–59.4 |
| **By education** | | |
| No education | 34.6 | 32.5–36.7 |
| Primary | 64.2 | 61.6–66.7 |
| Secondary | 78.6 | 77.3–79.9 |
| Higher | 92.3 | 90.8–93.7 |
| **By residence** | | |
| Rural | 46.0 | 44.0–48.0 |
| Urban | 76.1 | 74.2–77.9 |
| **By wealth** | | |
| Poorest | 30.7 | 28.0–33.4 |
| Poorer | 42.9 | 40.1–45.6 |
| Middle | 61.3 | 59.1–63.6 |
| Richer | 75.3 | 73.2–77.3 |
| Richest | 89.2 | 87.7–90.7 |
| **By region** | | |
| North West | 42.3 | 39.4–45.2 |
| North East | 44.0 | 40.8–47.3 |
| North Central | 54.6 | 51.6–57.6 |
| South South | 72.6 | 69.5–75.6 |
| South East | 84.3 | 82.2–86.3 |
| South West | 89.9 | 87.8–92.0 |

### 3. Adjusted Logistic Regression Results

**Survey-weighted multivariable logistic regression — adjusted odds ratios**

| Predictor | aOR | 95% CI | p-value |
|---|---|---|---|
| **Education** (ref: No education) | | | |
| Primary | 2.12 | 1.88–2.40 | <0.001 *** |
| Secondary | 2.86 | 2.50–3.26 | <0.001 *** |
| Higher | 5.64 | 4.45–7.15 | <0.001 *** |
| **Residence** (ref: Rural) | | | |
| Urban | 1.12 | 0.97–1.28 | 0.113 NS |
| **Wealth** (ref: Poorest) | | | |
| Poorer | 1.39 | 1.21–1.61 | <0.001 *** |
| Middle | 2.04 | 1.74–2.39 | <0.001 *** |
| Richer | 2.47 | 2.08–2.94 | <0.001 *** |
| Richest | 3.93 | 3.11–4.95 | <0.001 *** |
| **Region** (ref: North West) | | | |
| North Central | 0.92 | 0.79–1.07 | 0.288 NS |
| North East | 1.06 | 0.89–1.25 | 0.521 NS |
| South East | 2.13 | 1.77–2.56 | <0.001 *** |
| South South | 1.00 | 0.82–1.21 | 0.964 NS |
| South West | 3.31 | 2.56–4.27 | <0.001 *** |
| **Age group** (ref: 15–19) | | | |
| 20–24 | 1.28 | 1.08–1.51 | 0.004 ** |
| 25–29 | 1.40 | 1.16–1.69 | <0.001 *** |
| 30–34 | 1.80 | 1.48–2.18 | <0.001 *** |
| 35–39 | 1.70 | 1.37–2.10 | <0.001 *** |
| 40–49 | 1.93 | 1.55–2.40 | <0.001 *** |
| **Parity** (ref: 1 child) | | | |
| 2–3 children | 0.81 | 0.72–0.92 | <0.001 *** |
| 4–5 children | 0.67 | 0.58–0.77 | <0.001 *** |
| 6+ children | 0.59 | 0.51–0.68 | <0.001 *** |

Significance: *** p<0.001; ** p<0.01; NS = not significant

### 4. Confounding Assessment

The substantial reduction in effect sizes after adjustment reveals significant confounding:

| Variable | Crude OR | Adjusted OR | % Change | Interpretation |
|---|---|---|---|---|
| Higher education | 22.49 | 5.64 | −74.9% | Heavily confounded by wealth and residence |
| Secondary education | 6.94 | 2.86 | −58.9% | Substantial confounding |
| Primary education | 3.39 | 2.12 | −37.3% | Moderate confounding |
| Urban residence | Large | 1.12 (NS) | Lost significance entirely | Effect fully explained by wealth and education |

**Key insight:** Higher education's crude OR of 22.49 collapsed to 5.64 after adjustment 74.9% of the crude association was confounding, primarily driven by the correlation between education and wealth, residence, and region. This mirrors the SBA project finding where education's crude OR (64.04) fell to 7.01 (−89.0%) confirming a consistent structural pattern across both analyses.

### 5. Survival Analysis Results

**Median time to first ANC visit: 5 months of pregnancy (95% CI: 4–5 months)**

This is 2 months later than the WHO recommendation of first attendance before month 3. The KM table shows the peak initiation period is months 3–5 of pregnancy.

| Month of pregnancy | % not yet attended first ANC |
|---|---|
| Month 1 | 98.0% |
| Month 2 | 92.6% |
| Month 3 | 75.9% |
| Month 4 | 50.1% ← just above 50%, threshold not yet crossed |
| Month 5 | 27.7% ← median: first month where >50% have attended|
| Month 6 | 12.6% |
| Month 7 | 2.8% |

**Log-rank tests all significant at p < 0.0001:**

| Comparison | Chi-square | p-value |
|---|---|---|
| By education | 671 (3 df) | <2e-16 |
| By region | 664 (5 df) | <2e-16 |
| By wealth | 485 (4 df) | <2e-16 |
| By residence | 52.4 (1 df) | 5e-13 |

**Cox proportional hazards model adjusted hazard ratios:**

| Predictor | HR | 95% CI | p-value |
|---|---|---|---|
| **Education** (ref: No education) | | | |
| Primary | 1.10 | 1.04–1.16 | <0.001 *** |
| Secondary | 1.19 | 1.13–1.26 | <0.001 *** |
| Higher | 1.35 | 1.23–1.47 | <0.001 *** |
| **Residence** (ref: Rural) | | | |
| Urban | **0.93** | 0.89–0.97 | <0.001 *** |
| **Wealth** (ref: Poorest) | | | |
| Poorer | 1.07 | 1.02–1.13 | 0.011 * |
| Middle | 1.11 | 1.05–1.17 | <0.001 *** |
| Richer | 1.14 | 1.07–1.22 | <0.001 *** |
| Richest | 1.32 | 1.22–1.43 | <0.001 *** |
| **Region** (ref: North West) | | | |
| North Central | 1.29 | 1.22–1.37 | <0.001 *** |
| North East | 1.13 | 1.08–1.19 | <0.001 *** |
| South East | 1.22 | 1.14–1.30 | <0.001 *** |
| South South | 1.13 | 1.06–1.22 | <0.001 *** |
| South West | 1.36 | 1.26–1.46 | <0.001 *** |
| **Parity** (ref: 1 child) | | | |
| 4–5 children | 0.80 | 0.74–0.87 | <0.001 *** |
| 6+ children | 0.77 | 0.71–0.84 | <0.001 *** |

**The residence paradox:** Urban residence was not significant in logistic regression (aOR 1.12, p = 0.113) and showed slower ANC initiation in the Cox model (HR 0.928). Despite the large crude urban-rural gap in prevalence, urban residence carries no independent protective effect after controlling for education, wealth, and region. This suggests the urban advantage operates entirely through the higher education and wealth of urban women, not through any inherent characteristic of urban living or urban health infrastructure.

---

## Visualisations

### Figure 1: Prevalence of adequate ANC by sociodemographic characteristics

<img width="4800" height="3000" alt="fig1_combined_descriptive" src="https://github.com/user-attachments/assets/0ef4d2bc-89b5-401f-a57b-77e498555d24" />


6-panel chart showing:
- Education gradient (No education 34.9% → Higher 91.7%)
- Wealth gradient (Poorest 30.9% → Richest 87.9%)
- Residence gap (Rural 47.9% vs Urban 74.9% — crude)
- Regional disparity (North West 41.2% → South West 88.5%)
- Age pattern (youngest and oldest with lowest rates)
- Parity decline (1 child 64.2% → 6+ children 46.9%)

### Figure 2: Distribution of ANC visit counts

<img width="3000" height="1800" alt="fig2_anc_distribution" src="https://github.com/user-attachments/assets/d536320a-06f8-4136-88c8-182845fd4534" />


Shows the distribution of raw ANC visit counts with the WHO threshold (4 visits) marked. The peak visit frequency is 4–5 visits, with a meaningful cluster at 2–3 visits, women close to but not reaching the standard.

### Figure 3: Time to first ANC visit by place of residence (Kaplan-Meier)


<img width="3000" height="2400" alt="fig3_km_residence" src="https://github.com/user-attachments/assets/45e5f425-bbe4-4a7f-ab6c-7ffb1290c48e" />


KM curves show that urban women initiate ANC approximately 1 month earlier than rural women (median 4 vs 5 months). Log-rank p < 0.0001. Dashed line shows the median. Number at risk table shows women still awaiting first visit at each time point.

### Figure 4: Time to first ANC visit by education level (Kaplan-Meier)


<img width="3000" height="2400" alt="fig4_km_education" src="https://github.com/user-attachments/assets/0bae9e8f-f2e7-45b0-b15e-c7440af07381" />


Clear separation by education level. Higher educated women (darkest curve) drop fastest - attending earliest. Uneducated women stay highest longest - waiting latest into pregnancy for their first visit. Log-rank p < 0.0001.

### Figure 5: Time to first ANC visit by geopolitical zone (Kaplan-Meier)


<img width="3300" height="2700" alt="fig5_km_region" src="https://github.com/user-attachments/assets/91f4d8b8-2062-4dfd-a193-588601422e46" />


The north-south divide in ANC timing is visually striking. South West women (darkest curve) initiate earliest. North West women (pink curve) wait longest. At month 5, 2,493 North West women had still not attended their first visit, compared to 906 South West women, a 2.7-fold difference in the number waiting.

---

## Limitations

**1. Cross-sectional design**
Cannot establish causality, associations reflect correlations at one point in time.

**2. Self-reported ANC data**
Women report ANC visits from memory, sometimes recalling births up to 5 years prior. Recall bias may underestimate or overestimate visits.

**3. Survival analysis sample reduction**
The KM and Cox analyses used 16,084 women rather than 21,465 because `m13_1` (months pregnant at first ANC) had higher missing data than `m14_1` (total ANC count). Women excluded from survival analysis may differ systematically from those included, a potential source of selection bias.

**4. Cox model and complex survey design**
The Cox model was run with survey weights but without full complex survey variance estimation (clusters and strata). Standard errors may be slightly underestimated.

**5. Unmeasured confounders**
Variables not available in the DHS that could influence ANC attendance include: distance to nearest health facility, quality of care at facilities, cultural and religious norms regarding pregnancy, and women's autonomous decision-making power.

**6. Temporal limitation**
Data from 2018. The COVID-19 pandemic (2020–2021) significantly disrupted health services globally and may have altered ANC attendance patterns post-survey.

**7. Generalisability**
Findings are specific to Nigeria. The socioeconomic and health system context differs from other sub-Saharan African countries.

---

## References

1. National Population Commission (NPC) [Nigeria] and ICF. 2019. *Nigeria Demographic and Health Survey 2018*. Abuja, Nigeria, and Rockville, Maryland, USA: NPC and ICF.

2. World Health Organization. 2019. *Trends in maternal mortality 2000 to 2017: estimates by WHO, UNICEF, UNFPA, World Bank Group and the United Nations Population Division*. Geneva: WHO.

3. World Health Organization. 2002. *WHO antenatal care randomized trial: manual for the implementation of the new model*. Geneva: WHO. (4-visit ANC standard)

4. World Health Organization. 2016. *WHO recommendations on antenatal care for a positive pregnancy experience*. Geneva: WHO. (Updated 8-contact model)

5. United Nations. 2015. *Transforming our world: the 2030 Agenda for Sustainable Development*. New York: United Nations. (SDG 3.1)

6. Unegbu, U.L. 2024. *Determinants of Skilled Birth Attendance in Nigeria: A Population-Based Analysis Using DHS 2018*. GitHub. [Link to prior SBA project]

---

## Contact

**Ugoeze Lucy Unegbu**
MSc Medical Statistics & Epidemiology | Health Data Analyst | Epidemiologist

📫 Email: [unegbuugoezelucy@gmail.com](mailto:unegbuugoezelucy@gmail.com)
💼 LinkedIn: [linkedin.com/in/ugoeze-lucy](https://www.linkedin.com/in/ugoeze-lucy/)
📊 GitHub: [github.com/Ugoeze-Lucy](https://github.com/Ugoeze-Lucy)

**Open to:**
- Epidemiologist / Health Data Analyst roles in global and maternal health
- Research collaborations in maternal, newborn, and HIV health in LMICs
- DHS data analysis consultancies
- Speaking opportunities at conferences and academic events

---

## Acknowledgments

The DHS Program for making high-quality, nationally representative survey data publicly accessible. The National Population Commission of Nigeria for conducting the 2018 NDHS. ICF for technical support and data dissemination. The R open-source community for the packages that made this analysis possible.

---

## License

This project is licensed under the MIT License — see the LICENSE file for details.

**Data usage:** DHS data is used in accordance with DHS Program data use terms. No raw data files are included in this repository. Users must register independently at [dhsprogram.com](https://dhsprogram.com) to access the dataset.

---

## Citation

DOI: 10.64898/2026.05.02.26352203

If you use this analysis in your work, please cite as:

```bibtex
@misc{unegbu2026anc,
  author    = {Ugoeze Lucy Unegbu},
  title     = {Determinants of Adequate Antenatal Care Attendance in Nigeria:
               A Survey-Weighted Analysis Using DHS 2018},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/Ugoeze-Lucy/}
}
```

---

##  Support This Work

If you found this analysis useful:
- ⭐ Star this repository
- 🔀 Fork and build upon it (MIT licensed)
- 💬 Share with colleagues in public health and maternal health research
- 📧 Reach out for collaboration or discussion
