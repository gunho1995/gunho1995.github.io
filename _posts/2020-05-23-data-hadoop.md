---
layout: post
title: "Hadoop Ecosystem"
subtitle: "Big Data Ecosystem"
categories: data
tags: engineering
comments: true
---

## Hadoop Ecosystem

Distributed System 이 발전하며 빅데이터 저장과 분석을 하기 위해
개발된 Hadoop의 framework는 4가지로 구성된다.

HDFS (Hadoop Data File Storage), MAP REDUCE, YARN, HADOOP COMMON이다. 각 요소 별로
데이터 저장, 프로세싱, 리소스 매니징, 유틸리티를 담당한다.

- Hadoop 의 Map Reduce를 활용한 SQL 인터페이스 : Hive 와 같은 파생된 툴도 존재한다.


Hadoop 의 분산 처리 방법에 대해 알아보려고 한다.

1. HDFS 에 데이터를 저장한다.
2. 분산 처리를 하기 위해 HDFS의 데이터를 분활한다. 이 때 분활한 데이터 chunk를 Partition이라
지칭한다.
3. 분활된 데이터는 각 Map 프로세서에서 Map Reduce 되어 중간 데이터로 저장된다.
 - 분활된 데이터의 각 record를 읽는다.
 - 처리 목적에 맞는 key : value 형태의 tuple을 생성한다.
 - 각 Map 프로세서의 중간 결과를 key 에 대하여 shuffle -> cluster 생성
 - 각 cluster 별 key에 대하여 value 값 계산하여 reduce

Hadoop은 이 과정에서 생성되는 intermediate 데이터를 HDFs에 저장한다.

반면 Spark 는 intermediate 데이터를 Storage에 별도로 저장하지 않고, 메모리에서 intermediate 데이터에 대한
작업을 수행한다.


이와 같은 Distributed System은 계층 구조로 이루어진다.
Master 노드에서는 전체 작업을 조율하며 균등한 데이터가 각 노드에서 operation을 수행하도록 할당을 한다.

Master 노드를 cluster manager 라고 지칭하기도 한다.

Spark 에서는 세 종류의 cluster manager를 활용할 수 있는데, local 에서 작업 시 사용하는 standalone과
리소스 할당을 위한 YARN 또는 Mesos가 존재한다.
