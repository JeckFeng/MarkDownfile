# spark python版学习笔记

- 创建DataFrame

```
from pyspark import SparkContext ,SparkConf
from pyspark.sql import SparkSession
spark = SparkSession.builder.config(conf=SparkConf()).getOrcreate()
```
 在pyspark交互式环境中不需要创建spark对象和sc对象
- 读取文件方式

	```
	- spark.read.json('')
	- spark.read.txt('')
	- spark.read.parquet('')
	```
- DataFramede保存

	```
	- df.write.txt('')
      ...
      ...
      df.write.format('txt\json\parquet').save('文件路径')
  ```
  
- DataFrame的常用操作
	- ```df.printSchema()```
	- ```df.select(df['name'],df['age']+1).show()```	# select操作
	- ```groupBy()```
	- ```df.filter(df['age']>20).show()```	# filter过滤操作
	- ```df.sort(df['age'.desc()]).show()```	# sort操作 按年龄降序排序

- RDD转换为DataFrame
	- Row对象	
	- # 必须注册为临时表才能供下面的查询使用

		```
		df.createrOrReplaceTempView('表名')
		```