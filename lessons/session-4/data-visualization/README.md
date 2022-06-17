Data Visualization
===========================

Instructor: Will Beasley

Steps
--------------

1. In your personal folder on Enclave, create workbook called "graphs-1" in "session-4/"

1. Import data from Jerrod's lesson

    * From "Short Cource/ Student Worksapces/anzalone_j/session_3/workbook-output/Covid-19 patient summary fact table De-Id".
  
    * I prefer you use Jerrod's (instead of your own), so we're consistent.

1. Create a SQL transform called `pt_thinned`

    * I like when the transform name clearly indicates the [grain](https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/dimensional-modeling-techniques/grain/) of the resulting table.

    * Toggle "Save as dataset".

    * Temporarily trim to 5% of the 100k patients so our graphs are quicker during development.  Later on, remove the thinning and use everyone.  This strategy is common in stats (*e.g.* Andrew Gelman's advise in multilevel modeling).

    * Select the variables you need.  It reduces teh thigns that can go wrong.  Be stingy.  You can add more later.

    * code:

        ```sql
        SELECT 
            data_partner_id
            ,year(COVID_first_PCR_or_AG_lab_positive) as covid_year
            ,cast(age_at_covid as int)                as age_at_covid
            ,Severity_Type                            as severity_type
        FROM Covid_19_patient_summary_fact_table_De_Id
        WHERE 
            cast(right(person_id, 2) as int) between 0 and 4
        ```

1. Create an R transform called `year_age_boxplot_1`

    * Toggle "Save as dataset".

    * Iterate in the console.  What can we improve?

    * Starting code

        ```r
        year_age_boxplot_1 <- function (pt_thinned) {
            # Execute the `library()` lines separately from the others --when debugging in the console (ctrl+shift+enter).
            library(magrittr)
            library(ggplot2)

            if (class(pt_thinned) != "data.frame") {
              stop("The incoming dataset is NOT an R data.frame.")
            }

            ds <-
                pt_thinned %>%
                tibble::as_tibble() %>%
                dplyr::select(
                    age   = age_at_covid,
                    year  = covid_year,
                ) %>%
                dplyr::mutate(
                    # age   = as.integer(age), # Cast from a 64-bit to 32-bit integer
                    year_f  = factor(year)
                )

            g <-
                ggplot(ds, aes(x = year_f, y = age)) +
                geom_boxplot()
            
            print(g)

            # Return something, preferrably the dataset underneath the graph.
            #    Don't end with `print()`.
            return (ds)
        }
        ```

1. Create an R transform called `year_severity_1`

    * Toggle "Save as dataset".

    * Iterate in the console.  What can we improve?

    * Starting code

        ```r
        year_severity_1 <- function (pt_thinned) {
            
            # Execute the `library()` lines separately from the others --when debugging in the console (ctrl+shift+enter).
            library(magrittr)
            library(ggplot2)

            if (class(pt_thinned) != "data.frame") {
                stop("The incoming dataset is NOT an R data.frame.")
            }

            ds_year_severity <-
                pt_thinned %>%
                tibble::as_tibble() %>%
                dplyr::select(
                    data_partner_id,
                    year              = covid_year,
                    severity_type,
                ) %>%
                dplyr::mutate(
                    year_f  = factor(year)
                ) %>%
                dplyr::group_by(year_f, severity_type) %>%
                dplyr::summarize(
                    pt_count       = dplyr::n(),
                    partner_count  = dplyr::n_distinct(data_partner_id),
                ) %>%
                dplyr::ungroup()

            g <-
                ds_year_severity %>%
                ggplot(aes(x = severity_type, y = pt_count)) +
                geom_bar(stat = "identity") +
                facet_wrap("year_f")

            print(g)

            # Return something, preferrably the dataset underneath the graph.
            #    Don't end with `print()`.
            return (ds_year_severity)
        }
        ```

1. Once things are stable, remove the thinning code in `pt_thinned`, and rename it to something like `pt`.  It's a little tedious, but reduces your chance of forgetting.

1. Once you're comfortable with the basics, here are some tools & techniques to help you manage the complexity & volume

    * Tweaking the Spark Environment, including adding R packages.

    * [Saving an R object](https://unite.nih.gov/workspace/documentation/product/code-workbook/r-raw-file-access) that was the result of an expensive calculation.  Calculate it once, and let multiple downstream R transforms focus on a smaller role.

    * "Global Code", such as

        ```r
        load_packages <- function () {
          library(magrittr)
          library(ggplot2)
          library(survey)
        }

        predictors_1  <- "asthma * tx + smoking_ever + bmi_cut6 + gender_male + race_v2"

        tidy_model <- function (m, model_title) {
          m %>%
            broom::tidy() %>%
            dplyr::mutate(
              model = model_title
            ) %>%
            tibble::as_tibble() %>%
            dplyr::mutate_if(is.numeric, round, 5)
        }

        palette_dark <- c( # http://colrd.com/image-dna/29746/
        "(Intercept)"     = "gray50",   # Same color as reference group below
        "none documented" = "gray50",
        "saba"            = "#bfa9c4",  # lavender
        "nasal"           = "#45a79e",  # green
        "inhaled"         = "#bfc269",  # yellow green
        "systemic"        = "#f46b4f",  # orange
        "biologic"        = "#4287f5",  # blue
        "both"            = "#646596",  # purple
        )

        palette_light <- scales::alpha(palette_dark, alpha = .5)
        ```

Resources
--------------

* [ggplot2 website](https://ggplot2.tidyverse.org/reference/)

* [*ggplot2: Elegant Graphics for Data Analysis*](https://www.amazon.com/ggplot2-Elegant-Graphics-Data-Analysis/dp/331924275X/) by Hadley Wickham

* [*R Graphics Cookbook, 2nd edition*](https://r-graphics.org/) by Winston Chang

* See [N3C resources](../../../background/assets.md) we've listed, especially

    * The [Languages Section](https://unite.nih.gov/workspace/documentation/product/code-workbook/languages) in the Palantir Foundary/Enclave documentation

    * [N3C Training](https://unite.nih.gov/workspace/slate/documents/training)
