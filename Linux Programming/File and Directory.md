> 파일이란?

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
> ls 명령어
  - ls -l: 파일 정보 자세히 보기
  - ls -F: 실행 파일, symbolic link확인
  - ls -a: 숨겨진 파일("."로 시작하는 파일) 포함하여 보기
  - ls -laF: 숨겨진 실행파일 포함하여 자세히 보기 (합성 가능)
  - ls -t: 최근 수정 순 보기
>  alias
 - alias new_command 'orig_command': orig_command를 new_command로 간단하게 지정
   : shell에 따라 alias new_command='orig_command'로 작성
 - alias:  현재  alias지정된 내용 확인

> 파일 내용 확인
 - cat: 파일 내용 확면 출력
 - more: 화면 크기 단위 파일 내용 확인 (중간에 중단하려면 q)
 - head: 파일의 윗부분 내용 출력 (-n옵션으로 원하는 라인 수 설정 가능)
 - tail: 파일의 마지막부분 내용 출력 (-n 옵션으로 원하는 라인 수 설정 가능)
 - file: 파일의 유형(txt, image, exe 등)확인
> 파일/디렉토리 복사
 - cp file2 file2: file1을 file2에 복사(파일이 없으면 복사본 생성. 덮어쓰기 가능)
  - cp -i file1 file2: file1을 file2에 복사(만약 덮어쓰기 되면 할거냐고 확인 문자뜸)
  - cp [-i] files directory: files를 directory로 이동
  - cp -r dic1 dic2: dic1내용 전부 dic2로 복사
> 파일/디렉토리 삭제
 - rm files: 파일 삭제
 - rm -i files: 파일 삭제 여부 확인 후 삭제
 - rm -f files: 파일 강제 삭제(쓰기 권한 없어도 삭제됨)
 - rm -r dic: dic내에 파일 있어도 삭제
 - rm -rf dic: dic모드에 w권한 없어도 강제 삭제
> 파일 사용 권한

 :파일 사용 권한 주는 이유 = 다른 사용자의 액세스 제한, 자원 공유, 자신의 실수로부터 보호
 - 읽기(r), 쓰기(w), 실행(x)
 - 순서는 사용자(owner)+그룹(group)+모든유저(others)
 - Permission No.
  - 0 = ---
  - 1 = --x
  - 2 = -w-
  - 3 = -wx
  - 4 = r--
  - 5 = r-x
  - 6 = rw-
  - 7 = rwx
 - chmod mode_No file: file의 mode를 mode_No로 변경 (root유저는 전체, 일반 사용자는 본인 파일만 모드 변경 가능)
> 파일 비교
 - cmp file1 file2: 두 파일의 차이 여부 판단(처음 달라지는 부분 정보 출력)
 - diff file1 file2: 두 파일이 차이나는 줄 출력
> 메타 문자
 - *(asterisk): 0개 이상 차이나는 문자열에 일치
 - ?(question mark): 하나의 문자와 대응
 - [?-?](brackets): 괄호 안 문자 중 하나와 대응(?와 범위 동일)
 
