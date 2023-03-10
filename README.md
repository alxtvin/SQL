## Примеры SQL-запросов 
### Задание 1

1) Есть база данных с поездками на такси. По плану на линию обслуживания должно было выйти 10550 автомобилей — эта цифра покрывает спрос пользователей. Команде поступило много жалоб: свободных автомобилей оказалось недостаточно. Сколько такси вышло на линии на самом деле? Информация о всех машинах на линии есть в таблице cabs.

#### SQL-запрос:
SELECT     
COUNT(DISTINCT vehicle_id) AS cars    
FROM    
cabs;

2) Посчитай количество автомобилей в каждой компании. Отсортируй значения по убыванию. Команда предполагает, что некоторые компании не вывели достаточно автомобилей на линию. 
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

3) В приложении такси рассчитывается коэффициент стоимости поездки. Если погода хорошая, значение коэффициента равно 1. Если на улице дождь или шторм, коэффициент повышается до 2. У команды есть гипотеза, что в расчётах коэффициента ошибка. Чтобы проверить расчёт коэффициента, команде нужна выборка данных: разработчик может сверить коэффициент с данными в логах и исправить баг. Получи описание погодных условий из таблицы weather_records для каждого часа. В результирующей таблице должно быть два поля — дата и час (ts) и weather_conditions. Сделай выборку за период с 2017-11-05 00:00 по 2017-11-06 00:00.

#### SQL-запрос:
SELECT   
ts,   
CASE WHEN description LIKE '%rain%' OR description LIKE '%storm%' THEN 'Bad'   
WHEN description LIKE '%' THEN 'Good'   
ELSE description END AS weather_conditions   
FROM   
weather_records   
WHERE   
ts BETWEEN '2017-11-05 00:00' AND '2017-11-06 00:00';  

![sql1_3](https://github.com/alxtvin/SQL/blob/main/screenshots/sql1_3.png)

4) После обновления ПО таксопарки стали сообщать, что прибыль, которую они получают, не сходится с данными, которые отдаёт приложение. Разработка предполагает, что проблема может быть в данных о количестве поездок. Чтобы определить, есть ли баг, нужно получить выборку с количеством поездок каждого таксопарка за 15 и 16 ноября 2017 года. Выведи поле company_name. Поле с числом поездок назови trips_amount и выведи его. Результаты, полученные в поле trips_amount, отсортируй по убыванию. 
 
#### SQL-запрос:
SELECT   
cabs.company_name,  
COUNT(trips.trip_id) AS trips_amount  
FROM   
cabs  
LEFT JOIN trips ON cabs.cab_id = trips.cab_id  
WHERE   
trips.start_ts BETWEEN '2017-11-15 00:00' AND '2017-11-16 23:59'  
GROUP BY  
company_name  
ORDER BY   
trips_amount DESC;  

![sql1_4](https://github.com/alxtvin/SQL/blob/main/screenshots/sql1_4.png)
