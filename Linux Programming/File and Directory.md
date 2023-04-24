파일이란?
 : 데이터를 읽을 수 있는 자원, 또는 데이터를 쓸 수 있는 모든 대상
 : 일반(ordinary) 파일, 디렉토리(directory), 특수(special) 파일, 디바이스(device) 파일
 - 파일의 구분 (문서 파일 VS 이진 파일)
    - 문서 파일: ASCII문자만을 가진 일반파일 (ex .txt)
    - 이진 파일: 문자가 아닌 데이터가 들어있는 일반파일 (ex .exe)

pwd: 현재 작업 디렉토리 확인
rmdir dic: dic디렉토리 삭제 (empty상태만 가능)
mkdir dic: dic디렉토리 생성
  - ..: parent directory
  - ~: home directory
  - .: current directory

mv dic target_dic: target_dic안으로 dic이동. target_dic없으면 dic -> target_dic로 이름 변경
  - 파일도 동일
ls 명령어
  - ls -l: 파일 정보 자세히 보기
  - ls -F: 실행 파일, symbolic link확인
  - ls -a: 숨겨진 파일("."로 시작하는 파일) 포함하여 보기
  - ls -laF: 숨겨진 실행파일 포함하여 자세히 보기 (합성 가능)
  - ls -t: 최근 수정 순 보기
alias new_command 'orig_command': orig_command를 new_command로 간단하게 지정
  shell에 따라 alias new_command='orig_command'로 작성
