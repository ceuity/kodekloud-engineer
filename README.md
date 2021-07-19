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
