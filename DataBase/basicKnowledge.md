### 数据库基础知识

## 向某个数据库表中的添加字段：
``` 
    ALTER TABLE'数据库名'.'表名' 
     ADD COLUMN '新增字段' varchar(50) COLLATE_utf8mb4_unicode_ci DEFAULT NULL COMMENT '备注信息';
```  
## 查看数据库中表的数量:
```
SELECT count(TABLE_NAME) FROM information_schema.TABLES WHERE TABLE_SCHEMA='test';
其中test为数据库名字
```

## 修改数据库表中的备注信息:
```
/*mysql*/ ALTER TABLE 表名 MODIFY  字段名 类型 COMMENT '备注';

```

## 修改数据库表名的备注信息:
```
alter table test1 comment '修改后的表的注释';

```
