# mysql-partitioning

## Создание хранимых процедур
```
  mysql zabbix < sql/create_partition.sql
```
```
  mysql zabbix < sql/delete_partition.sql
```

## Вызов хранимых процедур
```
  CALL create_partition('history');
```
```
  CALL delete_partition('history');
```
