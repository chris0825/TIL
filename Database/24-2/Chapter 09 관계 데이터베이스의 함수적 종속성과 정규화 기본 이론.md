# 관계형 데이터베이스 설계
> '좋은'릴레이션 스키마를 생성하기 위해 애트리뷰트 그룹화
## 좋은 데이터베이스 스키마
1. 정보의 중복 X
2. 갱신 이상 X
3. 정보의 손실 X
4. 실세계를 훌륭하게 표현
5. 애트리뷰트 간 관계 표현 명확화
6. 무결성 제약조건 시행 간단히
7. 효율성

# 릴레이션 분해
- 하나의 릴레이션을 둘 이상의 릴레이션으로 분해
- 분해시 원래 릴레이션을 다시 구할 수 있어야 함
- 잘못된 분해는 이전보다 효율적이지 못할 수 있음
- 릴레이션의 분해는 함수적 종속성 지식을 기반으로 함

## 함수적 종속성(FD, Functional Dependency)
- 좋은 릴레이션 설계의 정형적 기준으로 정규화 이론의 핵심
- 2NF ~ BCNF까지 사용
- 애트리뷰트들의 의미와 애트리뷰트 간 상호 관계로부터 유도되는 제약조건
![함수적 종속성](https://github.com/chris0825/TIL/blob/main/Database/resource/%ED%95%A8%EC%88%98%EC%A0%81%20%EC%A2%85%EC%86%8D%EC%84%B1.PNG?raw=true)

# 정규화
> 주어진 릴레이션 스키마를 함수적 종속성과 기본키를 기반으로 분석하여 분해함으로써 값의 중복과 세가지 갱신이상(삽입, 삭제, 수정)을 최소화<br>
> 성능을 낮은 수준의 정규형을 선택하는 비정규화도 존재
![정규형](https://github.com/chris0825/TIL/blob/main/Database/resource/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%A0%95%EA%B7%9C%ED%99%94.PNG?raw=true)

## 제 1정규형(1NF)
> 도메인이 오직 원자값이어야함
![1NF](https://github.com/chris0825/TIL/blob/main/Database/resource/1NF%20%EC%98%88%EC%A0%9C.PNG?raw=true)
### 1NF 갱신이상
![1NF 갱신이상](https://github.com/chris0825/TIL/blob/main/Database/resource/1NF%20%EA%B0%B1%EC%8B%A0%EC%9D%B4%EC%83%81.PNG?raw=true)

## 제 2정규형(2NF)
![2NF](https://github.com/chris0825/TIL/blob/main/Database/resource/2NF%20%EC%98%88%EC%A0%9C.PNG?raw=true)
### 2NF 갱신이상
![2NF 갱신이상](https://github.com/chris0825/TIL/blob/main/Database/resource/2NF%20%EA%B0%B1%EC%8B%A0%EC%9D%B4%EC%83%81.PNG?raw=true)

## 제 3정규형(3NF)
![3NF](https://github.com/chris0825/TIL/blob/main/Database/resource/3NF%20%EC%98%88%EC%A0%9C.PNG?raw=true)
### 3NF 갱신이상
![3NF 갱신이상](https://github.com/chris0825/TIL/blob/main/Database/resource/3NF%20%EA%B0%B1%EC%8B%A0%EC%9D%B4%EC%83%81.PNG?raw=true)

## Boyce-codd정규형(BCNF)
![BCNF](https://github.com/chris0825/TIL/blob/main/Database/resource/BCNF%20%EA%B0%9C%EB%85%90.PNG?raw=true)
![BCNF 예제](https://github.com/chris0825/TIL/blob/main/Database/resource/BCNF%20%EC%98%88%EC%A0%9C.PNG?raw=true)
