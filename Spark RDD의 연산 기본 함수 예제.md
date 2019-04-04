# 스파크 RDD의 연산 기본 함수 예제 #spark #filter #union #map #flatMap #distinct #intersection #subtract #reduceByKey



## **sc.textFile() 텍스트 파일 읽어오기** [SparkContext 객체]

```scala
스칼라에서 README를 spark context 객체의 textFile 메서드를 이용해 읽어오면 RDD 객체가 생성됨

scala> val inputRDD = sc.textFile("/usr/local/lib/spark/README.md")

inputRDD: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[7] at textFile at <console>:27
```





## **filter() 주어진 조건에 해당하는 데이터만 선별** [Transformation 함수]

```scala
filter 메서드는 이미 존재하는 RDD를 변경하는 것이 아니라 완전히 새로운 RDD에 대한 포인터 리턴함

scala> val sparkRDD = inputRDD.filter(line => line.contains("spark"))

sparkRDD: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[8] at filter at <console>:29



scala> val apacheRDD = inputRDD.filter(line=>line.contains("apache"))

apacheRDD: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[9] at filter at <console>:29
```





## **union() 2개 이상의 RDD를 조합함, 합집합** [Transformation 함수]

```scala
union()는 새로운 RDD 포인터를 리턴함

scala> val unionRDD = sparkRDD.union(apacheRDD)

unionRDD: org.apache.spark.rdd.RDD[String] = UnionRDD[4] at union at <console>:33
```





## **count() RDD의 데이터 갯수** [Actions 함수]

```scala
scala> sparkRDD.count()

res3: Long = 10



scala> apacheRDD.count()

res4: Long = 8



scala> unionRDD.count()

res5: Long = 18
```





## **take() RDD에서 데이터를 가져옴** [Actions 함수]

```scala
scala> inputRDD.take(3).foreach(println)

\# Apache Spark

Spark is a fast and general cluster computing system for Big Data. It provides



scala> sparkRDD.take(3).foreach(println)

<http://spark.apache.org/>

guide, on the [project web page](http://spark.apache.org/documentation.html)

["Building Spark"](http://spark.apache.org/docs/latest/building-spark.html).



scala> apacheRDD.take(3).foreach(println)

<http://spark.apache.org/>

guide, on the [project web page](http://spark.apache.org/documentation.html)

and [project wiki](https://cwiki.apache.org/confluence/display/SPARK).
```





## **sc.parallelize() 데이터세트를 넘겨주고 RDD를 생성시킴** [SparkContext 객체]

```scala
scala> val input = sc.parallelize(List(1,2,3,4)) 

input: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[5] at parallelize at <console>:27



**map() 데이터를 가공함, 반환 타입이 같지 않아도 되서 유용함** [Transformation 함수]

scala> val result = input.map(x=>x*x)

result: org.apache.spark.rdd.RDD[Int] = MapPartitionsRDD[6] at map at <console>:29



scala> println(result.collect().mkString(","))

1,4,9,16
```





## **flatMap() 각 입력 데이터에 대해 여러 개의 아웃풋 데이터 생성** [Transformation 함수]

```scala
scala> val lines = sc.parallelize(List("hello spark","hi"))

lines: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[7] at parallelize at <console>:27



scala> val words = lines.flatMap(line=>line.split(" "))

words: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[8] at flatMap at <console>:29



scala> words.first()

res11: String = hello





scala> val rdd1 = sc.parallelize(List("coffee","coffee","tea","milk"))

rdd1: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[9] at parallelize at <console>:27



scala> val rdd2 = sc.parallelize(List("coffee","cola","water"))

rdd2: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[10] at parallelize at <console>:27
```





## **distinct() 중복 제거한 RDD 반환** [Transformation 함수] shuffling

```scala
scala> rdd1.distinct().foreach(println)

milk

coffee

tea
```





## **intersection() 두개 이상의 RDD 데이터 교집합 RDD 반환** [Transformation 함수] shuffling

```scala
scala> rdd1.intersection(rdd2).foreach(println)

coffee
```







## **subtract() 첫번째 RDD 항목들 중 두 번째 RDD 항목 제외한 RDD 반환** [Transformation 함수]

```scala
scala> rdd1.subtract(rdd2).foreach(println)

milk

tea
```







## **cartesian()  카테시안 곱 계산** [Transformation 함수] shuffling

```scala
scala> rdd1.cartesian(rdd2).foreach(println)

(coffee,coffee)

(coffee,cola)

(coffee,water)

(coffee,coffee)

(coffee,cola)

(coffee,water)

(tea,coffee)

(tea,cola)

(tea,water)

(milk,coffee)

(milk,cola)

(milk,water)
```







## **sample(withReplacement,fraction,[seed]) 복원 추출/비복원 추출로 표본 뽑아냄** [Transformation 함수]

```scala
scala> rdd1.sample(false,0.5).foreach(println)

coffee

tea

milk



scala> val data = sc.parallelize(List(1,2,3,3))

data: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[29] at parallelize at <console>:27
```







## **collect() RDD의 모든 데이터 요소 리턴** [Actions 함수]

```scala
scala> data.collect()

res21: Array[Int] = Array(1, 2, 3, 3)
```







## **countByValue() RDD에 있는 각 값의 개수 리턴** [Actions 함수]

```scala
scala> data.countByValue()

res22: scala.collection.Map[Int,Long] = Map(1 -> 1, 3 -> 2, 2 -> 1)
```







## **top(n) 상위 n개 요소 리턴** [Actions 함수]

```scala
scala> data.top(2)

res23: Array[Int] = Array(3, 3)
```







## **takeSample(withReplacement,n,[seed]) 복원/비복원 추출로 n개 표본 뽑아냄** [Actions 함수]

```scala
scala> data.takeSample(false,1).take(1).foreach(println)

3
```







## **reduce(func) RDD 값들을 병렬로 병합연산, 같은 타입 리턴** [Actions 함수]

```scala
scala> data.reduce((x,y)=>x+y)

res30: Int = 9

scala> data.reduce(_+_)

res31: Int = 9
```







## **aggregate(zeroValue) reduce와 유사하나 다른 타입 리턴, 아래 예제에서는 (총합,갯수)로 리턴** [Actions 함수]

```scala
scala> data.aggregate((0,0))((x,y)=>(x._1+y,x._2+1),(x,y)=>(x._1+y._1,x._2+y._2))

res32: (Int, Int) = (9,4)
```







## **persist() 영속화, 데이터를 JVM 힙heap 영역에 객체 형태로 저장함** [캐싱 함수]

```scala
scala> val input = sc.parallelize(List(1,2,3,4,5))

input: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[38] at parallelize at <console>:27

scala> import org.apache.spark.storage.StorageLevel

import org.apache.spark.storage.StorageLevel

scala> val result = input.map(x=>x*x)

result: org.apache.spark.rdd.RDD[Int] = MapPartitionsRDD[39] at map at <console>:30

scala> result.persist(StorageLevel.DISK_ONLY)

res34: result.type = MapPartitionsRDD[39] at map at <console>:30

scala> println(result.count())

5

scala> println(result.collect().mkString(","))

1,4,9,16,25
```





