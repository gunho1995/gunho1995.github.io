---
layout: post
title: Spark
subtitle: Spark characteristic
categories: data
tags: engineering
comments: true
---

# SPARK

매일 생산되는 데이터는 점점 증가하고 있으며, 늘어나는 데이터를 처리하기 위해 Map Reduce와 같은 기술이 개발된다.
하지만 많은 데이터를 처리 할 수 있어도, Storage 에 read&write 한다는 제약이 존재한다.

이를 극복하기 위하여 오픈소스 Apache Spark가 개발한다

Hadoop 과 동일하게 Distributed System을 활용하기 위한 도구이다. 
하지만 intermediate 데이터를 저장장치에 저장하지 않고 memory 에서 바로 처리한다는 장점을 가지고 있다.

SPARK는 자바, Scala, Python, R, SQL API를 지원한다

그 외에 특성에 대해서 조금 더 알아보려고 한다.


## Functional Language

Spark 는 functional language이다.
Functional Language는 Distributed System 에서 강점을 가진다.

분산처리 시스템에서는 하나의 node에서 발생한 issue 가 전체 데이터의 무결성에 영향을 끼친다.
매번 문제가 생길 때 마다, 문제가 발생한 node를 발견, 오류 수정, 데이터 프로세싱 재실행을 하기 위한 비용이 매우 크다.

Functional Language는 위의 문제에 대처를 쉽게 할 수 있다

파이썬 함수와 Algebra 함수를 비교해 보면,

```
result = 0

def add_five(x):
   global result
   result = 0
   result x + 5
```

```
f(x) = x + 5
f(1) = 6
```

python code는 반복 수행할 시 값이 변하는 특성을 가진다.
반면, Algebra 함수는 수행할 때 마다 같은 결과를 반환한다.

Functional Language의 함수는 Algebra Function과 같은 형태를 가지기 때문에 side effect를 방지할 수 있다.


## Lazy Evaluation

Spark 는 데이터를 분해하여 리소스 매니저에 의해 할당된 노드에서 작업을 수행한다.

데이터 프로세싱 시 많은 procedure 가 필요한 작업을 수행한다고 가정하면, 각 procedure 마다의 결과를 memory에서 처리한다.
다른 procedure의 결과를 memory 에 계속 처리하면 어느 순간 메모리 용량의 최대 치를 초과할 것이다.

이를 막기 위해서 functional language 의 특성인 lazy evaluation이 적용된다.

즉, 프로세싱에서 필요한 tuple 을 분류만 한 뒤, 최종적으로 분류된 tuple 에 대해서만 실행을 한다는 것이다.

