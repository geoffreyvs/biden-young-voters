# biden-young-voters
Goal is to have a chart that has the approval, disapproval and DK/Not sure data for 18-29s (or at least the first two).

Steps in the code:

1. Takes crosstab data from the FiveThirtyEight database (final date is in file name for crosstab data "skelley.BIDEN-YOUNG-VOTERS.0727 - app_crosstab_through[date]"), and then filters that data to include just the crosstab data by age groups. This includes bringing in the Harvard IOP Youth Poll for 18-29s as added data points. During this section, I also bring in a file with the day of the presidency for Biden so that I can calculate fit lines later on (calculating fit won't work with dates in mdy format as the x variable).

2. Brings in overall approval poll data to match up overall N of full poll with the crosstab age data. This is so that for instances where we don't have a sample size, I can estimate the sample size based on the relevant Current Population Survey data point for the age group in question (which I also bring in here). I then separate the polls that have sample sizes from those that don't and calculate estimated sample sizes for the latter. I then recombine the data points. We then use `slice` to get rid of a handful of polls where there is both aregistered voters and adult observation so we don't have multiple data points from the same poll.

3. I then filter for just the 18-29 age group, `gather` that data to put it into long form so I can group by approve (yes), disapprove (no) and the alternate answers (alternate_answers). I then have a ggplot chart of what this looks like with fit lines.

4. I then create the fit line estimates that show up in that chart using `loess` and `predict` for all three categories. The chart created from those estimates matches the fit lines in the ggplot version.
