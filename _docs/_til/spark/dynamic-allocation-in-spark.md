---
title: "Spark Dynamic Allocation 적용"
permalink: /til/spark/dynamic-allocation-in-spark
last_modified_at: 2020-07-02T11:24:39+09:00
redirect_from:
  - /theme-setup/
---
versions
- spark 2.3.1
- hadoop 2.6.5

spark 에서는 resource dynamic allocation을 공식적으로 지원한다.     

D.A를 위해서 아래의 4가지 옵션이 제공된다.
```
spark.shuffle.service.enabled
spark.dynamicAllocation.enabled
spark.dynamicAllocation.minExecutors
spark.dynamicAllocation.maxExecutors
```

별도로 구축한 yarn 위에서 spark job을 돌리는 경우 [추가적인 세팅](https://spark.apache.org/docs/latest/running-on-yarn.html#configuring-the-external-shuffle-service)이 필요하다.     

만약 CDH를 사용한다면 좀 더 간단해진다.
```
1. CDH 서비스에 spark 추가 (yarn이 설치 되어 있는 환경이라고 가정)
2. 자동으로 yarn-site.xml에 아래 세팅값이 추가됨을 확인
<property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle,spark_shuffle</value>
</property>
<property>
        <name>yarn.nodemanager.aux-services.spark_shuffle.class</name>
        <value>org.apache.spark.network.yarn.YarnShuffleService</value>
</property>
3. yarn 재시작
```

하지만 spark streaming job을 사용하는 경우 위의 설정과 함께 D.A로 잡을 실행하면 fail이 떨어진다.    
열심히 구글링하여 streaming의 경우 별도의 옵션값이 존재한다는 것을 알수있었다...     
(심지어 CDH 도큐먼트에서는 streaming의 경우 D.A 지원안한다는 말을 하고있다..ㅠㅠ)
```
spark.shuffle.service.enabled
spark.streaming.dynamicAllocation.enabled
spark.streaming.dynamicAllocation.minExecutors
spark.streaming.dynamicAllocation.maxExecutors
```

### !) 참고사항
1. spark streaming job의 경우 `spark.streaming.dynamicAllocation.enabled=true` 일 때 `--num-executors(=spark.executor.instances)` 옵션은 무시된다.
2. core 개수는 최초 잡을 올릴때 설정한 core가 그대로 유지된다.      
리서치 부족일 수도 있겠지만.. 현재까지 알아낸 바로는 core의 D.A는 안되는 듯 하다...