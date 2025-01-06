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
```sql
INSERT INTO game VALUES(3, 'Hacker', 114514), (4, 'Hr', 11414), (5, 'Hoger', 100000), (6, 'Player', 4444444), (7, 'noname', 1000);
SELECT id, playername hackers, coins FROM game WHERE coins >= 100000;
DELETE FROM game WHERE coins >= 100000;
SELECT id, playername players, coins FROM game;
-- 防外挂的游戏表^
```
```sql
INSERT INTO game VALUES(1, 'System', 999999), (3, 'Hacker', 114514), (4, 'Hr', 11414), (5, 'Hoger', 100000), (6, 'Player', 4444444), (2, 'noname', 1000);
SELECT id, playername hackers, coins FROM game WHERE coins >= 100000 AND id != 1;
DELETE FROM game WHERE coins >= 100000 AND id != 1;
SELECT id, playername players, coins FROM game WHERE id != 1;
SELECT id, playername Systems, coins FROM game WHERE id = 1;
-- System可以合法的开桂^
```
```sql
INSERT INTO game VALUES(1, 'System', 999999), (3, 'System', 114514), (4, 'System', 11414), (5, 'System', 100000), (8, 'Player', 0), (2, 'noname', 1000);
SELECT playername FROM game GROUP BY playername;
-- 得出玩家的名字^
```
```sql
INSERT INTO game VALUES(1, 'System', 999999), (3, 'System', 114514), (4, 'System', 11414), (5, 'System', 100000), (8, 'Player', 0), (2, 'noname', 1000);
SELECT playername, COUNT(playername) SameNameCount FROM game GROUP BY playername;
-- 求出重名玩家的数量^
```
```spl
INSERT INTO game VALUES(1, 'System', 999999), (3, 'System', 114514), (4, 'System', 11414), (5, 'gamer', 100000), (8, 'Player', 0), (2, 'noname', 1000);
DELETE FROM game WHERE 1 != id AND 'System' = playername OR coins > 99999;
SELECT id, playername, coins FROM game;
-- “System”重名bug已修复^
```
```sql
ALTER TABLE game MODIFY id INT UNSIGNED;
ALTER TABLE game MODIFY coins INT UNSIGNED;
-- “MODIFY”关键词的应用^
```
```sql
CREATE TABLE test(
    test TINYINT COMMENT '测试'
) COMMENT '测试表';
-- COMMENT注释^
```
```sql
DROP TABLE test;
-- 删表^
```
```sql
CREATE TABLE game(
    id INT UNSIGNED PRIMARY KEY UNIQUE AUTO_INCREMENT COMMENT '玩家编号',
    name varchar(20) UNIQUE COMMENT '名字',
    coins INT UNSIGNED DEFAULT 0 COMMENT '硬币数'
) COMMENT '游戏表';
-- 约束^
```
```sql
ALTER TABLE game ADD identity TINYINT UNSIGNED COMMENT '身份';
-- 加字段^
```
```sql
CREATE TABLE gameIdentity(
    id TINYINT UNSIGNED PRIMARY KEY UNIQUE AUTO_INCREMENT COMMENT '身份编号',
    identity VARCHAR(20) UNIQUE COMMENT '身份'
) COMMENT '身份表';
INSERT INTO gameIdentity(identity) VALUES('System'), ('Player');
-- 初始化表^
```
