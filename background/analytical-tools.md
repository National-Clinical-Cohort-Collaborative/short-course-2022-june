Analytical Tools --Background Requirements
=================

To be productive in the N3C Enclave during this short course, we recommend that you (a) are comfortable with basic SQL and (b) know at least a little Python or R.

SQL
----------------------

From https://github.com/National-COVID-Cohort-Collaborative/book-of-n3c-v1
> Almost every N3C project starts with SQL.  For the past 30 years, SQL has been the de facto language for large datasets like the N3C. It is well-suited for efficiently (a) selecting patients following exacting selection criteria, (b) joining a variety of predictor and outcome variables from multiple tables, and (c) producing a dataset better suited for analyses. Consequently it is a common ability for people in data science and IT.
>
> Our rule of thumb is to transform it in SQL if SQL can comfortable transform it. Otherwise use R or Python to transform it.

SQLBolt (<https://sqlbolt.com/>) is the easiest way to get self-started.  This website teaches and evaluates you in small manageable chunks.  Complete the first 12 lessons under "Interactive Tutorial", and then the Union lesson under "More Topics".  The later lessons are good too, but not used in N3C workflows.

If you'd like to learn the basic syntax more thoroughly, consider one of these options:

* [*Getting Started with SQL: A Hands-On Approach for Beginners*](https://www.amazon.com/Getting-Started-SQL-Hands-Beginners/dp/1491938617/) by Thomas Nield (Chapters 1-8, and Appendix A) or
* [*SQL in 10 Minutes a Day*](https://www.amazon.com/SQL-Minutes-Sams-Teach-Yourself/dp/0135182794), 5th edition by Ben Forta (Chapters 1-14, and Appendix C)

This resources above use SQLite, which is *almost* completely compatible with the flavor of SQL used in N3C.  The N3C Enclave uses Spark SQL.  During the course, refer to these sources if your code looks correct, but the "SQL Transform" throws an error:

* The [Spark SQL Guide](https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select.html) describes the flavor of SQL used in the N3C Enclave
* The [Apache Hive Manual](https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select.html) describes the mechanism underneath Spark SQL.* 
* [15 Basic And Highly Used Hive Queries that All Data Engineers Must know](https://www.analyticsvidhya.com/blog/2020/12/15-basic-and-highly-used-hive-queries-that-all-data-engineers-must-know/) by Siddharth Sonkar

Python
----------------------
Python has many resources for all levels of experience. 

Some general ones for getting started:
* [*Introduction To Python Programming (Udemy)*](https://www.udemy.com/course/pythonforbeginnersintro/?LSNPUBID=JVFxdTr9V80&ranEAID=JVFxdTr9V80&ranMID=39197&ranSiteID=JVFxdTr9V80-Hrdo.3OzB9u4kSvhJb.AqA&utm_medium=udemyads&utm_source=aff-campaign) 
* [*Python for Everybody*](https://www.py4e.com/) 

If you like Python and want to learn more, check out:
* [*Python Data Science Handbook (O'Reilly)*](https://jakevdp.github.io/PythonDataScienceHandbook/)
* [*Python for Data Science*](https://cognitiveclass.ai/courses/python-for-data-science)

R
----------------------
R also has many books for all levels of experience.  These three books are free online, as well as available as paperback.

* [*A Primer for Computational Biology*](https://open.oregonstate.education/computationalbiology/) by [Shawn O'Neil](https://som.ucdenver.edu/Profiles/Faculty/Profile/35866), one of our instructors.  Part III is dedicated to R.  Chapters 26-32 provide the basics you'll need for N3C.

If you like R and want to learn more, check out:
* [*R for Data Science*](https://r4ds.had.co.nz/) by Hadley Wickham & Garrent Grolemund
* [*Advanced R*](https://adv-r.hadley.nz/) by Hadley Wickham
