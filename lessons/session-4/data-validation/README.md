Data Validation
==============

Instructor: Will Beasley

Intro
--------------------------------

Start with the principles described in the [Validation](https://ouhscbbmc.github.io/data-science-practices-1/validation.html) chapter of [*Collaborative Data Science*](https://ouhscbbmc.github.io/data-science-practices-1).

Workbook for your Specific Project
--------------------------------

* Hammer all variables in your analysis

    * Predictors

    * Outcomes

    * Their multivariate relationships

* Consider potential confounders that aren't explicitly in your model, which may include

    * year/quarter/month of the pandemic

    * data partner ID

* Common gotcha variables

    * smoking --but this is a lot better with the LL templates

    * oxygen/ventilation/ecmo --but this is a lot better with the LL templates

    * Did the patient never have the medication or diagnosis?  Or was it never documented in a EMR that feeds N3C?

Logic Liaison's "Fact Density" Templates
------------------

* [Fact Density by Site Visualization](https://unite.nih.gov/workspace/module/view/latest/ri.workshop.main.module.3ab34203-d7f3-482e-adbd-f4113bfd1a2b?id=KO-9901C7E&view=focus)

    > This template calculates the Standardized Density, Median Absolute Deviation (MAD), and Directional Median Deviations (DMD) with respect to the numerical values in each column of the input table (any non-numerical field is converted to a binary value using the isNotNull() function) and creates heatmaps to visualize the metrics.

* [Data Density by Site and Domain](https://unite.nih.gov/workspace/module/view/latest/ri.workshop.main.module.3ab34203-d7f3-482e-adbd-f4113bfd1a2b?id=KO-C3B0BBE&view=focus)

    > This template calculates the Standardized Density, Median Absolute Deviation (MAD), and Directional Median Deviations (DMD) with respect to the number of unique patient/concept/days for each of the major OMOP tables (i.e. condition_occurrence, drug_exposure, etc) and uses them to create a heatmap displaying how many MADs each site is from the median for each OMOP table. The template also scores the site's date shifting practices.

* [Systematic Missingness by Site and Study Variable](https://unite.nih.gov/workspace/module/view/latest/ri.workshop.main.module.3ab34203-d7f3-482e-adbd-f4113bfd1a2b)

    > This LOGIC LIAISON template produces a final visualization that has a binary indicator for whether or not a site is systematically missing meaningful data for the study variables in the input dataset (defaulted to the Logic Liaison Covid-19 Patients Template)
