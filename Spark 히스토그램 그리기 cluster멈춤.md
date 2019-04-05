sc

from pyspark import SparkContext

file1 = "wasbs:///Test_Data/51983-0.txt"
file2 = "wasbs:///Test_Data/ab40thv.txt"
file3 = "wasbs:///Test_Data/pg15578.txt"
data1 = sc.textFile(file1)
data2 = sc.textFile(file2)
data3 = sc.textFile(file3)

import pandas as pd
from collections import OrderedDict
from datetime import date
data_1 = data1.flatMap(lambda line: line.split(" ")).map(lambda x:(x,1))
data_1 = spark.sparkContext.parallelize(data_1.collect())
data01 = data_1.reduceByKey(lambda a, b: a + b).collect()

def myFunc(e):
  return e[1]
data01.sort(reverse = True , key=myFunc)
df1 = pd.DataFrame(data01)
last1= df1.head(10)
last1



data_2 = data2.flatMap(lambda line: line.split(" ")).map(lambda x:(x,1))
data_2 = spark.sparkContext.parallelize(data_2.collect())
data02 = data_2.reduceByKey(lambda a, b: a + b).collect()
def myFunc(e):
  return e[1]
data02.sort(reverse = True , key=myFunc)
df2 = pd.DataFrame(data02)
last2=df2.head(10)
last2





data_3 = data3.flatMap(lambda line: line.split(" ")).map(lambda x:(x,1))
data_3 = spark.sparkContext.parallelize(data_3.collect())
data03 = data_3.reduceByKey(lambda a, b: a + b).collect()
def myFunc(e):
  return e[1]
data03.sort(reverse = True , key=myFunc)
df3 = pd.DataFrame(data03)
last3=df3.head(10)
last3





import matplotlib.pyplot as plt
plt.hist(last1)