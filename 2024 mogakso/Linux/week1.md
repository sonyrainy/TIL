- shutdown : 종료/다시시작
- ifconfig : 네트워크 카드 정보보기 또는 구성
- ssh(secure shell) : ssh 사용자이름@ip
<br>

- **디렉터리 내용 보기**
  
  - ls :	현재 폴더 내용 보기
  - pwd	: 현재 폴더 보기
  - cd : 폴더 전환
  - touch :	파일 없으면 새 파일 생성
  - mkdir :	디렉터리 생성
  - rm : 지정된 파일 이름 삭제
  - clear	: 화면 지우기
<br>

- **명령어를 알아야 하는 이유?**

리눅스가 처음 나왔을 때는 GUI 환경이 없었다. 따라서 디스크 작업, 파일엑세스, 디렉터리 작업, 프로세스 관리 등 모든 작업이 명령으로 완료되었다. 이 부분은 GUI로의 마우스와 키보드를 통한 명령을 타이핑으로 한 번에 여러 명령을 처리 가능하다는 점에서 유용하다. 직장/회사 에서는 많은 양의 서버 유지 관리 작업을 위해 SSH 클라이언트를 통해 원격으로 완료되며 터미널을 통한 명령어 작업은 여전히 중요하다. 유지관리가 작업 명령을 통해 완료된다고 볼 수 있다.

+) 

단일 사용자 운영체제: 동시에 한 명의 사용자만 사용 가능, 한 명의 사용자가 시스템의 모든 하드웨어 및 소프트웨어 리소스를 혼자 즐길 수 있다. ex) Windows XP의 이전 버전

다중 사용자 운영체제: 여러 사용자가 동시에 사용 가능한 컴퓨터로, 여러 사용자가 시스템의 모든 하드웨어 및 리소스를 공유한다. unix, linux는 처음부터 다중 사용자 운영체제로 설계되었다.

+) 깃의 링크를 카피해서
terminal에서 git clone [링크]를 활용하여 프로젝트를 로컬에 가져올 수 있다(복제).

- **시작과 종료하기**
  - reboot, shutdown -r now, init 6 명령으로도 재부팅이 가능하다. 
  - shutdown -P +10 : 10분 후에 종료
  - shutdown -r 22:00 : 오후 10시에 재부팅(r:reboot)
  - shutdown -c : 예약된 shutdown을 취소(cancel)
  - shutdonwn -k +15: 접속한 사용자엑 15분 후 종료 메시지를 보낸다. 실제로 종료되지는 않는다.

- 리눅스 다중 사용자 시스템

사용자를 생성하게 되면 홈 디렉터리 밑(week0의 디렉터리 계층구조 참고)으로 유저1, 유저2, 유저3.. 가 생기게 된다.
리눅스 서버 1대에는 여러 사용자가 동시에 접속한다. 슈퍼 유저에게는 사용자 생성 권한을 포함해 모든 작업이 가능하다.

- 사용자와 그룹 관련 명령어
  - adduser : 새로운 사용자 추가 한다(보통 가장 많이 사용).
```
$sudo adduser cookuser1
#adduser –uid 1111 cookuser2 : cookuser2 사용자를 생성하고, 사용자 id를 1111로 지정할 때 사용한다. 생성 후, cat /etc/passwd를 통해 cookuser2가 생성된 것을 확인할 수 있다.
#adduser –gid 1000 cookuser3 : cookuser3 사용자를 생성하고 그룹 id가 1000인 그룹에 포함한다.
#adduser –home /newhome cookuser4 : cookuser4 사용자를 생성하고 홈 디렉터리를 /newhome으로 지정한다.
#adduser –shell /bin/csh cookuser5 : cookuser5 사용자를 생성하고, 기본 셀을 /bin/csh로 지정한다.
```
+) ```$su user1``` : 사용자전환(user1으로 사용자 전환하여 작업이 가능하다. 원래 유저로 빠져나오고자 하면 exit를 사용한다.

- passwd : 사용자의 비밀번호 변경 명령어
- usermod : 사용자 속성 변경 명령어
 
ex) 
```#usermod --shell /bin/csh cookuser1``` : cookuser1 사용자의 기본 셀을 /bin/csh로 변경한다.

```#usermod --groups user1 cookuser1``` : cookuser1 사용자의 보조 그룹에 user1 그룹 추가

- userdel : 사용자 삭제 명령어
ex)
```#userdel cookuser2``` : cookuser2 사용자 삭제
```#userdel -r cookuser3``` : cookuser3 사용자 삭제 및 홈 디렉터리 삭제(권장)

- chage : 사용자의 비밀번호를 주기적으로 변경하도록 설정하는 명령어
```
#chage -l cookuser1 => cookuser1 사용자에 설정된 내용 확인
#chage -m 2 cookuser1 => cookuser1 사용자에 설정된 비밀번호를 사용해야하는 최소 일자(변경 후 최소 2일은 사용해야 함)
#chage -M 30 cookuser1 => coouser1 사용자에 설정된 비번을 사용할 수 있는 최대일자(변경후 최대 30일 사용가능)
#chage -E 2025/12/12 cookuser1 => cookuser1 사용자에 설정된 비번 만료일 (25/12/12까지 사용가능)
#chage -W 10 cookuser1 -> cookuser1 사용자에 설정된 비밀번호 만료 전 경고기간(비번 만료 10일전부터 경고메시지 출력), 지정하지 않으면 7일이 기본값
```

- groups : 사용자가 소속된 그룹을 보여주는 명령어
```
#groups -> 현재 사용자가 소속된 그룹 출력
#groups cookuser1 -> cookuser1 사용자가 소속된 그룹 출력
```
  - groupadd : 새로운 그룹 생성 명령어
```
#groupadd newgroup1 => newgroup1 그룹 생성
#groupadd -gid 222 newgroup2 => newgroup2 그룹을 생성하고 그룹 id를 2222로 지정
```
- groupmod: 그룹의 속성을 변경하는 명령어
```
#groupmod –new-name mygroup1 newgroup1 =>newgroup1 그룹의 이름을 mygroup1로 변경한다.
```
- groupdel : 그룹을 삭제하는 명령어
```
#groupdel newgroup2 => newgroup2 그룹삭제(newgroup2 그룹을 주 그룹으로 지정한 사용자가 없어야 한다.)
```
- gpasswd : 그룹의 비밀번호를 설정하거나 그룹 관리를 수행하는 명령어
```
#gpasswd mygroup1 -> mygroup1 그룹의 비밀번호를 설정한다.
#gpasswd -A cookuser1 mygroup1 => cookuser1 사용자를 mygroup1 그룹 관리자로 지정
#gpasswd -a cookuser4 mygroup1 => cookuser4 사용자를 mygroup1 그룹에 추가
#gpasswd -d cookuser4 mygroup1 =? cookuser4 사용자를 mygroup1 그룹에서 제거
```

-	chage : 사용자의 비밀번호를 주기적으로 변경하도록 설정하는 명령어
- groups : 사용자가 소속된 그룹을 보여주는 명령어
-	groupadd : 새로운 그룹을 생성하는 명령어
-	groupmod : 그룹의 속성을 변경하는 명령어
-	groupdel : 그룹을 삭제하는 명령어
-	gpasswd : 그룹의 비밀번호를 설정하거나 그룹 관리를 수행하는 명령어



- 리눅스 루트 비밀번호 재설정
1. 우분투가 실행되었다면, restart 후, esc나 shift를 연타하여 부트로더 GRUB 화면을 띄운다.
2. 2번째 옵션을 선택하고 recovery mod를 선택한다.
3. 메뉴 중 root를 선택한다. 텍스트 입력 화면에서 엔터를 치고, 나온 화면에서
```
$ mount -rw -o remount /
$ passwd root
```
를 통해 비밀번호 설정을 완료한다.

4. password updated successfully 라는 문구가 뜨면 된 것이다.
5. 재시작 하면 적용된 것을 확인 할 수 있다.


