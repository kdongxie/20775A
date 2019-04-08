# R-Server & HDInsight [Hadoop & Spark] Final Test

## Part 1. [빅데이터 수집]

### Q1. VideoShop데이터베이스의 VS_CUSTOMER테이블을 Sqoop을 사용하여 HDFS에 Import/Export하시오.


1. VS_CUSTOMER Table을 Import하는 Query 

```c
./bin/sqoop import --connect 'jdbc:sqlserver://70.12.114.147:1433;database=VideoShop' --username 'sa' --password 'Pa$$w0rd1234' --table VS_CUSTOMER -m 1 --target-dir /user/hadoop/sqoopMsSqlToHdfs
```


2. VS_CUSTOMER Table을 Export하는 Query

```c
./bin/sqoop export --connect 'jdbc:sqlserver://70.12.114.147:1433;database=VideoShop' --username 'sa' --password 'Pa$$w0rd1234' --table VS_TAPE -m 1 --export-dir /user/hadoop/sqoopMsSqlToHdfs/part-m-00000
```



## Part2. [Microsoft R 서버를 활용한 빅데이터 처리 및 분석]

### Q1. 전국 커피숍 년도별 폐업건수를 구하고 그래프로 출력하시오.

```R
coffeeshop = read.csv('coffee.csv',fileEncoding = "CP949",encoding = "UTF-8")
coffeeshop$dateOfclosure
shut = coffeeshop %>% filter(!is.na(dateOfclosure))
shut$dateOfclosure = substr(shut$dateOfclosure,0,4)
shuttotal = shut %>% group_by(dateOfclosure) %>% summarise(total = n())
plot(shuttotal)
shuttotal
```



## Part3. [HD Insight를 활용한 하둡, 스파크 엔지니어링]

### Q1. Apache Spark를 사용하여 WordCount를 구하시오. (ab40thv.txt)


1. Apache Spark shell을 실행시킨다

```c
[hadoop@server10 spark-2.3.3-bin-hadoop2.7]$ ./bin/spark-shell
```


2. 파일을 호출하여 변수에 저장한다. 

```scala
scala> val input = sc.textFile("ab40thv.txt")
```

3. 불러들인 파일 Map Reduce 하기

```scala
scala > val input_map = input.flatMap(x=>x.split(" ")).map(word=>(word,1)).reduceByKey((a, b) => a + b)
scala > val wordcounts = input_map.reduceByKey((a, b) => a + b)
scala > wordcounts.collect()
```





#### 평가기준

- R Server 및 Microsoft R Client의 작동 방식 이해
- R Client와 R Server를 사용하여 서로 다른 데이터 저장소에 저장된 큰 데이터 탐색
- 그래프 및 플롯을 사용하여 데이터 시각화
- 큰 데이터 세트 변환 및 정리
- 분석 작업을 병렬 작업으로 분할하기 위한 옵션 구현 
- 큰 데이터에서 생성 된 회귀 모델을 작성하고 평가 
- 큰 데이터에서 생성 된 파티셔닝 모델 생성, 스코어링 및 배포
- SQL Server 및 Hadoop 환경에서 R 사용 
- 기계 학습 및 알고리즘 및 언어 사용 방법
- Azure 머신러닝의 목적
- Azure 머신러닝 Studio의 주요 기능을 나열
- Azure 머신러닝에 다양한 유형의 데이터 업로드 및 탐색
- Azure 머신러닝을 사용하여 회귀 알고리즘 및 신경망을 탐색
- Azure 머신러닝을 사용하여 분류 및 클러스터링 알고리즘을 탐색
- Azure 머신러닝에서 R 및 Python을 사용하고 특정 언어를 사용할 시기를 선택
- 하이퍼 매개 변수 및 여러 알고리즘 및 모델을 탐색하고 사용하며 모델 점수를 매기고 평가
- 최종 사용자에게 Azure 머신러닝 서비스를 제공하는 방법과 Azure 머신러닝 모델에서 생성 된 데이터를 공유하는 방법
- 텍스트 및 이미지 처리를 위한 인지서비스 API를 탐색하고 사용하여 추천 응용 프로그램을 만들고 Azure 머신러닝을 사용하여 신경망 사용법을 설명
- Azure 머신러닝으로 HDInsight를 탐색하고 사용
- Azure 머신러닝을 사용하여 R and R Server를 탐색하고 R 서비스를 지원하도록 SQL Server를 배포 및 구성하는 방법

