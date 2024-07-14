Task 1: Create a stored procedure to insert a new record into the Worker table
DELIMITER //

CREATE PROCEDURE InsertWorker (
    IN p_Worker_Id INT,
    IN p_FirstName CHAR(25),
    IN p_LastName CHAR(25),
    IN p_Salary INT,
    IN p_JoiningDate DATETIME,
    IN p_Department CHAR(25)
)
BEGIN
    INSERT INTO Worker (Worker_Id, FirstName, LastName, Salary, JoiningDate, Department)
    VALUES (p_Worker_Id, p_FirstName, p_LastName, p_Salary, p_JoiningDate, p_Department);
END//

DELIMITER ;
--To call this procedure and add a new worker record:--
CALL InsertWorker(101, 'John', 'Doe', 50000, '2024-07-14', 'IT');
Task 2: Create a stored procedure to retrieve salary by Worker_Id
DELIMITER //

CREATE PROCEDURE GetSalaryById (
    IN p_Worker_Id INT,
    OUT p_Salary INT
)
BEGIN
    SELECT Salary INTO p_Salary
    FROM Worker
    WHERE Worker_Id = p_Worker_Id;
END//

DELIMITER ;
--To call this procedure and retrieve the salary of a worker:--
CALL GetSalaryById(101, @p_salary);
SELECT @p_salary AS Worker101Salary;
--Task 3: Create a stored procedure to update department by Worker_Id;--
DELIMITER //

CREATE PROCEDURE UpdateWorkerDepartment (
    IN p_Worker_Id INT,
    IN p_Department CHAR(25)
)
BEGIN
    UPDATE Worker
    SET Department = p_Department
    WHERE Worker_Id = p_Worker_Id;
END//

DELIMITER ;
To call this procedure and update the department of a worker:
CALL UpdateWorkerDepartment(101, 'HR');
Task 4: Create a stored procedure to count workers in a department
DELIMITER //

CREATE PROCEDURE CountWorkersInDepartment (
    IN p_Department CHAR(25),
    OUT p_workerCount INT
)
BEGIN
    SELECT COUNT(*) INTO p_workerCount
    FROM Worker
    WHERE Department = p_Department;
END//

DELIMITER ;
To call this procedure and get the count of workers in a department:
CALL CountWorkersInDepartment('IT', @p_workerCount);
SELECT @p_workerCount AS ITWorkerCount;
Task 5: Create a stored procedure to calculate average salary in a department
DELIMITER //

CREATE PROCEDURE GetAverageSalaryInDepartment (
    IN p_Department CHAR(25),
    OUT p_avgSalary DECIMAL(10, 2)
)
BEGIN
    SELECT AVG(Salary) INTO p_avgSalary
    FROM Worker
    WHERE Department = p_Department;
END//

DELIMITER ;
To call this procedure and get the average salary of workers in a department:
CALL GetAverageSalaryInDepartment('IT', @p_avgSalary);
SELECT @p_avgSalary AS ITAverageSalary;
