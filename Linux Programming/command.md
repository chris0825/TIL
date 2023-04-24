date: 현재 날짜와 시간 출력
  - date -u: 그리니치 날짜와 시간 출력
cal : 현재 월의 달력 출력.
  - cal year: 해당 년도 달력 출력
  - cal month year: 해당 년, 월 달력 출력

bc: 일반 계산기 (+, -, *, /, %, ^, sqrt(x))
  - bc -l: 공학용 계산기 (s(x) = sin x, c(x) = cos x, l(x) = log x, e(x) = exponential)
  - quit: 종료

users: 현재 로그인 한 사용자 확인
who: 현재 로그인 한 사용자 정보 확인(Login name, Login IP, address 등)
w: 현재 로그인 한 사용자 Job까지 출력
whoami: 자신의 Login Name확인
id: 자신의 User ID(UID), Group ID(GID) 확인
ping host_name: packet 송수신 확인
  - ping -c 10 host_name: packet 횟수 명시
cat file_name: file_name을 표준출력
  - cat file1 file2: 두 파일을 한번에 화면 출력
  - cat file1 file2 > file3: file1과 file2를 합쳐서 file3로 저장
  - cat file1 file2 file3 | more: 파일을 한번에 화면 출력 (more의 성질 부여)
grep pattern file: file 에서 pattern이 존재하는 줄 출력(대소문자 구분)
  - grep pattern file?: 파일 명에 file하고 뒤에 한글자 만 더 붙는 파일 에서 pattern검색 -> 물음표 갯수만큼 다른 문자 들어가도 검색됨
  - grep pattern file*: 파일 명이 file로 시작하는 파일에서 pattern 검색
find dirs -name "pattern": 이름이 pattern인 파일을 dirs디렉토리 집합에서 찾아서 출력
sort [-options] [-o outfile] infiles: 주어진 파일들(infiles)의 내용 정렬 -> -o outfile이 주어진 경우 정렬된 내용 outfile에 저장
  - 옵션: -r(리버스), -n(특수문자, 단어, 숫자 순 오름차순 정렬) -> 옵션은 합성 가능 ex) -rn
  - -o out_file: 해당 정렬을 out_file에 저장
split [-options] in_file [out_file]: in_file을 default = 1,000줄 단위로 분할, 출력파일 명 = xaa, xab, ..., xzz
  - 옵션: -l number (number줄 단위로 분할)
  - 출력 파일: out_file뒤에 aa~zz까지 분할된 파일만큼 붙음
wc [-options] files: files들의 줄 수[-l], 단어 수[-w], 문자 수[-c] 카운트
df: 현재 파일 시스템의 구성과 디스크 공간 할당/사용량 확인
du [-s] dirs: 디렉토리가 차지한 공간 확인 . -s붙으면 하위 폴더는 안보여주고 상위 폴더만 보임
