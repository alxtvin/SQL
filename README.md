## Примеры SQL-запросов 
### Задание 1

- Вводные данные:

![table_schema](https://github.com/alxtvin/SQL/blob/main/screenshots/table_schema.png)

1) Есть база данных с поездками на такси. По плану на линию обслуживания должно было выйти 10550 автомобилей — эта цифра покрывает спрос пользователей. Команде поступило много жалоб: свободных автомобилей оказалось недостаточно. Сколько такси вышло на линии на самом деле? Информация о всех машинах на линии есть в таблице cabs.

#### SQL-запрос:
SELECT     
COUNT(DISTINCT vehicle_id) AS cars    
FROM    
cabs;


2) Посчитай количество автомобилей в каждой компании из таблицы cabs. Отсортируй значения по убыванию. Команда предполагает, что некоторые компании не вывели достаточно автомобилей на линию. 
Выведи те компании, в которых меньше 100 автомобилей. 


#### SQL-запрос:
SELECT   
company_name,   
COUNT(vehicle_id) AS cnt  
FROM   
cabs  
GROUP BY  
company_name  
HAVING COUNT(vehicle_id) < 100  
ORDER BY   
cnt DESC;

![sql1_2](https://github.com/alxtvin/SQL/blob/main/screenshots/sql1_2.png)
