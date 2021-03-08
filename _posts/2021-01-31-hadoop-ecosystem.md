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

하둡은 코어 프로젝트 Hadoop Distributed File System (HDFS), MapReduce와 다양한 하둡 서브 프로젝트들이 모여서 하둡 Ecosystem을 구성하고 있습니다. 모든 서브 프로젝트를 다 사용할 필요는 없고 필요한 프로젝트를 선택하여 사용할 수 있습니다. 

![hadoop-ecosystem](../../assets/images/hadoop/hadoop-ecosystem)

오늘은 먼저 하둡의 코어 프로젝트들부터 살펴보도록 하겠습니다.

## 하둡 코어 프로젝트

### HDFS

HDFS는 말 그대로 하둡이 데이터를 분산 저장하는 저장소 입니다. HDFS는 블록 구조의 파일 시스템 입니다. HDFS는 파일을 저장할 때 그대로 저장하는 것이 아닌 설정된 blocksize로 파일을 쪼개어 block단위로 저장합니다. Default blocksize는 64mb, hadoop2부터는 default로 128mb로 설정되어 있으며 필요에 따라 크기를 늘리거나 줄일 수 있습니다. 또한 이 블록을 한곳에 모두 저장하는 것이 아닌 여러 서버에 중복해서 저장하기 때문에 데이터 유실이나 서버의 장애의 의한 손실을 줄일 수 있습니다. 데이터는 기본으로 블록당 3번씩 복제하게 설정되어 있고 복제 횟수 또한 설정할 수 있습니다. 이렇게 데이터를 쪼개어서 저장하기 때문에 데이터가 저장되는 한 개의 서버의 용량을 초과하여 저장할 수 있습니다. 물론 데이터의 크기는 연결된 모든 서버의 저장공간의 합 보다는 작아야 합니다.

Blocksize는 비교적 크게 설정되어 있는데 이것은 disk seek time을 줄이고 후에 설명하게 될 NameNode에 저장되는 메타데이터의 크기를 줄이기 위해서입니다. 또한 blocksize를 크게 함으로써 client와 NameNode의 통신을 감소시킬 수 있습니다.

HDFS는 다음 4가지의 목표를 갖고 설계되었습니다.

1. 장애복구

    장애를 빠른 시간에 감지하고 대처할 수 있게 설계되어있습니다. HDFS에 데이터를 저장하면 복제 데이터도 함께 저장되어 데이터 유실을 방지합니다. 또한 분산 서버 간에 주기적으로 상태를 체크하여 빠른 시간에 장애를 인지하고 대처할 수 있게 도와줍니다.

2. 스트리밍 방식의 데이터 접근

    HDFS는 클라이언트의 요청을 빠른 시간 내에 처리하는 것 보다 동일한 시간 내에 더 많은 데이터를 처리하는 것을 목표로 하고 있습니다.

3. 대용량 데이터 저장

    HDFS는 하나의 파일 크기의 제한이 없기 때문이 기가바이트에서 테라바이트 이상의 크기로 저장될 수 있게 설계되었습니다. 

4. 데이터 무결성

    HDFS는 데이터의 입력이나 변경 등을 제한해 데이터의 안정성을 저해하는 요소를 막고 있습니다. HDFS에는 한번 저장한 데이터는 변경이 불가능합니다. 대신 파일 이동이나 삭제, 복사는 가능하기 때문에 기존 파일을 변경하고 싶다면 먼저 삭제 후 새로 저장 해야합니다.

HDFS는 master-slave 아키텍쳐를 갖고 있습니다. 메타데이터 관리와 데이터노드를 모니터링 하는 마스터 서버인 **NameNode**와 client가 HDFS에 저장하는 파일을 로컬 디스크에 유지하는 **DataNode**로 나뉘어져 있습니다. 

**NameNode**

NameNode의 역할은 4가지 입니다.
1. 메타데이터 관리
2. DataNode 모니터링
3. Block 관리
4. Client 요청 접수

### Hadoop Distributed File System (HDFS)

먼저 HDFS가 무엇인지 알아보도록 하겠습니다.
HDFS는 대용량 파일을 분산된 서버에 저장하고 저장된 데이터를 빠르게 처리할 수 있도록 해주는 파일 시스템 입니다. 파일을 여러 노드에 복제해서 중복 저장 하기 때문에 데이터 유실의 위험성이 줄어들게 됩니다. 하지만 파일을 한번 생성하게 되면 수정이 어렵고 읽는 것만 가능하기 때문에 데이터의 무결성을 유지할 수 있습니다. 데이터의 수정이 불가하기 때문에 수정을 하기 위해서는 기존에 존재하는 데이터를 삭제나 이동 후 새로 생성해야합니다.  

### MapReduce



## 참고링크

[Enough is not enough 블로그 - [분산알고리즘] Hadoop(하둡) 이란?](https://eehoeskrap.tistory.com/219)

[시작하세요! 하둡 프로그래밍 - 빅데이터 분석을 위한 하둡 기초부터 Yarn까지, 정재화 지음](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158390389)

