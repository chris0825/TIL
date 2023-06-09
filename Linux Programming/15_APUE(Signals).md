- Signals
  - an illegal operation(ex divide by 0)
  - apower failure
  - an alarm clock
  - the death of a child process
  - a termination request from a user(Ctrl+C)
  - a suspend request from a user(Ctrl+Z)
- Predefined Signals
  - 31 (default) signals
  - Every signal has a name
    - begin with SIG
    - SIGABRT: abort()
    - SIGALRM: alarm()
  - Actions of the default signal handler
- Signal Generation
  - Terminal-generated signals
    - CTRL+C: SIGINT
    - CTRL+Z: SIGSTP
  - Hardware excepts generate signals
    - divide by 0: SIGFPE
    - invalid memory reference: SIGSEGV
  - kill()
    - sends any signal to a process or process group
    - need to be owner or super-user
  - Software conditions
    - SIGALRM: alarm clock expires
    - SIGPIPE: broken pipe
    - SIGURG: out-of-band network data
- Handling of Signals
  - Disposition or action
    - Ignore the signal: SIGKILL(9), SIGSTOP(^Z)
    - Catch the signal
    - Let the default action apply
- Representative Signals
  - SIGART: abort
  - SIGALRM: alarm
  - SIGCHLD: 자식 프로세스는 자신이 죽을 때 부모 프로세스에게 SIGCHLD보냄
  - SIGCONT
  - SIGFPE
  - SIGILL
  - SIGINT
  - SIGKILL: 9
  - SIGPIPE
  - SIGSEGV: core dump, 잘못된 참조변수
  - SIGTERM
  - SIGSTP: ^Z
  - SIGUSR1
  - SIGUSR2
- signal Handler 등록
  - SIG_IGN(ignore): SIGKILL, SIGSTOP제외 무시
  - SIG_DFL(default)
  - user-defined function
- pid means
  - pid > 0: signal to the process whose process ID is pid
  - pid == 0: signal to the processes whose process GID equals that of sender
- Permission to send signals
  - The super-user can send a signal to any process
  - The Real or Effective UID of the sender has to equal the Real or Effective UID of the receiver
- alarm()
  - alarm() sets a timer to expire at a specified time in future: kill of the signal is to terminate to process
  - Only one alarm clock per process: 사전 등록된 알람은 새로운 값에 대체된다
- pause()
  - suspends the calling process until a signal is caught
  - 그냥 종료하던지 signal handler가 등록된 경우 해당 handler가 처리를 마친 후 리턴함
- abort()
  - 비정상적 종료
  - SIGABRT
  - 프로세스 종료전에 아무것도 정리되지 않음
- sleep()
  - 지정된 시간(초)만큼 
