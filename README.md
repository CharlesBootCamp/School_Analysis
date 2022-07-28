# School Analysis
Module 4 PyCity Schools with Pandas

##Overview of the School District Analysis
A school board employee has given us the following tasks to analyise a set of data in a school district with a school that is suspected of altering testing data. The suspect data will be removed, specifically the Math and Reading test scores for the 9th graders at Thomas High School, and the impact on the overall data will be analysed.

How is the district summary affected when the suspect data is removed?
How is the school summary affected when the suspect data is removed?
How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
How does replacing the ninth-grade scores affect the following:
Math and Reading scores by grade
Scores by school spending
Scores by school size
Scores by school type
Resources
Data Source: students_complete.csv, schools_complete.csv
Software: Jupyter Notebook, 6.3.0
School District Analysis
The initial set up for this analysis was scrubbing the suspect data from the data set. Specifically the testing scores for math and reading in the 9th grade at Thomas High School were removed and the averages and percentages were adjusted for the remaining number of students tested. This was accomplished with the following steps:

Using a .loc() function, the data containing "Thomas High School" (in the school_name column), "9th" (in the grade column) and the whole reading score column (and math score in the second string of code) was selected and the values were repaced with NaN (Not a Number). This removes the suspect scores with-out setting the scores to 0 and incorrectly skewing the data.
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"), "reading_score"] = np.nan
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"), "math_score"] = np.nan
Using a .loc() function and a .count() function, the total students that contain the data "Thomas High School", and "9th" are counted.
thomas_ninth_student_count = student_data_df.loc[(student_data_df["school_name"]== "Thomas High School") & (student_data_df["grade"] == "9th")].count()["student_name"]
Using a .count() function, the total number of students are counted across the whole data set.
student_count = school_data_complete_df["Student ID"].count()
Seting the new count of students, that will be used in all subsequent calculations of averages and percentages. The total number of students, minus the suspect names, is equal to the new student count.
new_student_count = student_count-thomas_ninth_student_count
Now that the suspect data has been removed and the new count of valid students has been calculated, the analysis of how this has affected the total outcomes can be studied.

How is the district summary affected?
The modified summary shows that District wide, the Average Math Score decreased by .1, the Average Reading Score stayed the same, the percentage of students Passing Math decreased by .2%, the percentage of students Passing Reading increased by .1% and the percentage of students passing both Math and Reading decreased by .3%. The adjusted summary is the upper graphic, and the original is the lower. modified summary original summary
How is the school summary affected?
The modified summary shows that with-in Thomas High School, the Average Math Score decreased by .06, the Average Reading Score increased by .05, the percentage of students Passing Math decreased by .09%, the percentage of students Passing Reading decreased by .29%, and the percentage of students Passing both Math and Reading decreased by .31%. The adjusted summary is the upper graphic, and the original is the lower graphic. adjusted school summary original school summary
How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
Removing the 9th graders' scores did not affect the performance of Thomas High School in a very large degree. It is still in the second best school by overall passing percentage. However this is only the case if the scores are compaired against the number of the valid test scores (just the 10th, 11th and 12th grade students.)
If the scores were to be calculated against all of the students attending Thomas High School (including the 9th graders), the change is significant. The precentage of students passing any subject and overall, is decreased by almost 30%, and Thomas High School moves from the second best school by overall passing to the third worst. This data is provided as a theoritical, the overall data has been corrected to show the percentages by valid test scores and students only. cheaters get caught
How does replacing the ninth-grade scores affect the following:
Math and Reading scores by grade
The data is simply shown as NaN, Not a Number. This does not represent a 0, just "null value", an empty cell. math score by grade reading score by grade
Scores by school spending
Removing the 9th graders' scores effectivly does not affect the data. Thomas High School falls into the $630-$644 per student spending range, and the value of the percentage of students Passing Reading and the percentage of students passing both Math and Reading decrease by .1%. The adjusted data is the upper graphic. school spending adj school spending orig
Scores by school size
Removing the 9th graders' scores effectivly does not affect this data either. Thomas High School falls into the Medium (1000-2000) school size range, and the value of the percentage of the Students Passing Reading decreases by .1%. The adjusted data is the upper graphic. school siza adj school size original
Scores by school type
Thomas High School is a charter school. Across all charter schools, the data is not affected by removing the scores of the 9th graders. charter adj charter orig
Summary
Removing the 9th graders test scores did not greatly affect the scores over the whole district, at most .4% of a percentage point. The sample size is simply too great (39100 total students) for the removal of 461 scores to make a large impact. This did affect Thomas High Schools' individual percentage scores, with-in the school, but not by a large enough margin to greatly affect the scores. That being said, it is still academic dishonesty, as well as fraud to mis represent the test scores to the school board to artificially increase the scores at Thomas High School.
