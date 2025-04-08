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
```sql
ALTER TABLE `db`.`game` 
ADD CONSTRAINT `identity` FOREIGN KEY (`identity`) REFERENCES `db`.`gameidentity` (`id`) ON DELETE SET NULL ON UPDATE SET NULL;
-- 添加外键^
```
```sql
INSERT INTO game(name, coins, identity) VALUES('System', 9999999, 1);
INSERT INTO game(name, coins, identity) VALUES('System', 9999999, 0);
-- UNIQUE约束发力了^
```
```sql
SELECT id 编号, name 名字, coins 金币数量, IF(0 = identity, '玩家', '系统') 身份 FROM game;
-- IF函数的应用^
```
```sql
SELECT id 编号, name 名字, coins 金币数量, (SELECT iden.identity FROM gameidentity iden WHERE iden.id = game.identity) 身份 FROM game;
-- 标量子查询的应用^
```
```sql
# 我会用#号来注释
-- 见上面注释^
```
```sql
DELETE FROM game g WHERE 'System' != (SELECT gid.identity FROM gameidentity gid WHERE g.identity = gid.id) AND g.coins > 10000000;
-- 新的防外挂删除代码^
```
```sql
SELECT id, name, coins, identity FROM game WHERE name LIKE '___%';
-- “LIKE”的应用^
```
```sql
SET @a = 1;
SELECT @a;
-- 局部变量的使用^
```
```sql
SELECT @@autocommit;
-- 系统变量的查询^
```
```sql
SELECT 1, '&', 'db', 1 != 0, 1+6, 'aaa' LIKE '%';
-- MYSQL中99%的人都不知道的冷知识 —— SELECT关键字可以查询常量以及算式，布尔值等的结果^
```
```sql
SELECT id, name, coins, (SELECT gid.identity FROM gameidentity gid WHERE g.identity = gid.id) identity FROM game g WHERE id IN(1, 3, 5);
-- “IN”的应用^
```
```sql
CREATE TABLE test(
    t TINYINT
) ENGINE = MyISAM;
-- 表自定义设置存储引擎^
```
```sql
SHOW ENGINES;
-- 展示所有内置存储引擎^
```
```sql
SET GLOBAL TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
SELECT @@TRANSACTION_ISOLATION;
-- 设事务的隔离级别为read uncommitted^
```
```sql
SELECT id, name, coins, identity FROM game WHERE name REGEXP '.{3}';
-- 用正则表达式来查询数据^
```
```sql
SELECT g.id, g.name, g.coins, gid.identity FROM game g, gameidentity gid WHERE g.identity = gid.id;
-- 用隐式内链接来查询数据^
```
```sql
SELECT g.id, g.name, g.coins, gid.identity FROM game g INNER JOIN gameidentity gid ON g.identity = gid.id;
-- 用显式内链接来查询数据^
```
```sql
SELECT g.id, g.name, g.coins, gid.identity FROM game g LEFT JOIN gameidentity gid ON g.identity = gid.id;
-- 用左外链接来查询数据^
```
```sql
SELECT g.id, g.name, g.coins, gid.identity FROM game g RIGHT JOIN gameidentity gid ON g.identity = gid.id;
-- 用右外链接来查询数据^
```
```sql
SELECT t FROM test
UNION
SELECT t FROM testa;
-- 两表合为一^
```
```sql
SELECT t FROM test
UNION ALL
SELECT t FROM testa;
-- 把两表的全部数据合为一表^
```
```sql
SELECT AVG(t) FROM test;
-- 求平均值^
```
```sql
SELECT MIN(t) FROM test;
-- 求最小值^
```
```sql
SELECT MAX(t) FROM test;
-- 求最大值^
```
```sql
SELECT t+1 FROM test;
-- 使表t中所有的数据在被查询时全都加1^
```
```sql
SELECT CEIL(0.1);
-- 向上取整^
```
```sql
SELECT ROUND(0.1), ROUND(0.5);
-- 四舍五入^
```
SELECT FLOOR(0.1);
-- 向下取整^
```
```sql
SELECT ROUND(0.1), ROUND(0.5);
-- 四舍五入^
```
```sql
SELECT ROUND(1.254, 1), ROUND(1.254, 2);
-- 保留1位或2位小数^
```
``sql
SELECT SUM(t) FROM test;
-- 单表数据求和^
```
```sql
SELECT (SELECT SUM(t) FROM test) + (SELECT SUM(t) FROM testa) SUM;
-- 双表数据求和^
```
```sql
SELECT IFNULL(t, 'NULL') t FROM test;
-- IFNULL条件判断函数的应用^
```
```sql
SELECT CASE WHEN 2 = 1 THEN '1' WHEN 1 = 1 THEN '2' ELSE 'else' END;
-- “CASE WHEN THEN ELSE END”判断语句的应用^
```
```sql
SELECT CASE 1 WHEN 1 THEN '1' WHEN 2 THEN '2' ELSE 'else' END;
-- C/C++的switch语句^
```
```sql
SELECT LPAD('s',111, 'asdfgf')
-- 字符串函数^
```
```sql
SELECT SUBSTR('1234!@#$', 3, 4);
-- 提取子字符串^
```
```sql
SELECT POW(5, 5)
-- n的n次方^
```
```sql
SELECT ABS(-666);
-- ABS绝对值^
```
```sql
SELECT id, name, coins, identity FROM game WHERE 1 != id ORDER BY coins DESC LIMIT 2, 1;
-- 查询金币数量第三高玩家信息^
```
```sql
SELECT id, name, coins, identity FROM game WHERE 1 != id ORDER BY coins DESC LIMIT 3;
-- 查询金币数量前三高玩家信息^
```
```sql
SELECT id, name, coins, identity FROM game WHERE 1 <> id
-- 也是不等号^
```
```sql
CREATE USER 'aaa^^^111'@'127.0.0.1' IDENTIFIED BY 'aaa^^^111';
-- 创建用户^
```
```sql
ALTER USER 'aaa^^^111'@'127.0.0.1' IDENTIFIED BY 'aaa^^^111@';
-- 修改用户密码^
```
```sql
SELECT SUBSTR('12345678910', 5);
-- 另一种提取子字符串的方式^
```
```sql
SELECT DAY('2000-01-01');
-- 查询日期的天数
```
```sql
SELECT YEAR('2000-01-01');
-- 查询日期的年数^
```
```sql
SELECT MONTH('2000-01-01');
-- 查询日期的月数^
```
```sql
SELECT DATE_ADD('2000-01-01', INTERVAL 10 DAY);
-- DATE_ADD方法1^
```
```sql
SELECT DATE_ADD('2000-01-01', INTERVAL 10 MONTH); 
-- DATE_ADD方法2^
```
```sql
SELECT DATE_SUB('2000-01-01', INTERVAL 10 MONTH);
-- DATA_SUB方法1^
```
```sql
SELECT DATE_SUB('2000-01-01', INTERVAL 2000 YEAR);
-- DATA_SUB方法2^
```
```sql
SELECT DATEDIFF('2101-01-21', '2121-12-01');
-- DATADIFF方法1^
```
```sql
SELECT DATEDIFF('2101-01-21', '0121-12-01');
-- DATADIFF方法2^
```
```sql
SHOW INDEX FROM game;
-- 显示表的索引^
```
```sql
CREATE INDEX coinIndex ON game(coins);
-- 创建表的索引^
```
```sql
DROP INDEX coinIndex ON game;
-- 删除表的索引^
```
```sql
CREATE FULLTEXT INDEX nameIndex ON game(name);
-- 创建表的全文索引^
```
```sql
SELECT SUBSTRING_INDEX('11111,22222,33333', ',', 1);
-- SUBSTRING_INDEX函数的初次调用^
```
```sql
SELECT SUBSTRING_INDEX('11111,22222,33333', ',', 2);
-- SUBSTRING_INDEX函数的第二次调用^
```
```sql
SELECT SUBSTRING_INDEX('11111,22222,33333', ',', -1);
-- SUBSTRING_INDEX函数的第三次调用^
```
```sql
SELECT SUBSTRING_INDEX('11111,22222,33333', ',', -2);
-- SUBSTRING_INDEX函数的第四次调用^
```
```sql
SELECT 
    id, name, coins, identity,
    ROW_NUMBER() OVER()
FROM 
    game;
-- 无子句窗口函数^
```
```sql
SELECT 
    id, name, coins, identity,
    ROW_NUMBER() OVER(PARTITION BY identity ORDER BY coins DESC)
FROM 
    game;
-- 窗口函数的实际使用^
```
```sql
SELECT 
    id, device_id, gender, age, university, gpa,
    ROW_NUMBER() OVER (ORDER BY gpa DESC) 排行
FROM 
    user_profile;
-- 生成每个学生的排行榜^
```
```sql
SELECT 
    id, device_id, gender, age, university, gpa,
    RANK() OVER (ORDER BY gpa DESC) 排行
FROM 
    user_profile;
-- 生成每个学生的排行榜2^
```
```sql
SELECT 
    name, point, likes,
    LAG(name) OVER (ORDER BY point DESC) next_name,
    LAG(point) OVER (ORDER BY point DESC) next_point
FROM
    xiaoyuan_calculation_tb;
-- LAG跨行函数可能的应用^
```
```sql
SELECT
    salary_date 
INTO
    @sec_grp
FROM
    (
    SELECT 
        COUNT(*) OVER () rid, 
        salary_date 
    FROM 
    (
        SELECT
            (COUNT(*) OVER (ORDER BY salary_date RANGE BETWEEN INTERVAL 1 MONTH PRECEDING AND CURRENT ROW)) groupId, salary_date, salary
        FROM
            xiaomings_salary_tb
    ) tb
    WHERE
        groupId = 1
    ) tba
WHERE 
    rid = 1;
    

SELECT  
    ROW_NUMBER() OVER (PARTITION BY IF(salary_date < @sec_grp, 1, 2)) comboDays,
    salary_date, salary
FROM
    xiaomings_salary_tb;
-- 有bug却还能跑的程序^
```
```sql
SELECT 
    salary_date 
INTO 
    @sec_grp_mark
FROM 
(
    SELECT
        (COUNT(*) OVER (ORDER BY salary_date RANGE BETWEEN INTERVAL 1 MONTH PRECEDING AND CURRENT ROW)) groupId, salary_date, salary
    FROM
        xiaomings_salary_tb
    ORDER BY
        salary_date DESC
) tb
WHERE
    groupId = 1
LIMIT
    1;
  
SELECT  
    ROW_NUMBER() OVER (PARTITION BY IF(salary_date < @sec_grp_mark, 1, 2)) comboDays,
    salary_date, salary
FROM
    xiaomings_salary_tb;  
-- 变得正常的sql^
```
```sql
-- 函数TST
CREATE DEFINER=`root`@`localhost` FUNCTION `TST`() RETURNS int
    NO SQL
BEGIN
  #Routine body goes here...
RETURN 101;
END
-- NO SQL函数^
```
```sql
-- 函数TST
CREATE DEFINER=`root`@`localhost` FUNCTION `TST`( i int) RETURNS int
    READS SQL DATA
BEGIN
  DECLARE b TINYINT DEFAULT 0;
  SELECT IF(i= 0, 1, 0) INTO @b;
RETURN @b;
END
-- READS SQL DATA函数^
```
```sql
-- 函数TST
CREATE DEFINER=`root`@`localhost` FUNCTION `TST`( i int) RETURNS int
    DETERMINISTIC
BEGIN
  DECLARE b TINYINT DEFAULT 0;
  SELECT IF(i<0, 1, 0) INTO @b;
RETURN @b;
END
-- DETERMINISTIC函数^
```
```sql
-- 函数TST
CREATE DEFINER=`root`@`localhost` FUNCTION `TST`( i int) RETURNS int
    READS SQL DATA
BEGIN
  select T into @b FROM test LIMIT 1;
RETURN @b;
END
-- 查找表中数据的函数^
```
```
DROP TABLE IF EXISTS participants;

CREATE TABLE participants(
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(20),
    gender CHAR(1),
    time DATETIME,
    m FLOAT
);

INSERT INTO participants(name, gender, time, m) VALUES
('凤皇', '男', '2020-06-17 10:04:24', 1.49),
('柏佳兴', '男', '2020-06-17 10:03:35', 1.07),
('田静', '女', '2020-06-17 10:01:29', 1.34),
('何平', '男', '2020-06-17 10:01:05', 1.14),
('李尤爱', '女', '2020-06-17 10:05:07', 1.56),
('束组', '男', '2020-06-17 10:02:02', 1.66),
('曹彼壁', '男', '2020-06-17 10:03:09', 1.62),
('朱翠碧', '女', '2020-06-17 10:04:03', 1.15),
('赵涵然', '女', '2020-06-17 10:00:22', 1.61),
('傅幸', '男', '2020-06-17 10:02:34', 1.41);

SELECT 
    *
FROM
    participants;

SELECT 
    id, name, gender, time, m, 
    MAX(m) OVER (PARTITION BY gender ORDER BY time ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) maxForEachGender
FROM
    participants
-- 用了分组子句，排序子句和限行子句的窗口函数^
```
```sql
-- test存储过程
CREATE DEFINER=`root`@`localhost` PROCEDURE `test`(INOUT i int)
BEGIN
  SET i := i * 2;
END
-- 查询操作
SET @i := -115;
CALL test(@i);
SELECT @i;
-- 存储过程的创建和使用^
```
```sql
CREATE VIEW v AS SELECT t FROM test;
-- 创建视图^
```
```sql
SELECT t FROM v WHERE t > 3;
-- 使用视图^
```
```sql
CREATE VIEW va AS SELECT t FROM test WHERE t < 10;
-- 创建有条件的视图^
```
```sql
DROP VIEW va;
-- 删除视图^
```
```sql
CREATE VIEW vaa AS SELECT t FROM test WHERE t < 10 WITH CASCADED CHECK OPTION;
-- 创建CASCADED视图^
```
```sql
INSERT INTO vaa VALUES(1);
-- INSERT INTO vaa VALUES(1000); **ERROR**
SELECT t FROM test;
-- CASCADED视图的插入测试^
```
```sql
CREATE VIEW vbb AS SELECT t FROM test WHERE t < 10 WITH LOCAL CHECK OPTION;
-- 创建LOCAL视图^
```
```sql
INSERT INTO vbb VALUES(1);
-- INSERT INTO vaa VALUES(1000); **ERROR**
SELECT t FROM test;
-- LOCAL视图的插入测试^
```
```sql
CREATE VIEW vb AS SELECT t FROM vbb ORDER BY t DESC WITH LOCAL CHECK OPTION;
SELECT t FROM vb;
-- 创建LOCAL嵌套视图^
```
```sql
CREATE VIEW vc AS SELECT t FROM vb WITH CASCADED CHECK OPTION;
-- 创建CASCADED嵌套视图^
```
```sql
DROP VIEW v, vaa, vb, vbb, vc;
-- 批量删除视图^
```
```sql
DROP TABLE a, b;
-- 批量删表^
```
```sql
EXPLAIN SELECT 1;
-- 初用EXPLAIN关键字查询SELECT查询语句的执行情况^
```
```sql
CREATE INDEX t_index ON test(t);
EXPLAIN SELECT t FROM test;
-- 索引的用途^
```
```sql
EXPLAIN SELECT t FROM test USE INDEX(t_index);
-- SQL提示1——USE INDEX^
```
```sql
EXPLAIN SELECT t FROM test IGNORE INDEX(t_index);
-- SQL提示2——IGNORE INDEX^
```
```sql
CREATE INDEX game_IdAndnameAndCoins_Index ON game(id, name, coins);
-- 联合索引的创建^
```
```sql
EXPLAIN SELECT id, name, coins, identity FROM game FORCE INDEX(PRIMARY) WHERE id < 5 AND coins < 500;
-- SQL提示3——FORCE INDEX^
```
```sql
EXPLAIN SELECT id FROM game IGNORE INDEX(PRIMARY) WHERE id = 1;
-- 非常快的const查询^
```
```sql
SELECT g.id, g.name, g.coins, gi.identity FROM game g JOIN gameidentity gi ON g.identity = gi.id;
EXPLAIN SELECT g.id, g.name, g.coins, gi.identity FROM game g JOIN gameidentity gi ON g.identity = gi.id;
-- 查询联合查询执行的情况，平均很慢^
```
```sql
EXPLAIN SELECT id, name, coins, identity FROM game FORCE INDEX(PRIMARY) LIMIT 1, 6;
-- LIMIT分页查询的查询情况，全表扫描，很慢^
```
```sql
SELECT COUNT(*), identity FROM game GROUP BY identity;
EXPLAIN SELECT COUNT(*), identity FROM game GROUP BY identity;
-- GROUP BY分组查询，用了索引来查询，快了一点^
```
```sql
EXPLAIN SELECT id, name, coins, identity FROM game ORDER BY coins;
-- 可以优化ORDER BY排序子句了^
```
```sql
CREATE INDEX all_indexa ON game(coins, id, name, identity);
EXPLAIN SELECT id, name, coins, identity FROM game FORCE index (all_indexa) ORDER BY coins ASC;
-- 这下ORDER BY排序子句变快了^
```
```sql
EXPLAIN SELECT id, name, coins, identity FROM game ORDER BY coins DESC;
-- 索引往后遍历的查询语句^
```
```sql
CREATE INDEX all_indexb ON game(coins DESC, name ASC, id, identity);
EXPLAIN SELECT id, name, coins, identity FROM game USE INDEX(all_indexb) ORDER BY coins DESC, name ASC;
-- 创建索引时指定了字段的排序方式，查询语句很快就查好了^
```
```sql
DROP INDEX coins_index ON game;
EXPLAIN SELECT id, name, coins, identity FROM game WHERE id > 5 AND coins < 1000;
-- 意外的range查询^
```
```sql
CREATE INDEX coins_index ON game(coins);
EXPLAIN SELECT id, name, coins, identity FROM game WHERE id > 5 AND coins < 1000;
-- filtered字段的值很大的range查询语句^
```
```sql
CREATE TRIGGER tst_triger
AFTER INSERT ON test FOR EACH ROW
BEGIN
  SELECT MAX(t) FROM test INTO @ee;
END;
-- 创建insert行级插入触发器^
```
```sql
SHOW TRIGGERS;
-- 查看当前创建的触发器^
```
```sql
SHOW TRIGGERS;
DROP TRIGGER t;
SHOW TRIGGERS;
-- 删除触发器^
```
```sql
CREATE TRIGGER tst
AFTER UPDATE ON test FOR EACH ROW
BEGIN
    SELECT NEW.t FROM test INTO @ee;
END;
-- NEW关键字的用途——获取库中新数据^
```
```sql
UPDATE test SET t = 101 WHERE t = 100;
select @ee;
-- 触发器生效了^
```
```sql
-- abc存储过程创建语句内
CREATE PROCEDURE abc()
BEGIN
    SELECT CASE WHEN TRUE THEN TRUE END;
END;
-- abc存储过程创建语句外
CALL abc();
-- 重温存储过程的创建^
```
```sql
-- abca存储过程创建语句内
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 1;
    sum : LOOP
      SELECT i;
      SET i := i + 1;
      LEAVE sum;
    END LOOP sum;
END;
-- abca存储过程创建语句外
CALL abca();
-- LOOP循环的使用^
```
```sql
DROP PROCEDURE abca;
-- 删除存储过程abca^
```
```sql
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 1;
    sum : LOOP
      SELECT i;
      SET i := i + 1;
      IF i > 5 THEN
        LEAVE sum;
      END IF;
    END LOOP sum;
END;
-- abca存储过程创建后
CALL abca();
-- 循环5次^
```
```sql
-- abca存储过程创建前
DROP PROCEDURE abca;
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 1;
    SELECT i;
    sum : LOOP
      SET i := i + 1;
      IF i = 20 THEN
        LEAVE sum;
      END IF;
    END LOOP sum;
    SELECT i;
END;
-- abca存储过程创建后
CALL abca();
-- 把变量i用循环加到20^
```
```sql
-- abca存储过程创建前
-- DROP PROCEDURE abca;
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 1;
    SELECT i;
    REPEAT
        SET i := i + 1;
    UNTIL i >= 20 END REPEAT;
    SELECT i;
END;
-- abca存储过程创建后
CALL abca();
-- REPEAT循环的使用^
```
```sql
-- abca存储过程创建前
DROP PROCEDURE abca;
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 1;
    SELECT i;
    REPEAT
        SET i := i - 1;
    UNTIL i < 1 END REPEAT;
    SELECT i;
END;
-- abca存储过程创建后
CALL abca();
-- 类似于do-while循环的REPEAT循环^
```
```sql
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE tstCursor CURSOR FOR SELECT t FROM test;
END;
-- 尝试声明游标^
```
```sql
-- abca存储过程创建前
DROP PROCEDURE abca;
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 0;
    DECLARE tstCursor CURSOR FOR SELECT t FROM test;
    OPEN tstCursor;
    FETCH tstCursor INTO i;
    SELECT i;
    CLOSE tstCursor;
END;
-- abca存储过程创建后
CALL abca();
-- 游标的使用^
```
```sql
-- abca存储过程创建前
DROP PROCEDURE abca;
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 0;
    DECLARE tstCursor CURSOR FOR SELECT t FROM test;
    OPEN tstCursor;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    FETCH tstCursor INTO i;
    SELECT i;
    CLOSE tstCursor;
END;
-- abca存储过程创建后
CALL abca();
-- 多次FETCH^
```
```sql
-- abca存储过程创建前
DROP PROCEDURE abca;
-- abca存储过程创建中
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 0;
    DECLARE ia INT DEFAULT 8;
    DECLARE tstCursor CURSOR FOR SELECT t FROM test;
    OPEN tstCursor;
    WHILE ia > 0 DO
        FETCH tstCursor INTO i;
        SET ia := ia - 1;
    END WHILE;
    SELECT i;
    CLOSE tstCursor;
END;
-- abca存储过程创建后
CALL abca();
-- 多次FETCH(简略版)^
```
```sql
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 0;
    DECLARE ia INT DEFAULT 0;
    DECLARE tstCursor CURSOR FOR SELECT t FROM test;
    SELECT COUNT(*) FROM test INTO ia;
    OPEN tstCursor;
    WHILE ia > 0 DO
        FETCH tstCursor INTO i;
        SET ia := ia - 1;
    END WHILE;
    SELECT i;
    CLOSE tstCursor;
END;
-- 查询test表里最后一个元素^
```
```sql
CREATE PROCEDURE abca()
BEGIN
    DECLARE i INT DEFAULT 0;
    DECLARE ia INT DEFAULT 0;
    DECLARE tstCursor CURSOR FOR SELECT t FROM test;
    SELECT COUNT(*) / 2 FROM test INTO ia;
    OPEN tstCursor;
    WHILE ia > 0 DO
        FETCH tstCursor INTO i;
        SET ia := ia - 1;
    END WHILE;
    SELECT i;
    CLOSE tstCursor;
END;
-- 查询test表中t字段最中间的数据^
```
```sql
SELECT t FROM test
UNION ALL
SELECT t FROM test;
-- 自联合^
```
```sql
SELECT t FROM (SELECT t FROM test UNION ALL SELECT t FROM test) tb ORDER BY t;
-- 自联合+数据自动聚组(ORDER BY)^
```
```sql
SELECT COUNT(*), t FROM (SELECT t FROM test UNION ALL SELECT t FROM test) tb GROUP BY t;
-- 查询自联合之后的test表的数据的个数^
```
```sql
SELECT 
  COUNT(*), t 
FROM
  (SELECT 
    t 
   FROM 
    test UNION ALL SELECT t FROM test
  ) tb 
GROUP BY t
ORDER BY t
LIMIT 1;
-- 查询自联合之后的test表的数据中的最小值个数^
```
```sql
SELECT 
  COUNT(*), t 
FROM
  (SELECT 
    t 
   FROM 
    test UNION ALL SELECT t FROM test
  ) tb 
GROUP BY t
ORDER BY t DESC
LIMIT 1;
-- 查询自联合之后的test表的数据中的最大值个数^
```
```sql
SELECT 
  COUNT(*) count, t item 
FROM
  (SELECT t FROM test UNION ALL SELECT t FROM test) tb 
WHERE
  t IN(SELECT MIN(t) FROM test UNION ALL SELECT MAX(t) FROM test)
GROUP BY t
-- 查询自联合之后的test表的数据中的最小值与最大值个数^
```
```sql
SELECT COUNT(*) / 2 FROM test INTO @temp;
SELECT
  t
FROM
  (SELECT ROW_NUMBER() OVER (ORDER BY t) r, t FROM test) tb
WHERE
  r = @temp;
-- 查询test表中t字段最中间的数据·番外^
```
```sql
SELECT COUNT(DISTINCT t) / 2 FROM test INTO @temp;
SELECT t
FROM
  (SELECT ROW_NUMBER() OVER (ORDER BY t) r, t FROM (SELECT DISTINCT t FROM test) tb) tb
WHERE
  r = @temp;
-- 查询test表中t字段的中间值^
```
```sql
WITH tb AS (
  SELECT ROW_NUMBER() OVER (PARTITION BY t ORDER BY t) r, t FROM test
)


SELECT t FROM tb;
-- WITH临时表的创建^
```
```sql
WITH tb AS (
  SELECT ROW_NUMBER() OVER (PARTITION BY t ORDER BY t) r, t FROM test
)

SELECT t FROM tb WHERE r = (SELECT MAX(r) FROM tb);
-- 查询test表中出现次数最多的数据^
```
```sql
WITH tb AS (
  SELECT ROW_NUMBER() OVER (PARTITION BY t ORDER BY t) r, t FROM test
)

SELECT mr, t FROM (SELECT MAX(r) mr, t FROM tb GROUP BY t) tba;
-- 查询test表中每个元素的出现次数^
```
```sql
WITH tb AS (
  SELECT ROW_NUMBER() OVER (PARTITION BY t ORDER BY t) r, t FROM test
)

SELECT t FROM (SELECT MAX(r) mr, t FROM tb GROUP BY t) tba WHERE mr = (SELECT MIN(mr) FROM (SELECT MAX(r) mr, t FROM tb GROUP BY t) tba);
-- 查询test表中出现次数最少的数据^
```
```sql
WITH tb AS (
  SELECT ROW_NUMBER() OVER (PARTITION BY t ORDER BY t) r, t FROM test
)

SELECT mr, t FROM (SELECT MAX(r) mr, t FROM tb GROUP BY t) tba ORDER BY mr DESC;
-- 把test表中每个元素的出现次数从大到小进行排序^
```
```sql
INSERT INTO gameidentity VALUES(2, 'unk');
SELECT gameidentity.identity FROM game RIGHT JOIN gameidentity ON game.identity = gameidentity.id WHERE game.name IS NULL;
-- 右外查询^
```
```sql
EXPLAIN SELECT gameidentity.identity FROM game RIGHT JOIN gameidentity ON game.identity = gameidentity.id WHERE game.name IS NULL;
-- 查询右外查询的性能^
```
```sql
INSERT INTO test VALUES(-1), (-2), (-3), (-4), (-5);
SELECT ABS(t) FROM test;
-- ABS求绝对值函数的应用^
```
```sql
INSERT INTO test VALUES(-1), (-2), (-3), (-4), (-5);
SELECT -ABS(t) FROM test;
-- 把表中数据全都转为负数^
```
```sql
SELECT -t FROM test;
-- 查询数据的相反数^
```
```sql
SELECT --t FROM test;
-- 没变化^
```
```sql
SELECT +t FROM test;
-- 也没变^
```
```sql
-- CREATE TABLE testb(
--   a INT,
--   b INT
-- );
-- INSERT INTO testb VALUES(1, 2), (2, 4), (4, 8), (8, 16), (16, 20);

SELECT IF(1 = (SELECT COUNT(*) FROM (SELECT COUNT(*) FROM testb GROUP BY a / b) tb), 'TRUE', 'FALSE') isDirectproportion;
-- 检测testb表中a和b两个数据是否成正比例关系^
```
```sql
UPDATE testb SET b = 32 WHERE a = 16;
SELECT IF(1 = (SELECT COUNT(*) FROM (SELECT COUNT(*) FROM testb GROUP BY a / b) tb), 'TRUE', 'FALSE') isDirectproportion;
-- 检测testb表中a和b两个数据是否成正比例关系2^
```
```sql
SELECT IF(1 = (SELECT COUNT(*) FROM (SELECT COUNT(*) FROM testb GROUP BY a * b) tb), 'TRUE', 'FALSE') inverseProportion;
-- 检测testb表中a和b两个数据是否成反比例关系^
```
```sql
DELETE FROM testb;
INSERT INTO testb VALUES(1, 16), (2, 8), (4, 4), (8, 2), (16, 1);
SELECT IF(1 = (SELECT COUNT(*) FROM (SELECT COUNT(*) FROM testb GROUP BY a * b) tb), 'TRUE', 'FALSE') inverseProportion;
-- 检测testb表中a和b两个数据是否成反比例关系2^
```
```sql
DELETE FROM testb WHERE (SELECT 1);
-- DELETE子句中嵌套SELECT查询语句^
```
```sql
-- INSERT INTO testa VALUES(3), (4), (5);
SELECT t FROM testa LIMIT 1 INTO @first;
DELETE FROM testa WHERE t = @first;
-- 删除testa表中的第一行^
```
```sql
SELECT t FROM (SELECT ROW_NUMBER() OVER () r, t FROM test) tb ORDER BY r DESC; 
-- 反向查询test表的数据^
```
```sql
DELETE FROM test WHERE t = (SELECT t FROM (SELECT ROW_NUMBER() OVER () r, t FROM test) tb ORDER BY r DESC LIMIT 1);
-- 删除test表中的倒数第一行^
```
```sql
DELETE FROM test WHERE t = (SELECT t FROM (SELECT ROW_NUMBER() OVER () r, t FROM test) tb ORDER BY r DESC LIMIT 1, 1); 
-- 删除test表中的倒数第二行^
```
```sql
SELECT t FROM test LIMIT 1 INTO @first;
DELETE FROM test WHERE t IN(@first, (SELECT t FROM (SELECT ROW_NUMBER() OVER () r, t FROM test) tb ORDER BY r DESC LIMIT 1)); 
-- “掐头去尾”^
```
```sql
DROP TABLE IF EXISTS testUnion;
CREATE TABLE testUnion(
    num INT UNIQUE
);
INSERT INTO testUnion VALUES(1), (2), (3);
SELECT a.num, b.num FROM testunion a INNER JOIN testunion b;
-- 获取由1~3组成的两个数的所有序列^
```
```sql
DROP TABLE IF EXISTS testUnion;
CREATE TABLE testUnion(
    num INT UNIQUE
);
INSERT INTO testUnion VALUES(1), (2), (3), (4), (5);
SELECT a.num, b.num FROM testunion a INNER JOIN testunion b;
-- 获取由1~5组成的两个数的所有序列^
```
```sql
DROP TABLE IF EXISTS testUnion;
CREATE TABLE testUnion(
    num INT UNIQUE
);
INSERT INTO testUnion VALUES(1), (2), (3);
SELECT a.num, b.num, c.num FROM testunion a INNER JOIN testunion b INNER JOIN testunion c;
-- 三表联查^
```
```sql
DROP TABLE IF EXISTS testUnion;
CREATE TABLE testUnion(
    num INT UNIQUE
);
INSERT INTO testUnion VALUES(1), (2), (3);
SELECT a.num, b.num, c.num FROM testunion a INNER JOIN testunion b INNER JOIN testunion c ON a.num != b.num AND b.num != c.num AND c.num != a.num ORDER BY a.num, b.num, c.num;
-- 获取由1~3组成的三个数的所有唯一序列^
```
```sql
DELETE FROM gameidentity WHERE id = 2;
CREATE VIEW a AS SELECT game.name, game.coins, gameidentity.identity FROM game INNER JOIN gameidentity ON game.identity = gameidentity.id;
-- 创建多表联查的视图^
```
```sql
UPDATE a SET coins = 0 WHERE name = 'S';
-- 对视图进行修改操作^
```
```sql
INSERT INTO a(name, coins) VALUES('a', 1);
UPDATE game SET identity = 0 WHERE identity IS NULL; -- 修正
-- 对视图进行插入操作^
```
```sql
CREATE VIEW b AS SELECT name, coins FROM game;
DELETE FROM b WHERE name = 'S';
-- 对视图进行删除操作^
```
```sql
CREATE VIEW c AS SELECT name, coins, identity FROM game;
SELECT c.name, c.coins, gameidentity.identity identity FROM c INNER JOIN gameidentity ON c.identity = gameidentity.id;
-- 对普通视图进行多表联查操作^
```
```sql
SHOW CREATE VIEW c;
-- 查询建视图的语句^
```
```sql
DROP VIEW IF EXISTS c;
DROP VIEW IF EXISTS d;
CREATE VIEW c AS SELECT name, coins, identity FROM game;
CREATE VIEW d AS SELECT id, identity FROM gameidentity;
SELECT c.name, c.coins, d.identity identity FROM c INNER JOIN d ON c.identity = d.id;
-- “多视图联查”^
```
```sql
DROP VIEW IF EXISTS c, d, e;
CREATE VIEW c AS SELECT name, coins, identity FROM game;
CREATE VIEW d AS SELECT id, identity FROM gameidentity;
SELECT c.name, c.coins, d.identity identity FROM c INNER JOIN d ON c.identity = d.id;
-- 上面“多视图联查”的sql语句“简写”^
```
```sql
SELECT '%', "8", '1' UNION SELECT 'a', 'b', 'c';
-- 常量查询+UNION^
```
```sql
SELECT '%', "8", '1' UNION SELECT 'a', 'b', 'c' UNION SELECT '3.14', '15926', '53589';
-- 多层UNION^
```
```sql
SELECT '%', 111, '1' UNION ALL SELECT '%', 'b', 'c';
-- “混入数字”^
```
```sql
SELECT CONCAT(1122, '111');
-- 理论上不正确的函数使用^
```
```sql
SELECT CONCAT(t, 'aaa') FROM test;
-- 理论上不正确的函数使用2^
```
```sql
SELECT LPAD(t, 10, t) FROM test;
-- 理论上不正确的函数使用3^
```
```sql
SELECT TIMESTAMP('1111-11-11', '11:11:11');
-- 将日期与时间合二为一^
```
```sql
SELECT TIMESTAMP('2000-01-01', '10:00:00');
-- 将日期与时间合二为一2^
```
```sql
SELECT CURRENT_TIMESTAMP();
-- 获取当前时间^
```
```sql
SELECT UNIX_TIMESTAMP();
-- 获取当前时间戳^
```
```sql
SELECT SIN(0);
-- 数学函数^
```
```sql
SELECT COS(0);
-- 数学函数2^
```
```sql
CREATE TABLE aaa AS SELECT 1;
-- 通过查询语句建表^
```
```sql
DROP TABLE IF EXISTS participants, aaa;

CREATE TABLE participants (
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
  name VARCHAR(20), 
  gender CHAR(1), 
  time DATETIME, 
  m FLOAT DEFAULT NULL
);

INSERT INTO participants VALUES (1, '凤皇', '男', '2020-06-17 10:04:24', 1.49), (2, '柏佳兴', '男', '2020-06-17 10:03:35', 1.07), (3, '田静', '女', '2020-06-17 10:01:29', 1.34), (4, '何平', '男', '2020-06-17 10:01:05', 1.14), (5, '李尤爱', '女', '2020-06-17 10:05:07', 1.56), (6, '束组', '男', '2020-06-17 10:02:02', 1.66), (7, '曹彼壁', '男', '2020-06-17 10:03:09', 1.62), (8, '朱翠碧', '女', '2020-06-17 10:04:03', 1.15), (9, '赵涵然', '女', '2020-06-17 10:00:22', 1.61), (10, '傅幸', '男', '2020-06-17 10:02:34', 1.41);

CREATE TABLE aaa AS SELECT id, name, gender, time, m FROM participants;
-- 表复制^
```
```sql
DROP TABLE IF EXISTS aaa;
CREATE TABLE aaa AS SELECT game.id, game.coins, game.name, gi.identity FROM game JOIN gameidentity gi ON game.identity = gi.id;
-- 二表合一^
```
```sql
USE db;
DROP DATABASE IF EXISTS a;
DROP TABLE IF EXISTS aaa;
CREATE DATABASE a;
CREATE TABLE a.aaa AS SELECT game.id, game.coins, game.name, gi.identity FROM game JOIN gameidentity gi ON game.identity = gi.id;
-- 在db数据库里创建在a数据库中的aaa表^
```
```sql
CREATE TABLE emp AS SELECT t FROM test WHERE 2 = 1;
-- 用SELECT创建空表1^
```
```sql
CREATE TABLE empa AS SELECT * FROM participants WHERE FALSE;
-- 试着用“*”和SELECT创建空表^
```
```sql
INSERT INTO participants(name, time) VALUES("", "2000-01-01");
SELECT id, name, gender, time, m FROM participants WHERE !LENGTH(name);
-- 空字符串匹配1^
```
```sql
INSERT INTO participants(name, time) VALUES("", "2000-01-01");
SELECT id, name, gender, time, m FROM participants WHERE name RLIKE '^$';
-- 空字符串匹配2^
```
```sql
SELECT id, name, gender, time, m FROM participants WHERE name RLIKE '^..$';
-- 用正则查询名字只有两个字的人^
```
