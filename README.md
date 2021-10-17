# Pewlett-Hackard-Analysis

## Project Overview
The purpose of this analysis was to create a database and perform a detailed analysis on retirement elible employees at Pewleet Hackard. Specifically, this portion of the analysis determined the number of retiring employees by title and identified employees who are eligible to participate in a mentorship program. 

## Resources
- Data Source: departments.csv , dept_emp.csv, dept_manager.csv, employees.csv, salaries.csv, titels.csv
- Software: Visual Studio Code 1.60.1, pgAdmin 5.7, PstgreSQL 14

## Results
- The number of retiring employees by title are displayed in the following table:

![image_name](https://github.com/zackzydonik/Pewlett-Hackard-Analysis/blob/c98832d11a69dd7303f22563535c37b55592ee2a/Analysis%20Projects%20Folder/Pewlett-Hackard-Analysis%20Folder/retiring_titles.png)

- The job title with the most retirement eligble employees is Senior Engineer at 29,414 employees
- The job title with the least retiremtn eligble employees is Manager at 2 employees
- The following table breaks down the number of mentorship eligible employees. As can be seen in the table, there are no managers that are eligible for mentorship which could be a shortcoming for the company.

![image_name](https://github.com/zackzydonik/Pewlett-Hackard-Analysis/blob/c98832d11a69dd7303f22563535c37b55592ee2a/Analysis%20Projects%20Folder/Pewlett-Hackard-Analysis%20Folder/mentorship_eligibility_title.png)

## Summary
1. There 90,398 employees that are retirement eligible and will need to be filles as the "silver tsunami" begins to make an impact. This can be found using the following query.
    
        SELECT SUM(rt.count) FROM retiring_titles as rt

2. There are not enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees. As mentioned above, there are no Managers that are mentorship elibible. However, there are employees from each department that are elible for the program as shown by the following table:

![image_name](https://github.com/zackzydonik/Pewlett-Hackard-Analysis/blob/c98832d11a69dd7303f22563535c37b55592ee2a/Analysis%20Projects%20Folder/Pewlett-Hackard-Analysis%20Folder/mentorship_eligibility_department.png)

The code to generate this table is as followes:
    
        SELECT COUNT(me.emp_no), d.dept_name
        FROM mentorship_eligibility as me
        INNER JOIN dept_emp as de
        ON (me.emp_no = de.emp_no)
        INNER JOIN departments as d
        ON (de.dept_no = d.dept_no)
        GROUP BY (d.dept_name) 