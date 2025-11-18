# TestTasks
Завдання 1:
Початкові дані:
Date	Shop	Goods	Amount
01.10.2022	Shop1     	T1        	100.00
01.10.2022	Shop1     	T2        	350.00
01.10.2022	Shop1     	T3        	50.00
01.10.2022	Shop2     	T1        	100.00
01.10.2022	Shop2     	T2        	550.00
01.10.2022	Shop2     	T4        	-60.00
02.10.2022	Shop3     	T4        	0.00


Умова завдання
Розрахувати одним запитом:
  - загальний наростаючий підсумок згідно Amount;
  - наростаючий підсумок Amount в рамках магазину, з сортуванням по Amount за зростанням;
  - максимальне значення Amount в рамках магазину;
  - якщо Amount = 0 тоді знайти його попередне значення згідно поля Date;

SELECT 
    SUM(Amount) OVER(ORDER BY Date) AS sum_running_total_Amount, 
    SUM(Amount) OVER(PARTITION BY Shop ORDER BY Amount) AS srt_shop_Amount, 
    MAX(Amount) OVER(PARTITION BY Shop) AS max_shop_Amount, 
    CASE
        WHEN Amount = 0 THEN LAG(Amount) 
        ELSE ‘None’
END AS previous_Amount
FROM table
ORDER BY Amount;


Завдання 2:
Нормалізуйте дану таблицю (напишіть код створення таблиць з відповідною структурою):
ПІБ	Взвод	Зброя	Зброю видав/ Звання
Петров В.А.,оф.205	222	АК-47	Буров О.С., майор
Петров В.А.,оф.205	222	Глок20	Рыбаков Н.Г., майор
Лодарів П.С.,оф.221	232	АК-74	Деребанов В.Я., підполковник
Лодарів П.С.,оф.221	232	Глок20	Рибаков Н.Г., майор
Леонт'єв К.В., оф.201	212	АК-47	Буров О.С., майор
Леонт'єв К.В., оф.201	212	Глок20	Рибаков Н.Г., майор
Духів Р.М.	200	АК-47	Буров О.С., майор

CREATE TABLE Soldier (
    SoldierId INT IDENTITY PRIMARY KEY,
    FullName NVARCHAR(100) NOT NULL,
    Office NVARCHAR(20)
    PlatoonName INT NOT NULL
);

CREATE TABLE Weapon (
    WeaponId INT IDENTITY PRIMARY KEY,
    Name NVARCHAR(50) NOT NULL
);

CREATE TABLE Officer (
    OfficerId INT IDENTITY PRIMARY KEY,
    FullName NVARCHAR(100) NOT NULL,
    Rank NVARCHAR(50)  NOT NULL
    PlatoonName INT NOT NULL
);

CREATE TABLE WeaponIssue (
    IssueId    INT IDENTITY PRIMARY KEY,
    SoldierId  INT NOT NULL,
    WeaponId   INT NOT NULL,
    OfficerId  INT NOT NULL
); 

#тут треба додати зв'язки між таблицями, наразі зображення схематичне

Завдання 3:
Створіть БД з ім'ям HomeWork, у якій створіть таблицю Product з колонками: ProductId, Name, ProductNumber, Cost, Count, SellStartDate.
У таблицю Product запишіть 10 записів про товари:
Name               ProductNum    Cost     Count   SellStartDate
Корона             AK-53818         5$        50        08/15/2011
Мілка              AM-51122         6.1$      50        07/15/2011
Оленка             AA-52211         2.5$      20        06/15/2011
Snickers           BS-32118         2.8$      50        08/15/2011
Snickers           BSL-3818         5$        100       08/20/2011
Bounty              BB-38218         3$        100       08/01/2011
Nuts                 BN-37818         3$        100       08/21/2011
Mars                 BM-3618           2.5$      50        08/24/2011
Світоч             AS-54181         5$        100       08/12/2011
Світоч             AS-54182         5$        100       08/12/2011


Зробіть вибірку для продукції, кількість якої більше 59 шт.
Зробіть вибірку для продукції, ціна якої більше 3$ та надійшли на продаж з 08/20/2011.

CREATE DATABASE HomeWork; #execute1

USE HomeWork; #execute2

CREATE TABLE Product (
    ProductId INT IDENTITY(1,1) PRIMARY KEY,
    Name NVARCHAR(255) NOT NULL,
    ProductNumber NVARCHAR(255),
    Cost FLOAT,
    Count INT,
    SellStartDate DATETIME,
);

INSERT INTO Product (Name, ProductNumber, Cost, Count, SellStartDate)
VALUES 
(N'Корона', 'AK-53818', 5, 50, 08/15/2011),
(N'Мілка', 'AM-51122', 6.1, 50, 07/15/2011),
(N'Оленка', 'AA-52211', 2.5, 20, 06/15/2011),
('Snickers', 'BS-32118', 2.8, 50, 08/15/2011),
('Snickers', 'BSL-3818', 5, 100, 08/20/2011),
('Bounty', 'BB-38218', 3, 100, 08/01/2011),
('Nuts', 'BN-37818', 3, 100, 08/21/2011),
('Mars', 'BM-3618', 2.5, 50, 08/24/2011),
(N'Світоч', 'AS-54181', 5, 100, 08/12/2011),
(N'Світоч', 'AS-54182', 5, 100, 08/12/2011);
