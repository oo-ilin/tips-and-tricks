# 1. Работа с бекапами


## Делаем бекап
`mysqldump -u USER -pPASSWORD DATABASE > /path/to/file/dump.sql`

## Создаём структуру базы без данных
`mysqldump --no-data - u USER -pPASSWORD DATABASE > /path/to/file/schema.sql`

### Если нужно сделать дамп только одной или нескольких таблиц
`mysqldump -u USER -pPASSWORD DATABASE TABLE1 TABLE2 TABLE3 > /path/to/file/dump_table.sql`

## Создаём бекап и сразу его архивируем
`mysqldump -u USER -pPASSWORD DATABASE | gzip > /path/to/outputfile.sql.gz`

## Создание бекапа с указанием его даты
`mysqldump -u USER -pPASSWORD DATABASE | gzip > 'date +/path/to/outputfile.sql.%Y%m%d.%H%M%S.gz'`

## Заливаем бекап в базу данных
`mysql -u USER -pPASSWORD DATABASE < /path/to/dump.sql`

## Заливаем архив бекапа в базу
`gunzip < /path/to/outputfile.sql.gz | mysql -u USER -pPASSWORD DATABASE`  
  
или так  
  
`zcat /path/to/outputfile.sql.gz | mysql -u USER -pPASSWORD DATABASE`

## Создаём новую базу данных
`mysqladmin -u USER -pPASSWORD create NEWDATABASE` 

  

#### Дополнительно
Удобно использовать бекап с дополнительными опциями **-Q**, **-c**, **-e**, т.е.  

`mysqldump -Q -c -e -u USER -pPASSWORD DATABASE > /path/to/file/dump.sql`  
  
**-Q** оборачивает имена обратными кавычками  
**-c** делает полную вставку, включая имена колонок  
**-e** делает расширенную вставку. Итоговый файл получается меньше и делается он чуть быстрее  
  


Для просмотра списка баз данных можно использовать команду:  
`mysqlshow -u USER -pPASSWORD`
  
А так же можно посмотреть список таблиц базы:  
`mysqlshow -u USER -pPASSWORD DATABASE`

*Для таблиц InnoDB надо добавлять **--single-transaction**, это гарантирует целостность данных бекапа. 
Для таблиц MyISAN это не актуально, ибо они не поддерживают транзакционность.*
