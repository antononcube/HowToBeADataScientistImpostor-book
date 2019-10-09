
# Introduction

This chapter outlines motivation and concrete steps to make the data used by data scientists 
more usable, accessible, consistent and trustworthy.

The point of view taken in this chapter is that data should be seen as **a primary deliverable**.

Here is a list of related concepts:

- [Data Governance](https://en.wikipedia.org/wiki/Data_governance),

- [Data Stewardship](https://en.wikipedia.org/wiki/Data_steward),

- [Data Quality](https://en.wikipedia.org/wiki/Data_quality),

- [Data Curation](https://en.wikipedia.org/wiki/Data_curation).

## Data governance maturity models

I do not want to expand or emphasize too much on the
[Data Governance](https://en.wikipedia.org/wiki/Data_governance)
maturity models, but at some point any organization making or processing Data Science products has to adopt one of them.

I think the best one to start with (simple and serviceable) is the IBM Data Governance Maturity Model.
See the article:
["Getting started with data governance"](ftp://public.dhe.ibm.com/software/data/sw-library/ii/whitepaper/LIW14003USEN.pdf).

# Data as a primary deliverable

## Motivation

The pre-processed data we use for doing Machine Learning algorithms can be seen as a product by itself.

Using that perspective will bring desired qualities of operational datasets and related processes.

## Data governance

The following questions belong to the Data Governance domain.

- Who is responsible for gathering or collecting the data?

- Who is responsible for converting the data into a tractable, coherent, **operational dataset**?

    - This dataset is comprised of data base tables and relationships, and corresponding metadata descriptions.

- Who is responsible for the quality of the operational dataset?

- Who is responsible for the quality of the data?

- Who is responsible for the consistent interpretation of the data?

  - This includes:
    - measure units of the quantities/variables,
    - expected correlations,
    - expected laws (from Physics, Accounting, Economics, etc.)

- Replace "who" above with "which process" or "which tools".

## Data stewardship and data quality

- We want to ensure that have processes and protocols that turn data
  gathered from tenants into operational datasets.
   
- At least we should have clear checklist of going through the "standard" steps.

- For each triplet of tenant, data, and operational dataset, we should
  have clear outline of how the operational dataset is going to be used
  to achieve what goals.

## Concrete steps

### Gather data from the client

The meetings with the client and related "data transactions" should be documented.

### Evaluate data ingredients

After each meeting with the tenant or significant data pre-processing
and transformations milestone evaluate and document what the data
elements are about and "tell us."

### Form a sense of data ownership

The following questions outline typical prelimiary data analysis that helps build 
a sense of data ownership.

- What the data describes?

- How many files or tables in the database?

- Is the data tabular, or unstructured, or both?

- Are credentials for data access needed?

  - If yes, how do we get access?

- What are the sizes of the tables or files?

- If the data is tabular, how many rows and columns are expected?

- How many missing values are expected (overall, per table or file)?

- Are there expected, known, or prescribed limits and boundaries for the data values?

  - For example, heart rate in medical data is expected to be between 0 and 220 beats per minute. 

### Make a data package

Make a data package for one of the common technological computations systems.
These include: Java, R, Python, or Perl.

The data package should have following elements.

1. Code scripts for transforming tenant's data into the target operational dataset.

2. The actual operational dataset or a subset of it.

3. Documentation of the data assumptions and invariants.

    - The documentation can be comments in code scripts or explanationsin notebooks.

4. Unit tests to ensure the following expectations.

   1. Expectations about the data ingestion and processing.

   2. Expectations about tenant's data.

   3. Expectations about the obtained operational dataset.

**All package elements listed above are mandatory.**
That includes the three types of unit tests listed.

Further points follow.

- Use source version control system for the data package.

  - Something like GitHub.

  - For each commit make informative descriptions if the data ingestion 
    or data transformations are significantly changed.

  - Needless to say, run the unit tests before each commit.

- The data package should have help pages for the different dataelements or functions.

- All of the points above are illustrated in the concrete examples described in the next section.

Article discussing data packages making are given in the references section.

### Project management

Because we take "data as a primary product" we can employ and of
standard tools for project management and scheduling.

For example, we can do all of the following:

- schedule Agile tasks,

- do code and data reviews,

- follow work-plan completion lists.

## Concrete example

The R package "MathematicaVsRData", \[4\] is a full blown example.

## References

\[1\] ["Put your data in an R package"](https://grasshoppermouse.github.io/2017/10/18/put-your-data-in-an-r-package/).

\[2\] ["Creating and Using Data Packages in R"](http://okfnlabs.org/blog/2018/02/14/datapackages-in-r.html).

\[3\] ["Taking your data to go with R packages"](http://www.davekleinschmidt.com/r-packages/).

\[4\] Anton Antonov,
[MathematicaVsRData R package](https://github.com/antononcube/R-packages/tree/master/MathematicaVsRData),
(2019),
[R-packages at GiHub](https://github.com/antononcube/R-packages).