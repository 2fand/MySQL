```sql
SHOW DATABASE;
-- 第一学会的SQL语句^
```
```sql
SHOW DATABASE;
CREATE DATABASE db;
SHOW DATABASE;
DROP DATABASE db;
SHOW DATABASE;
-- 创建与删除数据库^
```
```sql
SHOW DATABASES;
CREATE DATABASE db;
USE db;
SELECT DATABASE();
-- 初用函数^
```
```sql
-- 双横杠注释
-- 初用双横杠注释^
```
```sql
CREATE TABLE `game` (
  `id` int DEFAULT NULL,
  `playername` varchar(20) DEFAULT NULL,
  `coins` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
-- 初创建表^
```
```sql
INSERT INTO game VALUES(0, 'Player', 100), (1, 'System', 9999999), (2, 'Hacker', 9999999);
SELECT playername FROM game;
DELETE FROM game where id = 2;
SELECT playername FROM game;
-- 初操作表中的数据^
```
