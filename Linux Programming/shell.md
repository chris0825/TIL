> 표준 출력
  - Redirection: 표준 출력을 파일로 보내는 것
> 파이프 라인

  : 표준 출력을 다른 프로그램의 입력으로 사용하고 할 때 사용
  - sort input | lpr: 
> 파이프 라인 분리 (tee)
  - tee [-a] files: 
> 히스토리

  : 명령 입력을 쉽게 하도록 C Shell에서 제공하는 기능
  
  : 히스토리 치환 기능 = 이전에 사용했던 명령을 다시 칠 필요 없이 고쳐서 재입력
  - history [n]: 최근 n개의 명령어 이력 보여줌
  - !!: 가장 최근에 수행한 명령어 반복 수행
  - !n: n번째 수행한 명령어 반복 수행
  - !pattern: 주어진 pattern으로 시작하는 가장 최근의 명령어 반복 수행
  