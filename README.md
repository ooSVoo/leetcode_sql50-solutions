# leetcode_sql50-solutions
this contains the solution list for leetcode SQL50 Module.

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

1. Problem - Recyclable and Low Fat Products ( 1757 )

solution - 
Select product_id from Products where low_fats = "Y" and recyclable = "Y" ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

2. Problem - Find Customer Referee (584)

Solution - 
Select name from Customer where not referee_id = 2 or referee_id is NULL;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

3. Problem - Big Countries (595)

Solution - 
Select Name , Population , area from World 
where area >= 3000000 or population >= 25000000 ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

4. Problem - Article Views 1

Solution - 
select DISTINCT author_id as id from Views
where viewer_id = author_id 
order by id ; 
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

5. Problem - Invalid Tweets (1683)

Solution - 
select tweet_id from Tweets
where LENGTH(content) > 15 ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

6. Problem - Replace Employee ID with the Unique Identifier (1378)

Solution - 
select unique_id , Name from  Employees
left join EmployeeUNI on Employees.id = EmployeeUNI.id ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

7. Problem - product Sales Analysis 1 (1068)

Solution - 
Select product_name, year, price from sales
inner join product on sales.product_id = product.product_id ; 
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

8. Problem - Customer Who visited but did not make any transactions (1581)

Solution - 
select v.customer_id, count(v.visit_id) as count_no_trans from Visit V
left join transactions T on v.visit_id = T.visit_id
where t.transactoin_id IS NULL
group by V.customer_id ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

9. Problem - Rising Temperature (197)

Solution - 
SELECT w1.id from Weather w1, Weather w2
WHERE w1.Temperature > w2.Temperature
and datediff(w1.recordDate, w2.recordDate) = 1 ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

10. Problem -  Average Time of Process per Machine (1661)

Solution - 
SELECT s.machine_id, ROUND(AVG(e.timestamp - s.timesatamp),3) as processing_time from activity s
JOIN Activity e on s.machine_id = e.machine_id AND s.process_id = e.process_id AND s.activity_type = "start" and e.activity_type = "end"
GROUP BY s.machine_id ; 
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

11. Problem - Employee Bonus (577)

Solution - 
SELECT name, bonus from Employee e
LEFT JOIN Bonus b ON e.empid = b.empid
WHERE bonus < 1000 or bonus IS NULL ; 
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

12. Problem - Students and Examinations (1280)

Soluton -
SELECT s.student_id, s.student_name, u.subject_anme, count(e.subject_name) as attended_exams from Students as s
join subjects as u
left join examninations as e on student_id = e.student_id and u.subject_name = e.subject_name
GROUP BY s.student_id, u.subject_name
ORDER BY s.student_id, u.subject_name ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

13. Problem - Managers with at least 5 Direct Reports (570)

Solution - 
WITH report_count as (
  SELECT managerid from employees
  GROUP BY managerid
  HAVING count(id) >= 5
)
SELECT Name from Employee WHERE id IN (SELECT managerid from report_count)
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

14. Problem - Confirmation Rate (1934)

Solution - 
SELECT s.user_id , ROUND(SUM(IF(c.action = "confirmed",1,0)) / count(*)),2) as confiramtion_rate FROM signups s
LEFT JOIN confirmations c on s.user_id = c.user_id
GROUP by s.user_id ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

15. Problem - Not Boring Movies (620)

Solutions - 
SELECT * FROM Cinema 
WHERE mod(id, 2) <> 0 AND description 1+ 'boring'
ORDER by rating DESC ; 
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

16. Problem -  Averagae Selling Price

Solution - 
SELECT
    p.product_id,
    IFNULL(ROUND(SUM(p.price * u.units) / SUM(u.units), 2), 0) AS average_price
FROM Prices AS p
LEFT JOIN UnitsSold AS u
ON
    p.product_id = u.product_id
    AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id ;
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

17. Problem - Project Employees 1 (1075)

Solution - 
SELECT p.project_id, ROUND (AVG (experience_years),2) as average_years from project as p 
LEFT JOIN Employee as e ON p.employee_id = e.employee_id
GROUP BY project_id ; 

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

18. Problem - Percentage of Users Attended a Contest (1633)

Solution - 
SELECT Contest_id, ROUND (COUNT (DISTINCT user_id) *100 / SELECT COUNT(user_id) FROM Users), 2) as Percentage FROM Register
GROUP BY Contest_id
ORDER BY Percentage DESC, Contest_id ; 

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

19. Problem - Queries Quality and Percentage (1211)

Solution - 
SELECT query_name, ROUND( AVG (rating / position),2) as Quality, ROUND(SUM (rating < 3) / COUNT(*)*100, 2) as poor_query_percentage FROM Queries
WHERE query_anem IS NOT NULL
GROUP BY query_name ; 

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

20. Problem - Monthly Transactions 1 (1193)

Solution - 
SELECT month, country, COUNT(*) as trans_count,  SUM(Sate = 'approved') as approved_count,
sum(amount) as trans_total_amount,
sum(if (state = 'approved, amount, 0)) as approved_total_amount
from (SELECT *, date_format( trans_date, '%Y-%m') as month
from transactions) as tab
GROUP BY Country, Month ; 

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

21. Problem -  Immediate Food Delivery II (1174)

Solution - 
WITH cte
    AS ( SELECT customer_id, order_date, MIN(order_date)
    OVER (PARTITION BY customer_id) AS min_date, customer_pref_delivery_date FROM delivery)
SELECT ROUND(( SUM(CASE
                    WHEN order_Date = customer_pref_delivery_date AND customer_pref_delivery_date = min_date THEN 1
                    ELSE 0
                  END) / COUNT( DISTINCT customer_id ) * 100,2) AS immediate_percentage
FROM cte
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

22. Problem - Game Play Analysis IV (550)

Solution - 
SELECT ROUND(COUNT(DISTINCT player_id) / SELECT COUNT(DISTINCT player_id) FROM Activity), 2) AS fraction FROM Activity
WHERE (player_id, DATE_SUB(event_date, INTERVAL 1 DAY) IN ( SELECT player_id, MIN(event_date) AS first_login FROM Activity GROUP BY player_id )
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

23. Problem - Number of Unique Subjects taught by Each Teacher (2356)

Solution - 
SELECT teacher_id , COUNT(DISTINCT subject_id) AS cnt FROm Teacher
GROUP BY teacher_id
_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

24. Problem - User Activity for the Past 30 Days I (1141)
Solution -
SELECT activity_date as day, COUNT(DISTINCT user_id) as active_users FROM Activity
WHERE datediff('2019-07-27',activity_date) < 30 AND activity_date <= '2019-07-27'
GROUP BY activity_date

 _______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

25. Problem -  Product Sales Analysis III (1070)
Solution - 
SELECT product_id, year as First_year, quantity, price from SALES
WHERE (product_id, year) IN (SELECT product_id, MIN(YEAR) FROM SALES GROUP BY product_id )

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

26. Problem - Classes More than 5 Students (596)
Solution - 
SELECT class FROM Courses
GROUP BY 1 HAVING count(*) >= 5

_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________




