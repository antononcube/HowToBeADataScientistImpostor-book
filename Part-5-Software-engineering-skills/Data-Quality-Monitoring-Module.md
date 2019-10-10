# Data Quality Monitoring Module Design


## Introduction

In this chapter we discuss the design of data quality monitoring software module. 
The module design and programming has the following mission statement.
 
> Make a software module that verifies assumptions and required properties of 
certain data and provides reports of data's evolution (or changes in time.)

## Design

At least one programming language -- Raku Perl 6 -- can interpret the code specifications below.
 
### Monadic design

Consider the following pipeline example of progressively more difficult tests to pass.
    
        DQMonUnit() ==>
        DQMonVerifyDataPresense( directory-path, file-names ) ==>
        # DQMonVerifyDataPresense( database, table-names ) ==>
        DQMonVerifyDataShape( shape-spec ) ==>
        DQMonCheckDataSize( size-expectations ) ==>
        DQMonCheckMissingValues( NA-expectations ) ==>
        DQMonVerifyLongFormConversion( eventRecordsSpec, entityAttributesSpec ) ==>
        DQMonConvertToLongForm( eventRecordsSpec, entityAttributesSpec ) ==>
        DQMonVerifyVariableDistributions( var-dist-pairs | var-values ) ==>
        DQMonCheckOutlierPresense( outliers-expectations ) ==>
        DQMonSnapshotReport ( file-path )
        
An alternative is to use predefined overall specification.
    
        DQMonUnit( data-quality-spec ) ==>
        DQMonVerifyDataPresense ==>
        DQMonVerifyDataShape ==>
        DQMonCheckDataSize ==>
        DQMonCheckMissingValues ==>
        DQMonVerifyLongFormConversion ==>
        DQMonConvertToLongForm ==>
        DQMonVerifyVariableDistributions ==>
        DQMonCheckOutlierPresense ==>
        DQMonSnapshotReport
        
that can be contracted into:
    
        DQMonUnit( data-quality-spec ) ==>
        DQMonExecuteStandardVerificationPipeline
        
There are several ways to provide the functionalities behind the monadic pipeline(s) above.

Using Design Patterns like Template Method and Strategy can provide the desired architectural properties.

**Remark:** Each of the pipelines above is "on the spot" written code for Template Method's `abstractAlgorithm`.

**Remark:** All pipeline segments are "*verbs*".

### Repeated execution

The monadic pipelines shown above would be repeatedly executed over a certain time regular grid.
    
        DQMonUnit( data-quality-spec ) ==>
        DQMonExecuteStandardVerificationPipeline( execution-time-grid )
        
The monad object above is observed with Model View Controller pattern.

Here is an observer pipeline (with the same monad):
    
        DQMonUnit( data-quality-spec, reports-location ) ==>==>
        DQMonRetrieveSnapshotReports ==>
        DQMonComputeScoreEvolutionStatistics ==>
        DQMonPlotScoreRadarChart ==>
        DQMonPlotScoreTimeSeries ==>
        DQMonScoreEvolutionReport( file-path )

### The monadic error object

Typically in monad pipelines we just return and error symbol with something is wrong.

For this pipeline the verification errors produced by the monad functions are outcomes that have to be reported.
Hence, the monad object itself keeps the various types of verification errors and observations as object members.

It might be a good idea to investigate the possibility of managing log files or a database for 
the verification error objects.

## Data shapes to consider

- One of the most common data shapes are CSV files or database tables with "wide form" interpretation.

- Related common data shape is Star Schema of the long form of the wide form.

- Another common data shape is shallow JSON files.
  - Key-value arrays.
  - Arrays of objects that are key-value arrays.
  - The values can be arrays.
    
For many temporal data handling Machine Learning tasks or modules the Star Schema for events 
is (most) adequate or at least an important use case in data feeding.
Hence, we should be able to test and verify Star Schema structure: 
both (1) its presence or existence, and (2) conversion to it.

## Variable distributions

- This is similar to what is done in `ERTMon`, \[2\].

- For example, the outliers counting and presence is done in `ERTMon`.

## Reporting

- TBD...

## Concrete use cases

- TBD..

## Unit testing

### How to test the module?

TBD...

### Data

TBD...

- Data generation

- Data modification

### Repeated execution

TBD...

## References

\[1\] Anton Antonov, 
["Monad code generation and extension"](https://mathematicaforprediction.wordpress.com/2017/06/23/monad-code-generation-and-extension/),
(2017),
[MathematicaForPrediction at WordPress](https://mathematicaforprediction.wordpress.com).

\[2\] Anton Antonov, 
["Parametrized event records data transformations"](https://mathematicaforprediction.wordpress.com/2018/10/05/parametrized-event-records-data-transformations/),
(2018),
[MathematicaForPrediction at WordPress](https://mathematicaforprediction.wordpress.com).