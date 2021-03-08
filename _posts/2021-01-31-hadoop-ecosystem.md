--- 
title: "[Hadoop] 하둡 Ecosystem"
excerpt: 하둡 Ecosystem과 주요 프레임워크

categories:
    - Hadoop
tags:
    - Hadoop
use_math: true
toc: true
toc_sticky: true
---

## 하둡 Ecosystem

하둡은 코어 프로젝트 Hadoop Distributed File System (HDFS), MapReduce와 다양한 하둡 서브 프로젝트들이 모여서 하둡 Ecosystem을 구성하고 있습니다.

![hadoop-ecosystem](../../assets/images/hadoop/hadoop-ecosystem)

먼저 하둡 코어 프로젝트를 살펴보도록 하겠습니다

## 하둡 코어 프로젝트

하둡 코어 프로젝트의 경우 하둡을 설치하게 되면 같이 설치가 됩니다.

### Hadoop Distributed File System (HDFS)

먼저 HDFS가 무엇인지 알아보도록 하겠습니다.
HDFS는 대용량 파일을 분산된 서버에 저장하고 저장된 데이터를 빠르게 처리할 수 있도록 해주는 파일 시스템 입니다. 파일을 여러 노드에 복제해서 중복 저장 하기 때문에 데이터 유실의 위험성이 줄어들게 됩니다. 하지만 파일을 한번 생성하게 되면 수정이 어렵고 읽는 것만 가능하기 때문에 데이터의 무결성을 유지할 수 있습니다. 데이터의 수정이 불가하기 때문에 수정을 하기 위해서는 기존에 존재하는 데이터를 삭제나 이동 후 새로 생성해야합니다.  

### MapReduce



## 참고링크

[Enough is not enough 블로그 - [분산알고리즘] Hadoop(하둡) 이란?](https://eehoeskrap.tistory.com/219)

