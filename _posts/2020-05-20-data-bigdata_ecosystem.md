---
layout: post
title: "Big Data Ecosystem"
subtitle: "Big Data Ecosystem"
categories: data
tags: engineering
comments: true
---

## 사전 지식

하드웨어의 4가지 Key Components: CPU, MEMORY, STORAGE, NETWORK 에 개념에 대해서 먼저 이해해야 한다.

속도 별로 나열하면,
CPU OPERATION, MEMORY READ, STORAGE ACCESS, NETWORK TRIP 이다.

예를 들어 Twitter에서 생성되는 하루 동안의 코로나 관련 트윗을 활용하여 분석 수행을 Single Machine에(RAM: 8GB) 에서 작업 할 시,
1. Twitter API를 통한 네트워크 다운로드 (예: 크기는 더 방대하지만 200GB 가정)
2. STORAGE에 저장
3. STORAGE READ -> MEMORY (CPU OPERATION #1 (한 번에 8GB 만큼)
4. MEMORY에서 COVID-19 관련 트윗 EXTRACTION (CPU OPERATION #2)
5. EXTRACT 한 데이터 STORAGE WRITE (CPU OPERATION #3)

모든 200GB 데이터 처리 전까지 3~5 단계 반복을 거친다.

CPU OPERATION에 비해, STORAGE와 MEMORY 처리 속도로 인해 Bottleneck 현상이 발생한다.

이를 해결하기 위해 활용할 수 있는 것이 Distributed System이다.


##Distributed System

Single Machine 에서 작업하지 않고, 200GB의 데이터를 가용한 다른 Machine과 함께 작업한다.

이는 다음의 방법으로 수행할 수 있다.

1. 가족들의 개인 노트북에 200GB 의 데이터를 4분할하여 네트워크로 (이메일) 전송한다.
2. 각 가족들의 노트북에서 간단한 파이썬 코드를 작성하여 코로나 관련 트윗을 추출한다.
3. 추출한 트윗을 다시 내 PC로 네트워크로 전송 받는다.


간단한 분산 시스템을 활용하여 작업의 능률을 올릴 수 있다고 기대한다.


하지만, 단점이 존재한다.

1. 각 노트북의 프로그램 환경 동일 (파이썬 버전, etc)
2. 네트워크 전송 시간 (가장 오래 걸리는 프로세스)
3. 분산 처리된 데이터 집계 전까지, 최종 결과 예측 불가능
4. 각 PC에서 50GB 데이터 처리 시간 소요
   * 모든 PC의 RAM은 8기가라고 가정


다른 예를 들어보고자 한다.

사설 분산 처리 시스템에서 가용한 PC 40대를 확보하였다.

1. 각 PC에 200/40 = 5GB 만큼의 데이터 전송
2. 코로나 트윗 추출 코드 실행 
3. 결과를 내 PC로 전송


이번 경우에서 위에 언급하였던 4번 단점을 제외하고 동일하게 적용된다.
하지만 극복할 방법이 존재하고, 충분히 단점을 감수하다고 판단된다.

그 근거로,
단점 1번 : 개봘 환경 통일은 분산 시스템 구축 시 단 1번만 필요하다.
단점 2번 : 데이터 전송시간 trip 한 번만 필요하다. 또한, 5GB의 데이터를 한 번더 나누어, 
1> 2.5GB 데이터 전송
2> 2.5GB 데이터에 대한 추출 실행
3> 다른 2.5GB 데이터 전송

과 같은 방벙론을 적용할 수 있다.
단점 3번: 전체적인 데이터 처리 속도가 감소하므로 감수하다고 판단된다.


정리하면, Distributed System을 사용하여 데이터 처리를 하는 것이 효율적이다라는 결론을 얻을 수 있다.
이 때 Distributed System을 활용하는 방법으로 Hadoop 에서 적용한 MAP REDUCE와 같은 기술이 있다.

관련된 내용은 다음 포스트에서 다뤄보고자 한다.

