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

예를 들어 Twitter에서 생성되는 하루 동안의 코로나 관련 트윗을 활용하여 Single Machine에서 작업 할 시,
1. Twitter API를 통한 네트워크 다운로드
2. STORAGE에 저장
3. STORAGE READ -> MEMORY (CPU OPERATION #1)
4. MEMORY에서 COVID-19 관련 트윗 EXTRACTION (CPU OPERATION #2)
5. EXTRACT 한 데이터 STORAGE WRITE (CPU OPERATION #3)

모든 데이터 처리 전까지 3~5 단계 반복을 거친다.

CPU OPERATION에 비해, STORAGE와 MEMORY 처리 속도로 인해 Bottleneck 현상이 발생한다.

이를 해결하기 위해 활용할 수 있는 것이 Distributed System이다.

