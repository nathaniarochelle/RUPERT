# rupert-analysis

Analysis code for the RUPERT study:

**"Beyond good intentions: Potential for negative effects of a digital peer support and psychoeducation platform for German emergency medical personnel"**

Rochelle, N. S. ([ORCID](https://orcid.org/0009-0000-4794-5974)), Zimdahl, M., Blume, A., Bell, S., Lukersmith, S., Niedermeier, N., & Reich, H. ([ORCID](https://orcid.org/0000-0002-9577-1144))

German Foundation for Depression and Suicide Prevention, Leipzig · Goethe University Frankfurt · Diskussionsforum Depression e.V., Leipzig · University of Canberra

Trial registration: [DRKS00029917](https://www.drks.de/DRKS00029917)



## About the study

RUPERT is a digital peer support and psychoeducation platform against depression for German emergency medical personnel. It consists of a landing page, a protected information platform, a discussion forum and expert chats. Data were collected at three time points (T0, T1, T2). This repository contains the R code for the analysis of negative effects (Negative Effects Questionnaire, NEQ) and sociodemographic characteristics.



## Contents

| File | Description |
| ---- | ----------- |
| `[Statistics Analyses.txt]` | Statistical analyses: data cleaning and joining, sociodemographic descriptives, NEQ frequencies and severity, binary coding of negative effects and logistic regressions (RQ3). |
| `[Values and Items.txt]` | Values and items: description of all variables used in the script, with response codes (e.g. 1 = not selected, 2 = selected) and the item wording of the 21 NEQ items. |




## Data

**The data files are not part of this repository.** They are only released on request. If interested, please contact: Nathania Seanette Rochelle, nathania.seanette.rochelle@deutsche-depressionshilfe.de

The script expects the following data frames:

| Object | Description |
| ------ | ----------- |
| `RUPERT_ori` | Original survey export, one row per participant and time point, ID variable `CASE`. |
| `RUPERT_HR` | Corrected version with the additional variables `state`, `Participant_ID`, `Time` and `sex`, ID variable `Count`. |

Both are merged by `CASE = Count` into `RUPERT_join`. Only participants with `state` 0 or 1 are included in the analyses. 

Values of `state`:

| Value | Meaning |
| ----- | ------- |
| 0 | [to be added] |
| 1 | [to be added] |
| 2 | implausible |
| 3 | duplicate |



## Analysis steps

1. **Data cleaning and joining:** merge of the original data with the corrected HR dataset.
2. **Sociodemographics:** sex, relationship status, professional degree, qualifications, employment status, age and years of experience at T0 and T1.
3. **RQ1:** Frequencies of reported negative effects after the use of the RUPERT intervention (NE01) and of their attribution to the program or to other circumstances (NE04), per item at T1 and T2. Severity ratings (NE03) are described overall and separately by attribution.
4. **RQ2:** If any negative effects were observed at T1, do they persist at T2? Are there delayed negative effects that were not present at T1, but present at T2?
5. **RQ3:** To what extent are negative effects associated with age, gender, and years of experience? Logistic regressions with age, sex and years of experience (T0) as predictors of reporting at least one negative effect attributed to the program, separately for T1 and T2.


## Codebook (short version)

Full version in `Values and Items.txt`.

### Sociodemographics

| Variable | Content | Coding |
| -------- | ------- | ------ |
| `SD03` | Sex | 1 = male, 2 = female, 3 = diverse |
| `SD07` | Relationship status | 1 = single, no relationship; 2 = single, in a relationship; 3 = married / registered partnership; 4 = separated / divorced / partnership dissolved; 5 = widowed; 6 = other |
| `SD08_01` to `SD08_09` | Professional degree (checkboxes) | 1 = not selected, 2 = selected |
| `SD08_09a` | Other degree | open text |
| `SD09` | Year of entry | |
| `SD10` | Years employed | |
| `SD11` | Qualification | 1 = Rettungshelfer, 2 = Rettungssanitäter, 3 = Rettungsassistent, 4 = Notfallsanitäter, 5 = other |
| `SD12_01`, `SD12_02` | Employment: paid / voluntary | 1 = not selected, 2 = selected |
| `SD13_02` | Weekly hours (voluntary) | |

### Negative effects (NEQ, 21 items, `xx` = 01 to 21)

| Variable | Content | Coding |
| -------- | ------- | ------ |
| `NE01_xx` | Did the negative effect occur? | 1 = no, 2 = yes |
| `NE03_xx` | Severity | 1 = not at all, 2 = slightly, 3 = moderately, 4 = severely, 5 = very severely |
| `NE04_xx` | Cause | 1 = participation in the program, 2 = other circumstances |

### Usage behavior

| Variable | Content | Coding |
| -------- | ------- | ------ |
| `UF01_01` to `UF01_04` | Components used: landing page, information platform, discussion forum, expert chats | 1 = not selected, 2 = selected |
| `UF02_01` | Hours per week on the information platform | |
| `UF04_01` | Hours per week in the forum | |


## How to reproduce

1. Place the data files in the project folder (they are not included).
2. Open `[Statistics Analyses.txt]` in RStudio.
3. Run the script from top to bottom.


## Requirements

R [version] with `dplyr`, `tidyr`, `ggplot2`, `purrr`.

## References


Sources for the Negative Effects Questionnaire (NEQ):

Rozental, A., Kottorp, A., Boettcher, J., Andersson, G., & Carlbring, P. (2016). Negative effects of psychological treatments: An exploratory factor analysis of the negative effects questionnaire for monitoring and reporting adverse and unwanted events. *PloS One, 11*(6), e0157503.

Rozental, A., Kottorp, A., Forsström, D., Månsson, K., Boettcher, J., Andersson, G., Furmark, T., & Carlbring, P. (2019). The Negative Effects Questionnaire: Psychometric properties of an instrument for assessing negative effects in psychological treatments. *Behavioural and Cognitive Psychotherapy, 47*(5), 559–572. https://doi.org/10.1017/S1352465819000018
