# Problem Statement

Analyze statewide participations after the new SAT format was released in March 2016. Find out states with lower-than-expected SAT participation rates and make recommendations to improve SAT participation rates as an employee of the College Board.

# Executive Summary

**Examine SAT participation in 51 states using datasets from 2017 and 2018**

### Contents:
 - 2017 Data Import & Cleaning
 - 2018 Data Import and Cleaning
 - Exploratory Data Analysis
 - Data Visualization
 - Descriptive and Inferential Statistics
 - Outside Research
 - Conclusions and Recommendations

# Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state             |object |final|The different states in USA participating in ACT & SAT|
|act2017_part_rate |float  |final|The percent of participation in ACT 2017 by state           |
|act2017_eng       |float  |final|The mean score of English in ACT 2017 by state               |
|act2017_math      |float  |final|The mean score of Mathematics in ACT 2017 by state           |
|act2017_read      |float  |final|The mean score of Reading in ACT 2017 by state               |
|act2017_sci       |float  |final|The mean score of Science in ACT 2017 by state               |
|act2017_com_score|float  |final|The composite score of English, Mathematics, Reading and Science in ACT 2017 by state|
|sat2017_part_rate |float  |final|The percent of participation in SAT 2017 by state             |
|sat2017_erw       |int    |final|The mean score of Evidence-Based Reading and Writing in SAT 2017 by state|
|sat2017_math      |int    |final|The mean score of Mathematics in SAT 2017 by state           |
|sat2017_total_score|int   |final|The total score of Evidence-Based Reading and Writing; and Mathematics in SAT 2017 by state|
|act2018_part_rate |float  |final|The percent of participation in ACT 2018 by state            |
|act2018_com_score |float  |final|The composite score of English, Mathematics, Reading and Science in ACT 2018 by state|
|act2018_eng       |float  |final|The mean score of English in ACT 2018 by state                |
|act2018_math      |float  |final|The mean score of Mathematics in ACT 2018 by state           |
|act2018_read      |float  |final|The mean score of Reading in ACT 2018 by state               |
|act2018_sci       |float  |final|The mean score of Science in ACT 2018 by state               |
|sat2018_part_rate  |float  |final|The percent of participation in SAT 2018 by state            |
|sat2018_erw        |int   |final|The mean score of Evidence-Based Reading and Writing in SAT 2018 by state|
|sat2018_math       |int    |final|The mean score of Mathematics in SAT 2018 by state           |
|sat2018_total_score|int   |final|The total score of Evidence-Based Reading and Writing; and Mathematics in SAT 2018 by state|

# Conclusions:

1.	States that show 100% SAT participation in 2017 and 2018 have mandated state-wide SAT testing.
2.	States that showed increase to near 100% SAT participation in 100% is because it became compulsory for students to take SAT in 2018.
3.	SAT Total Scores and SAT Participation rate have a negative correlation. This is because state-wide testing includes all students and all of them may not be applying to college.

# Recommendations:
1.	Encourage states to make SAT a state-wide testing requirement. When SAT is a compulsory requirement and is free, participation rates will increase.
2.	Promote [SAT School Day](https://www.testive.com/state-sat-act/) to improve SAT participation rates even if the state is not mandated to take this test. The SAT School Day is convenient for students to take the test in school on a weekday than and provides free tests to low-income students.
3.  Market SAT as an additional test for College-bound students increase their competitiveness in college applications.

### Given Sources:

1.	[SAT](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/)
2.	[ACT](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-lows)

### Additional Sources:
1.	[SAT School Day](https://www.testive.com/state-sat-act/)
