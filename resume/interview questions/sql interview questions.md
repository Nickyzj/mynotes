# [Interview Questions](https://www.youtube.com/channel/UCM5ldu3IonPjffpYSnSYYJA/videos)

## [IQ15 - 6 SQL Query Interview Questions](https://www.youtube.com/watch?v=uAWWhEA57bE&t=835s)

1. Return employee record with highest salary

```sql
select * 
from employee
where salary in
(select max(salary) from employee);
```

2. Return the highest salary in employee table

```sql
select max(salary) from employee;
```

3. Reutrn the 2nd highest salary from employee table

```
select max(salary)
from employee
where salary not in 
(select max(salary) from employee);
```

4. Select range of employees based on id

```
select *
from employee
where id between 2003 and 2008;
```

5. Return an employee name with the highest salary and the employee's department name

```sql
select e.first_name, e.last_name, e.salary, d.department_name
from employee e inner join department d 
on (e.department_id = d.department_id)
where salary in 
(select max(salary) from employee);
```

6. Return highest salary, employee_name, department_name for each department

```sql
select e.salary, e.first_name, e.last_name, d.department_name
from employee e inner join dempartment d
on (e.department_id = d.department_id)
where salary in 
(select max(salary) from employee group by department_id)
```

