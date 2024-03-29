--- 
title: "[DS] 쇼핑몰 상품 카테고리 분류"
excerpt: 카카오 아레나 데이터 경진대회 1등 노하우 책을 참고했습니다.

categories:
    - DataScience
tags:
    - DataScience
use_math: true
toc: true
toc_sticky: true
---

# 1회 대회 살펴보기
## 1.1 대회 설명
- 다음 쇼핑하우 [https://shoppinghow.kakao.com/top](https://shoppinghow.kakao.com/top)에 있는 상품들을 사용자에게 효과적으로 노출하기 위해 일관된 분류 체계를 만들 필요가 있음. 
- 수작업으로 하기엔 너무 양이 많고 룰 베이스 분류기법을 적용하더라도 상품 커버리지와 정확도에 한계가 있음. 

### 1.1.1 상품 카테고리를 분류하는 이유
- 사용자가 원하는 상품을 빠르게 검색하고 탐색하게 하기 위해
- 대분류 > 중분류 > 소분류 > 세분류
- 키워드를 입력해 상품을 검색하면 해당 키워드가 포함된 상품이 검색되며 키워드와 관련성이 높은 순으로 정렬하여 보여주기 때문에 카테고리 정보가 매우 중요

### 1.1.2 대회 내용 설명
- 상품의 정보
    - 상품명
    - 브랜드
    - 정제된 상품명
    - 생산자명
    - 가격
    - 대표 이미지 피처
- 대회 입상자의 솔루션 대부분은 텍스트와 이미지를 모두 사용한 모델
- 32일 동안 총상금 3,000만원을 걸고 진행되어 6팀이 입상
- [https://arena.kakao.com/c/5](https://arena.kakao.com/c/5)에 공개되어 있음

## 1.2. 대회 평가 척도
-  dev 데이터셋 507,783, test 데이터셋 1,526,523개의 상품 카테고리 분류 예측 결과를 각각 제출하여 정확도 평가
- 상품마다 4단계 카테고리 예측
- 세분류로 갈수록 가중치 붙어서 점수 더 높음
- 57개 대분류 카테고리, 552개 중분류 카테고리, 3190개 소분류 카테고리, 404개 세분류 카테고리
- 모든 상품은 대분류, 중분류 값은 존재하지만 소분류, 세분류 값은 없을 수도 있음

## 1.3. 데이터셋 훑어보기
### 1.3.1 데이터셋 설명
- 3개의 데이터셋과 카테고리 매핑 정보 제공
- HDF5 파일 형식
- train 데이터셋
    - 총 8,134,818건의 데이터가 100만건 단위로 분할되어 저장
- dev 데이터셋
    - 총 507,783건의 데이터
- test 데이터셋
    - 총 1,526,523건의 데이터가 100만건 단위로 분할되어 저장

### 1.3.2 대회 데이터 탐색
- train 데이터 상품 수
    - 813만개의 상품 데이터는 19만개의 브랜드, 24만개의 제조사로 구분되어 있으며 정제된 상품명의 unique 개수는 256만개로 상품명 다음으로 유일값이 많음
- 상품 카테고리 분류 분포
    - 카테고리별 상품 수가 얼마나 편중되어 있는지 카테고리별 상품 수 그래프와 비대칭도를 측정
        - 소분류(19.2)>세분류(7.37)>중분류(5.47)>대분류(1.15) 순으로 카테고리의 상품 편중이 커짐
- 상품명에 담긴 정보
    - 상품명은 사용자가 상품을 잘 이해할 수 있게 많은 정보를 담고 있음
    - 하지만 정제되어 있지 않음
        - 띄어쓰기를 안하거나 공백 분자가 아닌 '_'로 띄어쓰기가 되어있음
    - 전처리에 주의 필요
    - 상위 입상자의 솔루션에는 서브워드 단위로 분리하는 BPE(Byte Pair Encoding) 알고리즘이 활용됨
- 사용 빈도가 높은 단어
    - 정제된 상품 명에는 카테고리 이름과 비슷한 단어들이 많이 출현됨을 확인할 수 있음
    - 정보의 생략을 의미하는 "상품상세설명, 상세정보, 별도, 상세페이지 해당없음 상품상세설명참조"와 같은 단어도 많이 포함되어 있음
- 이미지 피처 시각화
    - 이미지를 t-SNE로 차원축소 후 대분류 카테고리 기준으로 시각화한 결과 대분류 기준으로 상품들이 적절히 군집화된 것을 확인
    - 이미지를 활용하면 성능 높일 수 있음
