# Update product tags table

- create a table in MySQL with two columns, "id" (autoincrement) and "sku"
`CREATE TABLE your_table_name (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sku VARCHAR(255) NOT NULL
);`

- find identical values "sku" and remove duplicates
`DELETE t1 FROM march_8 t1
INNER JOIN march_8 t2 
WHERE t1.id > t2.id 
AND t1.sku = t2.sku;`

- there is table with colums "id", "sku_init", "tags_init", "sku_march8", "tags_march8". take the value from cell tags_init next to it sku_init in each row, then find the same sku in column sku_march8 and add the value from column tags_init to tags_march8
`UPDATE your_table_name AS m8
JOIN your_table_name AS init ON m8.sku_march8 = init.sku_init
SET m8.tags_march8 = init.tags_init;`

- add to each cell in column "tags_march8" tag "8 марта", if there are already some values there, for example "Блестящие образы, Новинки, Танец для него", add it to the end separated by commas
`UPDATE your_table_name
SET tags_march8 = CONCAT(tags_march8, ', 8 марта');`

- command to remove "	, " in the cells where there is only value ", 8 марта"
`UPDATE your_table_name
SET tags_march8 = REPLACE(tags_march8, ', 8 марта', '8 марта')
WHERE tags_march8 = ', 8 марта';`