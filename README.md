# kodekloud-engineer

https://kodekloud-engineer.com/

Nautilus라는 가상의 회사에서 발생하는 System 문제들을 해결해보는 사이트

- Linux File Permissions

    지정된 위치의 파일에 권한을 부여하는 문제. 단순히 실행 권한만 부여하면 안되고 읽은 후 실행하기 때문에 읽기 권한도 같이 부여해야 한다.

    `chmod +rx filename`

- Postfix troubleshooting

    `/etc/hosts` 에서 IPv6의 주소를 사용하지 않도록 주석처리

    `postfix check` 명령어로 오류를 확인할 수 있다.

- NFS Troubleshooting

    NFS 란 Networking File System의 약자로 네트워크를 이용하여 mount 하는 파일시스템을 이야기 한다.

    `systemctl status nfs-server` 명령어로 nfs 서버가 작동중인지 확인

    서버의 `/etc/exports` 파일에 공유할 폴더를 설정

    Client에서 `showmount -e [ip_addr]` 명령어로 해당 ip와 공유하고 있는 디렉토리 확인

    `mount -t nfs server_ip:dir client_dir` 로 nfs 마운트

    `mount | grep nfs` 명령어로 마운트 되었는지 확인
  
- Linux Collaborative Directories

    사용자의 그룹과 권한을 바꾸는 문제

    `chmod` 와 `chgrp` 을 이용해서 권한과 그룹을 바꿔준다.

    하위 폴더까지 해당 속성을 적용할 경우엔 `-R` flag를 사용한다.
    
- Create a group

    각 앱서버에 새로운 그룹을 만들고 유저를 추가하는 문제

    `groupadd` 명령어로 그룹을 추가한 다음 `adduser [username] -G [groupname]` 명령어로 유저를 해당 그룹에 추가할 수 있다.
    
- Linux SSH Authentication

    jump server에서 각 App Server에 ssh 인증 없이 접속할 수 있도록 하는 문제

    `ssh-keygen` 명령어로 ssh key를 생성한다.

    `ssh-copy-id username@host`   명령어로 해당 App Server에 ssh 공개키를 복사하면 ssh 인증 없이 접속할 수 있다.
    
- Create a CronJob

    CronJob을 만드는 문제

    `yum install cronie` 명령어로 Cron을 설치한 후, `crond` 서비스를 실행시킨다.

    `crontab -e` 명령어로 CronJob을 생성한다.
    
- DNS Troubleshooting

    앱서버의 DNS가 제대로 작동하지 않는 문제

    `/etc/resolv.conf` 에 구글의 기본 DNS 서버인 `8.8.8.8` 을 추가한다.
    
- Linux User Expiry

    특정 기간까지만 유효한 유저를 생성하는 문제

    `useradd -e YYYY-MM-DD user_name` 명령어로 유저를 생성한 후, `chage -l user_name` 명령어로 유저의 정보를 확인할 수 있다.
    
- Linux Banner

    리눅스 로그인 시 배너를 띄우게 하는 문제

    `/etc/motd` 파일은 유저가 로그인하거나 ssh를 통해 접속했을 때 해당 파일의 내용을 출력해준다.

    jump server에서 `scp` 명령어를 이용해 배너 파일을 각 서버에 복사한 후, sudo 권한을 얻어 해당 위치에 복사한다.

    만약 `scp`가 작동하지 않을 경우에는 `openssh-clients`를 설치하면 된다.
    
- Linux Services

    각 앱서버에 특정 패키지를 설치한 후 부팅 시 마다 실행되도록 하는 문제

    `yum` 을 이용하여 해당 패키지를 설치한 후, `systemctl enable service_name`을 이용하여 부팅 시 마다 시작될 수 있도록 한다.
    
- Linux Firewalld Rules

    방화벽에서 특정 포트로 통신할 수 있도록 해당 규칙을 추가하는 문제

    설정 파일 : `/etc/firewalld/firewalld.conf` DefaultZone public 설정

    포트 추가 : `firewall-cmd --permanent --zone=public --add-port=8083/tcp`

    [https://www.lesstif.com/system-admin/rhel-centos-firewall-22053128.html](https://www.lesstif.com/system-admin/rhel-centos-firewall-22053128.html)
    
- Linux Run Levels

    runlevel을 multi-user(CLI)에서 graphical(GUI)로 바꾸는 문제

    `systemctl get-default` 명령어로 runlevel을 확인할 수 있다.

    `systemctl set-default graphical.target` 명령어로 runlevel을 변경할 수 있다.

- Apache Troubleshooting

    각 앱서버에 있는 Apache의 문제점들을 해결하는 문제

    세 개의 서버 모두 설정 파일이 잘못되어 있어서 해당 오류를 수정하고 `httpd daemon`을 다시 실행시켜준다.

    확인해야 할 사항은 다음과 같다.

    1. 포트
    2. 서버 이름
    3. Root Directory 경로
    4. html Directory 경로

- Linux String Substitute

    특정 파일에 있는 단어를 전부 수정하는 문제

    `sed -i 's/source/dest/g' file` 명령어를 이용하여 해당 파일의 source 단어를 dest로 변경한다.

- Linux String Substitute (sed)

    특정 파일에 있는 단어를 포함한 행을 제거하거나 단어를 전부 수정하는 문제

    `sed '/source/d' input_file > output_file` 명령어를 이용하여 source 단어가 포함된 모든 행을 제거한 결과를 파일로 저장할 수 있다. 특정 단어를 정확하게 지정하고 싶을 경우 `sed '/\<source\>/d'` 를 사용한다.

    `sed 's/\<source\>/dest/g' input_file > output_file` 명령어를 이용하여 source 단어를 dest 단어로 바꿀 수 있다.

    참고 : [https://jhnyang.tistory.com/287](https://jhnyang.tistory.com/287)
    
- MariaDB Troubleshooting

    MariaDB가 초기화되지 않아 발생한 문제를 해결하는 문제

    데이터베이스 서버에 접속하여 `systemctl status mariadb` 명령어로 우선 DB가 정상적으로 실행중인지 확인한다.

    `systemctl start mariadb` 명령어로 DB를 실행시키면 에러가 발생하여 실행되지 않는다.

    `systemctl status mariadb -l` 명령어로 에러를 확인해본 결과 `/var/lib/mysql` 폴더가 제대로 초기화되지 않아서 발생하는 문제이다. 따라서 `/var/lib/mysql` 폴더를 생성한 후 권한을 부여하거나, `mysqld` 폴더를 `mysql`로 변경한다.

    수정 후 `systemctl start mariadb` 명령어를 입력하면 정상적으로 작동하는 것을 확인할 수 있다.
