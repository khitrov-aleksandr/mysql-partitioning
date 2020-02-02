# mysql-partitioning
Функция `create_partition` создаёт партицию для таблицы с минимальным значением параметра clock равным: текущее время в секундах плюс одна неделя(608400).
Функция `delete_partition` удаляет самую первую партицию с начала.

## Создание хранимых процедур
```bash
  mysql zabbix < sql/create_partition.sql
```
```bash
  mysql zabbix < sql/delete_partition.sql
```

## Вызов хранимых процедур
```sql
  CALL create_partition('history');
```
```sql
  CALL delete_partition('history');
```
## Пример создания таблицы с партициями
```sql
  CREATE TABLE history (
    itemid bigint(20) unsigned NOT NULL,
    clock int(11) NOT NULL DEFAULT '0',
    value double(16,4) NOT NULL DEFAULT '0.0000',
    ns int(11) NOT NULL DEFAULT '0',
    KEY history_1 (itemid,clock)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
  PARTITION BY RANGE (clock)
  (PARTITION p1572296400 VALUES LESS THAN (1572296400));
```
