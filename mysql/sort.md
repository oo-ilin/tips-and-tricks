#### Выбрать данные с сортировкой по WHERE IN
  
**-- Вариант 1**  
`SELECT * FROM table WHERE id IN (118,17,113,23,72)   
ORDER BY FIELD(id,118,17,113,23,72)`

**-- Вариант 2**  
    SELECT  
        id,  
        date  
    FROM items  
    WHERE id IN (1,2,1,3)  
    ORDER BY FIND_IN_SET(id, '1,2,1,3');
 
**-- Вариант 3**  
`SELECT id, date FROM items where id = 1
UNION ALL
SELECT id, date FROM items where id = 2
UNION ALL
SELECT id, date FROM items where id = 1
UNION ALL
SELECT id, date FROM items where id = 3;`