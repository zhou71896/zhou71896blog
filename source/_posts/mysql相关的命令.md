---
title: mysql相关的命令
date: 2022-05-19 14:04:59
tags: mysql

---
常用的批量修改命令

```mysql
UPDATE swjtu_excel_divide_class c
INNER JOIN (
	SELECT
		job_number,
		name
	FROM
		swjtu_base_teacher 
) AS t ON c.teacher = t.name
SET c.teacher_number=t.job_number

```

标准差，最大值，最小值，平均数

```mysql
select round(stddev(score)) from swjtu_excel_cet_f  where id
SELECT MAX(score) from swjtu_excel_cet_f where college='电气工程学院' AND score>0
SELECT MIN(score) from swjtu_excel_cet_f where college='电气工程学院' AND score>0
SELECT ROUND(AVG(score)) from swjtu_excel_cet_f where college='电气工程学院' AND score>0
```

求中位数

```mysql

SET @rowindex := - 1;
SELECT
	AVG(a.score)
FROM
	(
		SELECT
			(@rowindex := @rowindex + 1) AS rowindex,
			score
		FROM
			swjtu_excel_cet_f where score>0 and college='电气工程学院'
		ORDER BY
			score
	) a
WHERE
	rowindex IN (
		FLOOR(@rowindex / 2 + 1),
		CEIL(@rowindex / 2 + 1)
	)
```

数据库不同版本允许groupby设置

```mysql
set @@GLOBAL.sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'
```

批量插入数据

```mysql
INSERT INTO swjtu_base_unit(
	unit_name,
	unit_desc,
	unit_address,
	unit_category_code
) SELECT
	unit_name,
	unit_introduction as unit_desc,
	unit_address,
	unit_category_code
FROM
	smart_unit
WHERE
	father_id = 'bb5557f7923548c1b7bb24f134317997';
```

