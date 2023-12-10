### 조합 논리회로와 순차 논리회로의 차이
- 조합 논리회로: 현재의 입력 값들에 의해서만 출력이 결정
- 순차 논리회로: 회로 내부의 현재 상태 값도 출력을 결정하는 요소

### 레지스터, D 플립플롭, D래치
- D래치 2개 = D 플립플롭
- D 플립플롭 병렬 배치 = 레지스터

### D래치만 사용이 불가한 이유
: 순차 논리회로의 특성상 현재 회로 내부의 상태 값이 출력을 결정하는 요소로 작용하기 때문에 쓰기 활성화 신호(WE)가 1인 동안 D래치의 출력값이 1과 0을 무한 반복함(불안정)
(따라서, 출력이 곧 입력이 되는 회로에서는 D래치 사용 불가. D 플립플롭 사용)
: 따라서 D래치 2개를 사용해 현재 출력과 입력을 분리시킨 D 플립플롭을 순차 논리회로의 기본 소자로 사용