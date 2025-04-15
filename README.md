# DSC 385 - Project 4 Causal Inference


## Overview

Right heart catheterization (RHC) is a diagnostic procedure for directly
measuring cardiac function in critically ill patients. In an influential
study, Connors et al. (1996) studied the effectiveness of RHC with an
observational study design. The study collected data on 5735
hospitalized adult patients; 2184 of them are assigned to the
experimental treatment, receipt of RHC within 24 hours of admission, and
the remaining 3551 assigned to the control condition. The outcome was
death at 30 days after admission to the hospital. The goal is to assess
the causal effect of RHC (the treatment) on the binary outcome, death at
30 days after admission.

The dataset provided here is a cleaned version of the original dataset.
The treatment variable in the dataset is `swang1` and the outcome
variable is `death`. To simplify the analysis, we have restricted the
data to 20 covariates that have been identified as the top confounders
in an ad-hoc exploratory analysis.

Below is a table describing each of the variables in the dataset:

<table>
<colgroup>
<col style="width: 48%" />
<col style="width: 51%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Variable Name</th>
<th style="text-align: left;">Interpretation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">age</td>
<td style="text-align: left;">Age in years</td>
</tr>
<tr class="even">
<td style="text-align: left;">sex</td>
<td style="text-align: left;">Male / Female</td>
</tr>
<tr class="odd">
<td style="text-align: left;">cat1</td>
<td style="text-align: left;">Primary Diagnosis: COPD, Multiple Organ
System Failure (MOSF) w/Sepsis, MOSF w/Malignancy, CHF, Coma, Cirrhosis,
Lung Cancer, Colon Cancer</td>
</tr>
<tr class="even">
<td style="text-align: left;">cat2</td>
<td style="text-align: left;">Secondary Diagnosis: MOSF w/Sepsis, Coma,
MOSF w/Malignancy, Lung Cancer, Cirrhosis, Colon Cancer</td>
</tr>
<tr class="odd">
<td style="text-align: left;">ca</td>
<td style="text-align: left;">yes = Cancer localized, no =
metastatic</td>
</tr>
<tr class="even">
<td style="text-align: left;">death</td>
<td style="text-align: left;">Death within 30 days after hospital
admission</td>
</tr>
<tr class="odd">
<td style="text-align: left;">pafi1</td>
<td style="text-align: left;">PaO2 / F102 ratio</td>
</tr>
<tr class="even">
<td style="text-align: left;">wtkilo1</td>
<td style="text-align: left;">Weight</td>
</tr>
<tr class="odd">
<td style="text-align: left;">surv2md1</td>
<td style="text-align: left;">Estimate of probability of surviving 2
months</td>
</tr>
<tr class="even">
<td style="text-align: left;">dementhx</td>
<td style="text-align: left;">Dementia, stroke or cerebral infarct,
Parkinsons’s disease</td>
</tr>
<tr class="odd">
<td style="text-align: left;">gastr</td>
<td style="text-align: left;">Gastrointestinal diagnosis</td>
</tr>
<tr class="even">
<td style="text-align: left;">wblc1</td>
<td style="text-align: left;">White blood count</td>
</tr>
<tr class="odd">
<td style="text-align: left;">temp1</td>
<td style="text-align: left;">Temperature</td>
</tr>
<tr class="even">
<td style="text-align: left;">das2d3pc</td>
<td style="text-align: left;">DASI-Duke Activity Status Index</td>
</tr>
<tr class="odd">
<td style="text-align: left;">chfhx</td>
<td style="text-align: left;">Congestive heart failure</td>
</tr>
<tr class="even">
<td style="text-align: left;">hema</td>
<td style="text-align: left;">Hematological diagnosis</td>
</tr>
<tr class="odd">
<td style="text-align: left;">chrpulhx</td>
<td style="text-align: left;">Chronic pulmonary disease, severe
pulmonary disease</td>
</tr>
<tr class="even">
<td style="text-align: left;">cardiohx</td>
<td style="text-align: left;">Cardiovascular symptoms</td>
</tr>
<tr class="odd">
<td style="text-align: left;">meta</td>
<td style="text-align: left;">Metabolic diagnosis</td>
</tr>
</tbody>
</table>

The goal of the project is to try to determine the effect of right heart
catheterization on 30-day mortality using data from an observational
study. In doing so, you will use propensity score matching to reduce the
potential impact from confounding variables.

## Getting the Data

The data can be obtained from the following GitHub repository:

`https://github.com/Principles-of-Data-Science/Project4`

You can pull the GitHub repository into RStudio as follows:

1.  Click on File \> New Project…

2.  Click on “Version Control”

3.  Click on “Git”

4.  Paste in the URL
    **https://github.com/Principles-of-Data-Science/Project4** into the
    “Repository URL” field

5.  Type in the “Project directory name” if needed

6.  Set the directory if you don’t want to use the default

7.  Click “Create Project”

## The Report

The text of your report will provide a narrative structure around your
code and outputs with R Quarto. Answers without supporting code will not
receive credit and outputs without comments will not receive credit
either. Write full sentences to describe your findings. All code
contained in your final project document must work correctly (render
early, render often)!

**The report template provided in the GitHub repository contains
prompts/questions that you will need to answer. Please follow the
prompts in the template and answer all of the questions there.**

### Formatting

-   Create the report using R Quarto knitted to a PDF file, with headers
    for each section and each question answered;

-   Include comments describing your R code;

-   Include any references (datasets, context), if needed.

-   Please do not print out very large objects that require multiple
    pages; only print out what is needed to explain your reasoning for a
    question.

-   It is extremely important that you **select pages** when submitting
    on Gradescope (see more below). Points will be taken off if you do
    not select the appropriate pages for each question in the Gradescope
    outline.

## Submission of the Report to Gradescope

This project report will be submitted on Gradescope for grading.
Gradescope is a tool that enables the teaching staff to efficiently
grade assignments like this one according to a defined rubric. **You
will not be submitting this project on Canvas**. Anything submitted to
Canvas will be ignored.

If you have never submitted anything to the Gradescope web site, please
watch this [video demonstration of how to do
so](https://youtu.be/nksyA0s-Geo?si=nSsG145iOgjyauVf).

To submit your project report, please follow these steps:

1.  First render your project report into a PDF file. This can be done
    by either rendering directly to PDF in RStudio or by rendering to an
    HTML file and then “Printing” to a PDF file. Either way, **you must
    have a PDF file to submit to Gradescope**.

2.  Go to the course Canvas page and click on the “Gradescope” link on
    the navigation bar on the left hand side.

3.  When the Gradescope page loads, click on the assignment titled
    “Project 3: Prediction Modeling”.

4.  You should be prompted with a window allowing you to submit a PDF
    file of your assignment.

5.  After uploading your PDF file, you will be prompted to select pages
    of your PDF file that correspond to questions in the “Question
    Outline”. Please make sure to do this carefully, as it essential for
    allowing us to grade your project efficiently.

6.  After selecting the pages, submit the assignment.

## Late Policy

As per the Syllabus, projects will not be accepted late. There are no
exceptions; please do not contact the instructor or TA to request an
exception.
