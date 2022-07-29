# School Analysis
The purpose of this challenge is to use pandas to determine the averages/passing % of students in reading and math.

## Overview of the School Analysis
A school board employee has given us the following tasks to analyise a set of data in a school district with a school that is suspected of altering testing data:

- How is the district summary affected when the suspect data is removed?
- How is the school summary affected when the suspect data is removed?
- How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
- How does replacing the ninth-grade scores affect the following: Math and Reading scores by grade, scores by school spending, scores by school size, and scores by school type

If any data is suspicious, the data will be removed, specifically the Math and Reading test scores for the 9th graders at Thomas High School; after this, the data will be properly filtered down and analyzed.

## Resources
The resources I used for this challenge are the students_complete.csv and schools_complete.csv files, as well as the Jupyter Notebook for the use of pandas.
## School Analysis
The first part necessary for this challenge was removing the questionable data. The Thomas High School 9th grade Math and Reading scores that fit this criteria were removed and the averages and percentages were adjusted for the remaining number of students tested. This was done by the following methods:

Using a .loc() function, the data containing "Thomas High School" (using the school_name column), "9th" (using the grade column) and the reading score column (as well as the math score) was selected and the values were repaced with NaN (Not a Number). These following snippets remove the bad data and replace them with the NaN:

student_data_df.loc[(student_data_df["grade"] == "9th") & (student_data_df["school_name"] == "Thomas High School"),["reading_score"]] = np.nan

student_data_df.loc[(student_data_df["grade"] == "9th") & (student_data_df["school_name"] == "Thomas High School"), ["math_score"]] = np.nan

Using both a .loc() function and a .count() function, the number of 9th graders at Thomas High School can be calculated and then later used to determine the total number of the rest of the students

thomas_ninth_student_count = student_data_df.loc[(student_data_df["school_name"]  == "Thomas High School") & (student_data_df["grade"] == "9th")].count()["student_name"]

Using another .count() function, the total number of students thruoghout all the schools and grades in the data are calculated:

student_count = school_data_complete_df["Student ID"].count()


All new calculations of averages and percentages will now be done using the total number of students minus those suspected of cheating: 

new_student_count = student_count - thomas_ninth_student_count

Now that the data is clean of any abnormalities, the data can be properly used for all future checks and problems.


According to the data, the school district summary shows that although the average Math Score decreased by .1, from 79.0 to 78.9 , the average Reading Score stayed the same, the percentage of students Passing Math decreased by .2%, from  the percentage of students Passing Reading decreased by .1%, from 85.8 to 85.7. Ultimately, the % Overall Passing students went down .3%, from 65.2 to 64.9.


Also according to the data, the school summary shows that with-in Thomas High School; using floating point variables rounding to the nearby tenth, the average Math Score decreased by .1, from 83.4 to 83.3, the average Reading Score increased by .1, from 83.8 to 83.9, the percentage of students Passing Math decreased by .1%, from 93.3 to 93.2, and the percentage of students Passing Reading decreased by .3%, from 97.3 to 97. Ultimately, the % Overall Passing students went down by .3%, from 90.9 to 90.6. 

Thankfully, removing the 9th grade invalid scores of Thomas High School didn't seem to influence the data very much, keeping below 1% change in all cases. Thomas does meet the criteria to become the second best school around, but only if the 9th grade scores are compared with the other classes (10th, 11th, and 12th). However, if the data was taken using all of the data, including the 9th graders, a huge shift occurs. The total percentages decrease by approximately 30%, which is a major change compared to before; this change moves Thomas from second best school into the third worst school in the district. The following is the adjusted data:

                    School type Total Students  Total Budget    Student Budget  Math  Read  %Math %Read %Overall
Thomas High School	Charter	    1635	           $1,043,130.00  $638.00	        83.4	83.9	66.9  69.7  65.1

How does replacing the ninth-grade scores affect the following:
- Math and Reading scores by grade

The data is that is not available is replaced with NaN, standing for not available, which isn't standing for the value of 0, but just an empty slot. 

- Scores by school spending

Removing the 9th graders' data doesn't alter the data too much in the spending, with the only alterations occuring in the $630-$644 per student spending range. For Thomas High School, both the % Passing Reading and the % Overall Passing decrease by .1%.

- Scores by school size

This data isn't altered too much either, only changing in the medium school size region. For Thomas High School, the % Passing Reading went down by .1%.

- Scores by school type

Thomas High School is a charter school, and the data across all charter schools does not change with the removal of the 9th grader data.

## Summary
Ultimately, the removal of the 9th graders test scores did not greatly affect the scores throughout the whole district. With a sample size of 39,100 total students, the removal of 461 students doesn't affect the data that much. While this did alter the data inside of the Thomas High School, it wasn't enough to cause major problems. In the end, although there wasn't much, there was still evidence of cheating and the necesity to remove the data, to make sure that no bad data is given for the statistics.
