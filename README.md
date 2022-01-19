
## **Overview**

The purpose of this analysis was to prepare tables for the School Board summarizing certain requested statistics for various schools. 

**NOTE**: During the analysis, it came to our attention that reading and math grades for 9th Graders at Thomas High School showed evidence of academic dishonesty. In order to provide as clear and accurate a picture as possible, the School Board asked us to modify our code and findings in order to disregard scores attributable to 9th Graders at Thomas High.

In order to accomplish this, we made the following changes:

- We first had to replace all grades for 9th Graders at Thomas High with Null Values. This was accomplished as follows:

- Next, we had to modify our student counts to exclude these students for future calculations. This was accomplished as follows:


- Lastly, we had to make modifications to the Per School Summary Table by replacing our existing calculations for Thomas High School with results that excluded 9th graders, but included all of the other grades. This was accomplished as follows:

# Step 6. Get all the students passing math from THS

thomas_passing_math = thomas_df[(thomas_df["math_score"] >= 70)].count()["student_name"]

```


```python
# Step 7. Get all the students passing reading from THS

thomas_passing_reading = thomas_df[(thomas_df["reading_score"] >= 70)].count()["student_name"]

```


```python
# Step 8. Get all the students passing math and reading from THS

thomas_overall_passing = thomas_df[(thomas_df["math_score"] >= 70) & (thomas_df["reading_score"] >= 70)].count()["student_name"]


```


```python
# Step 9. Calculate the percentage of 10th-12th grade students passing math from Thomas High School. 

thomas_math_percentage = float(thomas_passing_math) / float(count_thomas) * 100
```


```python
# Step 10. Calculate the percentage of 10th-12th grade students passing reading from Thomas High School.

thomas_reading_percentage = float(thomas_passing_reading) / float(count_thomas) * 100
```


```python
# Step 11. Calculate the overall passing percentage of 10th-12th grade from Thomas High School. 

thomas_overall_percentage = float(thomas_overall_passing) / float(count_thomas) * 100
```


```python
# Step 12. Replace the passing math percent for Thomas High School in the per_school_summary_df.

per_school_summary_df.loc[["Thomas High School"], ["% Passing Math"]] = thomas_math_percentage
```


```python
# Step 13. Replace the passing reading percentage for Thomas High School in the per_school_summary_df.

per_school_summary_df.loc[["Thomas High School"], ["% Passing Reading"]] = thomas_reading_percentage
```


```python
# Step 14. Replace the overall passing percentage for Thomas High School in the per_school_summary_df.

per_school_summary_df.loc[["Thomas High School"], ["% Overall Passing"]] = thomas_overall_percentage
```



## Results

What follows is a before and after comparison of our results using the changes noted above:

- Overall Summary of Total Students, Total Budget, Average Scores, and Passing Rates for All Schools Within the District:


- Per-School Summary (Top 5 Schools) of Total Students, Total Budget, Per Student Budget, Average Scores and Passing Rates: 

- Table of Math Scores By Grade:

- Table of Reading Scores By Grade:

- Table of Average Scores and Passing Rates Based on Per Capita Spending

- Table of Average Scores and Passing Rates Based on School Size

- Table of Average Scores and Passing Rates Based on School Type


## **Summary**

As you can tell from the before and after images above, there were no significant changes once we modified the scores between to account for the aforementioned academic dishonesty. 

Perhaps the biggest change was for both the Math Scores table and Reading Scores table above. As you can see in the images, 9th Grade Scores for Thomas High School are showing up as NAn, as these are being excluded from the analysis per the above. In the old version, average Math Scores for 9th Graders and Thomas High were 83.6, and average Reading Scores were 83.7.

Additionally, there were very minor changes in the District Summary report (the first one discussed in the bullets above). Specifically, under the original analysis, the average math and reading scores were 79.0 and 81.9, respectively. Under the new analysis, Math Scores changed slightly to 78.9. Again, due to rounding, the impact is negligible. 

Lastly, whereas Thomas High's position as the number two performing overall school did not change, some of the numbers (as evidenced in the image above) changed. As an example, whereas the previous Overall Passing Percentage was 90.48012%, the new percentage became 90.630324. There were similar changes in every category.
