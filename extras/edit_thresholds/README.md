_TODO: test dqd results are the same, maybe try with more checks_

# Intro
This script can be used to edit selected thresholds in a DQD result. This of course assumes that you have run the DQD, observed it, and have a list of checks for which you would like a different threshold.

## About the checks
There are 20 different checks. The thresholds for these checks are recorded in one of 3 files: `Table`, `Field` or `Concept` level. This script has been tested -for now- only for the ones defined in the file `DQD_Field_Level_v5.3.1.csv`, but is supposed to be valid for the rest.
For more information about the checks and their thresholds, visit: https://ohdsi.github.io/DataQualityDashboard/articles/CheckTypeDescriptions.html

## About this script
In the aforementioned files, each check can be found using a combination of the check name itself, together with information from additional columns. In summary, the checks and additional columns are the following:

_[Please note that not all checks have been tested. If you get an error, multiple or no index for any of these checks, let me know!]_


| | Test      | Additional columns | Other |
| -- | ----------- | ----------- | ----------- |
|  | __TABLE LEVEL__ |  |  |
| 1 | measurePersonCompleteness      |   cdmTableName  |  |
|  | __FIELD LEVEL__ |  |  |
| 2| cdmField   | cdmTableName        | not present in any of the table/field/concept level control files|
| 3| isRequired   | cdmTableName, cdmFieldName        | |
<!-- | 4| cdmDatatype   | cdmTableName, cdmFieldName,cdmDatatype        | | -->
| 4| cdmDatatype   | cdmTableName, cdmFieldName        | |
| 5| isPrimaryKey   | cdmTableName, cdmFieldName        | |
| 6| isForeignKey   | cdmTableName, cdmFieldName, fkTableName        | |
| 7| fkDomain   | cdmTableName, cdmFieldName, fkDomain        | |
| 8| fkClass   | fkClass, cdmFieldName        | |
| 9| isStandardValidConcept   | cdmTableName, cdmFieldName        | |
| 10| measureValueCompleteness   | cdmTableName, cdmFieldName        | |
| 11| standardConceptRecordCompleteness   | cdmTableName, cdmFieldName        | |
| 12| sourceConceptRecordCompleteness   | cdmTableName, cdmFieldName        | |
| 13| sourceValueCompleteness   | cdmTableName, cdmFieldName        | |
<!--| 14| plausibleValueLow   | cdmTableName, cdmFieldName, plausibleValueLow        | |-->
<!--| 15| plausibleValueHigh   | cdmTableName, cdmFieldName, plausibleValueHigh        | |-->
<!--| 16| plausibleTemporalAfter   | cdmTableName, cdmFieldName, plausibleTemporalAfterFieldName, plausibleTemporalAfterTableName        | | -->
| 14| plausibleValueLow   | cdmTableName, cdmFieldName      | |
| 15| plausibleValueHigh   | cdmTableName, cdmFieldName     | |
| 16| plausibleTemporalAfter   | cdmTableName, cdmFieldName  | |
| 17| plausibleDuringLife   | cdmTableName, cdmFieldName        | |
|  | __CONCEPT LEVEL__ |  |  |
<!--| 18| plausibleValueLow   | cdmTableName, cdmFieldName, plausibleValueLow       | |-->
<!--| 19| plausibleValueHigh   | cdmTableName, cdmFieldName, plausibleValueHigh    | |-->
<!--| 20| plausibleGender   | cdmTableName, cdmFieldName, plausibleGender        | |-->
| 18| plausibleValueLow   | cdmTableName, cdmFieldName       | |
| 19| plausibleValueHigh   | cdmTableName, cdmFieldName    | |
| 20| plausibleGender   | cdmTableName, cdmFieldName    | |


## How to run?

1. Define the checks for which you want to edit the thresholds in a .csv file, like this:

| Check_name      | cdmTableName | cdmFieldName |
| isRequired | MEASUREMENT  | person_id |
| cdmDatatype | MEASUREMENT  | person_id |
| plausibleValueLow  | PERSON  | year_of_birth  |

2. Run `edit_thresholds.R` functions: `pivot_longer_func()` and  `print_threshold_location()`.

3. With the threshold 'location', or index in the long table, edit your thresholds (and notes!) as desired. _(Keep in mind that the printed value corresponds to the index. If you open the table in Excel, the row in Excel might be displaced by one because of the first row.)_

4. Run `edit_thresholds.R` function: `pivot_wider_func()` and save the resulting table, which you can use for your future analysis!

