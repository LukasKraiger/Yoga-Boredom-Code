# Data README

Contact: Lukas Kraiger <lukas.kraiger@univie.ac.at>

Last update: 19.10.2026

## Study overview

This repository contains the data for a longitudinal study of yoga practice and boredom. The project combines:

- a baseline questionnaire collected at study entry
- repeated post-session questionnaires collected after each yoga session
- a prepared analysis dataset used for longitudinal mediation models in Mplus

The raw files are exported from the ESMira study app as semicolon-delimited CSV files.

## ESMira study source code

File: `esmira_study_source_code.json`

This is the ESMira source-code export for the study, provided so the study setup
can be imported into an ESMira server. It contains the study settings and the
two questionnaires (the start questionnaire and the post-session questionnaire),
not participants' response data.

To import it, sign in to the ESMira admin tool and use its study import/source
code workflow to load `esmira_study_source_code.json`. See the
[ESMira website](https://esmira.kl.ac.at/) and its
[documentation wiki](https://github.com/KL-Psychological-Methodology/ESMira/wiki)
for the current import instructions. Review the imported study's settings and
publication status on your server before making it available to participants.

## Dataset structure

### 1) Baseline questionnaire

File: `raw/baseline.csv`

This file contains the participant-level baseline information collected at the start of data collection.

Fields in this file:

- `entryId`: unique record identifier within the exported file
- `userId`: pseudonymous participant identifier; used to link repeated responses from the same participant
- `uploaded`: export timestamp in unixtime
- `appType`: device type (e.g., iOS/Android)
- `appVersion`: app version used to complete the questionnaire
- `studyId`: study identifier
- `accessKey`: empty variable normally used to identify specific invitation links
- `studyVersion`: study version
- `studyLang`: language used in the questionnaire
- `questionnaireName`: name of the instrument or questionnaire
- `eventType`: event type recorded in the app
- `timezone`: timezone at time of response
- `responseTime`: Unix timestamp of the response
- `responseTime_formatted`: response timestamp in human-readable format
- `formDuration`: time taken to complete the questionnaire
- `pageDurations`: page-level completion time information
- `lastInvitation`: timestamp of last invitation/reminder completely zero since there where no invitations
- `lastInvitation_formatted`: formatted reminder timestamp, empty since lasInvitations is always zero
- `SD02.1`: Item aksing about age "Please enter your age (in years).", participants could answer openly
- `SD01`: Item asking about the gender of participants "Which gender do you identify as?". Participants had the Options 1 = female, 2 = male, 3 = diverse/non-binary, 4 = prefer not to answer
- `CU01.1`: Item asking about the country participants live in "Which country do you currently live in?", participants could answer openly.
- `group`: study group or condition when recorded, since there was no group this variable is empty

### 2) Post-session questionnaires

File: `raw/post_session.csv`

This file contains the repeated-measures assessments collected after each yoga session. It is the main longitudinal dataset used for the main analyses.

Core fields include:

- `entryId`: unique record identifier
- `userId`: pseudonymous participant identifier
- `uploaded`: export timestamp in unixtime
- `appType`: device type (e.g., iOS/Android)
- `appVersion`: app version used to complete the questionnaire
- `studyId`: study identifier
- `accessKey`: empty variable normally used to identify specific invitation links
- `studyVersion`: study version
- `studyLang`: language used in the questionnaire
- `questionnaireName`: name of the instrument or questionnaire
- `eventType`: event type recorded in the app
- `timezone`: timezone at time of response
- `responseTime`: Unix timestamp of the response
- `responseTime_formatted`: response timestamp in human-readable format
- `formDuration`: time taken to complete the questionnaire
- `pageDurations`: page-level completion time information
- `lastInvitation`: timestamp of last invitation/reminder completely zero since there where no invitations
- `lastInvitation_formatted`: formatted reminder timestamp, empty since lasInvitations is always zero
- `PL01`: Question about the yoga setting "How did you just practice yoga?". With the options 1 = alone, 2 = in a group 
- `FQ01.1`: "I experienced joy.". With answer options 1 = completely disagree to 5 = completely agree.
- `FQ01.2`: "I was proud.". With answer options 1 = completely disagree to 5 = completely agree.
- `SB01.1` to `SB01.6`: boredom items. With answer options 1 = completely disagree to 5 = completely agree.
- `VL01.1` to `VL01.5`: value items. With answer options 1 = completely disagree to 5 = completely agree.
- `MO01.1` to `MO01.4`: motivation items. With answer options 1 = completely disagree to 5 = completely agree.
- `CO01.1` to `CO01.5`: overchallenge items. With answer options 1 = completely disagree to 5 = completely agree.
- `CO02.1` to `CO02.5`: underchallenge items. With answer options 1 = completely disagree to 5 = completely agree.
- `group`: study group or condition, which was not used and is therefore empty.

The repeated questionnaire structure supports longitudinal analyses at the within-person level. Each participant may contribute multiple rows, with one row per completed session.

## Prepared analysis data

File: `MPLUS_scale_ordered_intervals.dat`

This file is the prepared long-format dataset used for Mplus models. It was generated by aggregating the repeated item responses into scale means and ordering observations by participant and time.
For thar the data_prep.R was used which can be found alongside the other code in the GitHub repo: https://github.com/LukasKraiger/Yoga-boredom

Variables in the prepared dataset:

- `userId`: participant identifier
- `BO`: boredom scale mean
- `VA`: value scale mean
- `OC`: overchallenge scale mean
- `UC`: underchallenge scale mean
- `MO`: motivation scale mean
- `intervaldays`: number of days since the previous measurement occasion; the first observation for each participant is coded as 0

## GitHub Repository contents (https://github.com/LukasKraiger/Yoga-boredom)

- `data_prep.R` — prepares the raw CSV files and creates the Mplus-ready dataset
- `Figure 1 Violin Plot.R` — reproduces the violin plot figure from the prepared dataset
- `indirect_effect.R` — extracts Mplus estimates and computes indirect effects
- `mediation_RDSEM_H1_intervall.inp` — model H1
- `mediation_RDSEM_H2_intervall.inp` — model H2
- `mediation_RDSEM_H3_intervall.inp` — model H3
- `mediation_RDSEM_H4_intervall.inp` — model H4
- `mediation_RDSEM_H5_OC_intervall.inp` — model H5 for overchallenge
- `mediation_RDSEM_H5_UC_intervall.inp` — model H5 for underchallenge
- `mediation_RDSEM_H5_VA_intervall.inp` — model H5 for valence
- `levels_of_boredom_new.inp` — additional boredom-level model

## Requirements

To run the code, you need:

- R (4.x or newer recommended)
- Mplus
- R packages:
  - `misty`
  - `MplusAutomation`
  - `officer`
  - `flextable`
  - `dplyr`
  - `lubridate`
  - `tidyr`
  - `ggplot2`


## How to run this
# Data

The data files are hosted on the project's Zenodo record and the code is in the
GitHub repository. To regenerate the prepared analysis dataset, download these
two raw questionnaire files and place them in `Data/raw/` in the repository
root:

- `baseline.csv`
- `post_session.csv`

Create the `Data/raw/` folder if it does not already exist. Then, from the
repository root, run:

```bash
Rscript data_prep.R
```

This creates `Data/MPLUS_scale_ordered_intervals2.dat`, the prepared dataset
used by the Mplus models and figure script. The generated dataset is not
tracked in Git.

To skip data preparation, download `MPLUS_scale_ordered_intervals2.dat` from
Zenodo directly into `Data/`.


## Data processing workflow

The script `Code/data_prep.R` performs the following steps:

1. Reads the raw CSV files from `Data/raw/`
2. Excludes administrative or test participants
3. Retains only participants with at least two repeated post-session observations
4. Sorts responses by participant and time
5. Computes scale means for the repeated measurement instruments
6. Exports the Mplus-ready file `MPLUS_scale_ordered_intervals2.dat` plus an Mplus input file.

The prepared file is intended to be a reproducible analysis dataset rather than a raw export.

### Reproduce the figure

From the repository root, run:

```bash
Rscript "figure_1_violin_plot.R"
```

This script runs the data_prep.R script and will create the figure output in the repository root.

### Run the Mplus and indirect-effect analyses

Run the relevant `.inp` files in Mplus with the repository root as the working
directory, then estimate indirect effects from the repository root with:

```bash
Rscript indirect_effect.R
```

## Notes

- The scripts are written with English comments to support reuse and adaptation.
- Paths are relative to the repository root.
- The figure script depends on the prepared data file generated by `data_prep.R`.

## Data protection note

The study data use a pseudonymous participant identifier (`userId`) to link repeated measurements within participants.
