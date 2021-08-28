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
    
- Disable root login

    root 계정을 이용한 SSH 접속을 막는 문제

    SSHD 설정 파일을 수정하여 root 계정을 이용한 SSH 접속을 막을 수 있다.

    `/etc/ssh/sshd_config` 파일에 `PermitRootLogin no` 를 추가하거나 주석을 해제한 후 `systemctl restart sshd` 명령어로 ssh 서비스를 재시작하면 된다.
    
- Setup SSL for Nginx

    서버에 Nginx 를 설치하고 SSL 설정하는 문제

    1. nginx 설치

        기본 yum repo에는 nginx 패키지가 없기 때문에 `yum install epel-release` 명령어로 EPEL Repository를 추가하거나  `/etc/yum.repos.d` 폴더에 repo 파일로 추가한다.

        `yum install nginx` 명령어로 nginx를 설치한다.

        `systemctl start nginx` 명령어로 서비스를 실행한다.

        `/usr/share/nginx/html` 폴더에 `index.html` 파일을 만든다.

    2. 방화벽 설정

        `yum install firewalld` 명령어로 방화벽을 설치한다.

        `firewall-cmd` 명령어로 http와 https 규칙을 추가한다.

        ```bash
        # firewall-cmd --zone=public --permanent --add-service=http
        # firewall-cmd --zone=public --permanent --add-service=https
        # firewall-cmd --reload
        ```

        방화벽 설정을 완료했다면 `systemctl restart nginx` 명령어로 nginx를 재시작하여 curl 등을 이용하여 http로 접속이 되는지 확인한다.

    3. SSL 설정

        `/etc/nginx/nginx.conf` 파일을 수정한다.

        ```bash
        # /etc/nginx/nginx.conf

        # add into "server" section
            server {
                listen       80 default_server;
                listen       [::]:80 default_server;
                listen       443 ssl;
                server_name  www.srv.world;
                root         /usr/share/nginx/html;

                ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
                ssl_prefer_server_ciphers on;
                ssl_ciphers ECDHE+RSAGCM:ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:!aNULL!eNull:!EXPORT:!DES:!3DES:!MD5:!DSS;
                ssl_certificate      /etc/pki/tls/certs/server.crt;
                ssl_certificate_key  /etc/pki/tls/certs/server.key;
        ```

        `ssl_certificate` 와 `ssl_certificate_key` 는 미리 주어진 키 경로를 입력하거나 해당 폴더로 복사한다.

        설정 완료 후 nginx를 재시작하여 SSL이 제대로 적용되었는지 확인한다.

        `curl -Ik https://<app-server>/`

        200 응답이 온다면 성공!

    - 참고자료

        [https://www.tecmint.com/install-nginx-on-centos-7/](https://www.tecmint.com/install-nginx-on-centos-7/)

        [https://www.server-world.info/en/note?os=CentOS_7&p=nginx&f=4](https://www.server-world.info/en/note?os=CentOS_7&p=nginx&f=4)

- Configure Local Yum repos

    yum에 Local Repository를 추가하는 문제

    yum 공식 Repo에 rpm 패키지가 없는 경우 다른 Repo를 추가하거나 local Repository를 구축해서 사용할 수 있다.

    yum의 Repository는 기본적으로 `/etc/yum.repos.d` 폴더에 존재한다.

    다음과 같이 `repo` 확장자를 가지는 파일을 만든다.

    ```
    # vi /etc/yum.repos.d/localyum.repo

    [localyum]
    name=localyum
    baseurl=file:///your_rpm_packages/folder
    enabled=1
    gpgcheck=0
    ```

    해당 과제에서는 이미 repo 설정 등에 관한 파일들이 있었기 때문에 `createrepo` 명령어를 사용하지 않았다.

    설정이 완료되면 `yum repolist` 명령어로 제대로 설정이 되었는지 확인한 후 `samba` 패키지를 설치하면 끝

    - 참고자료

        [https://letitkang.tistory.com/119](https://letitkang.tistory.com/119)

        [https://linuxstory1.tistory.com/entry/편리하게-패키지를-설치하는-YUM](https://linuxstory1.tistory.com/entry/%ED%8E%B8%EB%A6%AC%ED%95%98%EA%B2%8C-%ED%8C%A8%ED%82%A4%EC%A7%80%EB%A5%BC-%EC%84%A4%EC%B9%98%ED%95%98%EB%8A%94-YUM)

        [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-managing_yum_repositories](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-managing_yum_repositories)
        
- Linux LogRotate

    LogRotate를 이용하여 Log를 관리하는 문제

    처음에 `/etc/logrotate.d/` 폴더에 보면 여러가지 application 들의 logrotate 설정 파일들이 보일 것이다. 이 문제에서는 `haproxy` 라는 package를 설치하여 특정 기간의 로그를 저장하도록 설정하는 것이다.

    `/etc/logrotate.d/`에 존재하는 파일은 어느 기간 동안 얼만큼의 간격으로 로그를 저장할 것인지 설정할 수 있다.

    모든 app server에 해당 package를 설치한 후 logrotate 설정을 하면 끝
    
- Add Response Headers in Apache

    Apache 설정에서 헤더를 추가하여 XSS 공격 방어 등 여러가지 기능을 추가하는 문제

    `yum install -y httpd` 명령어로 Apache를 설치한 후 `/etc/httpd/conf/httpd.conf` 파일을 수정하여 port 변경 및 각종 헤더를 추가한다. 주어진 조건은 다음과 같다.

    ```html
    Header set X-XSS-Protection "1; mode=block"
    Header always append X-Frame-Options SAMEORIGIN
    Header set X-Content-Type-Options nosniff
    ```

    테스트를 위하여 `/var/www/html` 폴더에 간단한 index 파일을 생성한다.

    `curl -i http://server:port` 명령어로 헤더가 잘 설정되었는지 확인할 수 있다.
    
- Web Server Security

    Apache에서 헤더에 버전이 노출되는 문제와 Directory listing을 방지하는 문제

    - 헤더에 버전이 노출되는 문제는 `/etc/httpd/conf/httpd.conf` 파일에 다음과 같은 설정을 추가한다.

        ```bash
        ServerTokens Prod
        ServerSignature Off
        ```

    - Directory listing 방지는 마찬가지로 설정 파일에서 directory 관련 부분에서 `Options` 항목에서 `Indexes` 항목을 지워준다. ex) `Options FollowSymLinks`

- Apache Redirects

    Apache에서 Redirction을 설정하는 문제

    Apache에서는 Redirect를 이용한 방법과 Rewrite module을 이용한 두 가지 방법으로 Redirection을 설정할 수 있다. 여기서는 Redirect를 이용한 방법으로 문제를 해결하였다.

    - Redirect

        호스트 설정 파일에 다음과 같은 VirtualHost Block을 추가하여 Redirection을 설정할 수 있다. 이 문제에서는 `/etc/httpd/conf.d/main.conf` 파일로 따로 설정해주었다.

        ```
        <VirtualHost *:6100>
        	ServerName stapp01.stratos.xfusioncorp.com
        	Redirect 301 / http://www.stapp01.stratos.xfusioncorp.com:6100/
        </VirtualHost>

        <VirtualHost *:6100>
        	ServerName www.stapp01.stratos.xfusioncorp.com:6100/blog/
        	Redirect 302 /blog/ http://www.stapp01.stratos.xfusioncorp.com:6100/news/
        </VirtualHost>
        ```

    - Rewrite module

        위와 마찬가지로 VirtualHost Block에서 다음과 같이 설정하여 Redirection을 설정할 수 있다.

        ```
        <VirtualHost *:6100>
        	RewriteEngine on
        	RewriteBase /
        	rewritecond %{http_host} ^domain.com [nc]
        	rewriterule ^(.*)$ http://www.domain.com/$1 [r=301,nc]
        </VirtualHost>
        ```

    HTTP Response Status Code에 따라 해당 페이지가 영구적으로 이동되었는지, 임시적으로 이동되었는지 구분할 수 있다.

    응답 코드는 영구적으로 이동했을 경우 301, 임시적으로 이동했을 경우 302를 사용한다.
    
- Linux Find Command

    특정 폴더에서 특정 확장자만 가진 파일만 복사하는 문제. 파일의 디렉토리 구조를 그대로 유지해야 한다.

    ```bash
    find /var/www/html/ecommerce -type f -name "*.js" -exec cp --parents {} /ecommerce \;
    ```

    `find` 의 `-exec` 옵션을 사용하면 `find`의 output을 input으로 넘길 수 있다. 계층 구조를 유지해야 하기 때문에 `cp` 의 `--parents` flag를 사용했고, `find` 의 결과는 `{}`로 넘겨져서 한 줄씩 실행된다. `\;` 는 `-exec` 옵션의 끝을 나타낸다.
    
- Linux GPG Command

    GnuPG 를 이용하여 암호화/복호화에 대해 배우는 문제

    이 문제에서는 공개 키와 비밀 키가 주어지고 해당 키를 이용하여 주어진 파일을 암호화/복호화 하는 문제이다.

    - 주어진 key file import

        ```bash
        gpg --import private.asc
        ```

    - key list 조회

        ```bash
        gpg --list-keys # 공개 키 조회
        gpg --list-secret-keys # 비밀 키 조회
        ```

    - Encrypt

        ```bash
        gpg --encrypt -r kodekloud@kodekloud.com --armor < encrypt_me.txt -o encrypted_me.asc
        ```

        - `-r` : `--recipient` 어떤 User의 key를 이용하여 Encrypt 할 것인지
        - `--armor` : 아스키코드로 출력. 해당 옵션을 사용하지 않을 시 Binary file로 생성
        - `-o` : 출력 파일명
    - Decrypt

        ```bash
        gpg --decrypt decrypt_me.asc > decrypted_me.txt
        ```

    암호화된 파일을 복호화한 후 cat 명령어를 이용하여 확인해보면 정상적으로 복호화 된 것을 확인할 수 있다.

    - 참고자료 : [https://johngrib.github.io/wiki/gpg/](https://johngrib.github.io/wiki/gpg/)
    
- Linux Bash Scripts

    Shell Script 를 이용하여 특정 작업을 자동화하는 문제

    App Server에서 zip 을 이용하여 백업 파일을 생성하고, 해당 파일을 scp를 이용해 Backup Server로 복사할 수 있는 스크립트를 만들면 된다.

    ```bash
    #!/bin/bash

    zip -r /backup/xfusioncorp_beta.zip /var/www/html/beta
    scp /backup/xfusioncorp_beta.zip clint@stbkp01:/backup
    ```

    scp 명령어를 사용할 때 ssh 인증이 필요하지 않도록 미리 `ssh-copy-id`를 이용하여 ssh key를 copy해두어야 한다.

- Install Package

    모든 앱서버에 `epel-release` package를 설치하는 문제

    EPEL(Extra Packages for Enterprise Linux)은 Fedora Project에서 제공되는 저장소로 각종 패키지의 최신 버전을 제공하는 community 기반의 저장소로, RHEL의 패키지 정책은 보수적이고 안정성 위주라 패키지 업데이트가 잘 되지 않는다.

    이전에는 rpm 패키지를 다운로드 받아서 설치해야 했던 것으로 보이나, 지금은 `yum install epel-release` 명령어로 바로 다운로드 가능하며, `yum repolist` 명령어로 정상적으로 설치되었는지 확인할 수 있다.
    
- Linux Configure sudo

    특정 유저에게 sudo 권한을 주는 문제

    CentOS에서 유저에서 sudo 권한을 부여하는 방법은 두 가지가 있다.

    1. `wheel` 그룹에 사용자 추가

        `usermod -aG wheel {username}`

        `sudo whoami` : 이 명령은 암호를 입력하라는 메세지를 표시하며, 암호가 정확하고 사용자가 `wheel` 그룹에 있으면 `root` 가 터미널에 출력된다.

    2. `Sudoers` 파일에 사용자 추가

        sudo 권한을 가진 사용자는 `/etc/sudoers` 파일에서 구성된다. 따라서 sudoers 파일을 수정하거나 `/etc/sudoers.d` 디렉토리에 새 구성 파일을 추가하여 sudo 사용자를 추가할 수 있다.

        `visudo` 명령을 사용하여 `/etc/sudoers` 파일을 편집한다. `visudo` 명령어는 저장하기 전에 파일의 구문 오류를 확인한다.

        `/etc/sudoers` 파일의 가장 마지막 줄에 다음과 같이 추가한다.

        ```bash
        username ALL=(ALL) NOPASSWD:ALL
        ```

        암호 없이 특정 명령어만 수행하게 할 경우에는 다음과 같이 설정한다.

        ```bash
        username ALL=(ALL) NOPASSWD:/bin/mkdir,/bin/rmdir
        ```

    - 참고자료 : [https://www.delftstack.com/ko/howto/linux/how-to-add-sudo-users-in-centos/](https://www.delftstack.com/ko/howto/linux/how-to-add-sudo-users-in-centos/)

- Application Security

    `iptables` 를 이용하여 특정 포트를 허용/차단하도록 설정하는 문제

    Apache는 3000포트로, Nginx는 8094포트로 연결되어 있을 때, 3000번 포트는 막고 8094번 포트는 열어주는 것이 목적이다.

    `iptables` 명령어를 이용하여 규칙을 설정할 수 있다.

    - `iptables -A INPUT -p tcp --dport 8094 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT`
        - `-A` : 맨 아래에 규칙을 추가
        - `-p` : Protocol
        - `-m state --state` : 패킷의 상태와 목적에 따라 제어
            - NEW : 새로 접속을 시도하는 패킷
            - ESTABLISHED : 접속을 한 상태의 패킷
            - INVALIED : 유효하지 않은 패킷
            - RELATED : 접속에 연관성을 가지는 패킷 ex) FTP 접속 패킷, ICMP 에러 메세지
    - `iptables -A INPUT -p tcp --dport 3000 -m conntrack --ctstate NEW -j REJECT`

    설정 후 `iptables -L --line-numbers` 명령어로 규칙을 확인할 수 있다. 확인 결과, 이 문제에서는 5번에 reject 되어있는 규칙이 있어서 해당 규칙을 수정해줄 필요가 있다.

    `iptables -R INPUT 5 -p icmp -j REJECT` 해당 규칙을 설정하고 나면 `service iptables save` 명령어로 규칙을 저장한다.

    `telnet` 을 이용하여 접속을 시도해보면 3000 포트는 닫혀있고 8094 포트는 열려있는 것을 확인할 수 있다.
    
- Linux Postfix Mail Server

    `postfix` 와 `dovecot` 을 이용하여 메일서버를 설정하는 문제

    - `postfix` : 메일을 주고받는 서버
    - `dovecot` : 메일을 관리하는 서버
    1. `postfix` 설치 및 설정

        `yum install -y postfix`

        ```bash
        # /etc/postfix/main.cf

        # 76 lines
        myhostname = stmail01.stratos.xfusioncorp.com

        # 83 lines
        mydomain = stratos.xfusioncorp.com

        # 99 lines
        myorigin = $mydomain

        # 113 lines
        inet_iterfaces = all

        # 116 lines comment

        # 165 lines uncomment

        # 264 lines
        mynetworks = 172.16.238.0/24, 127.0.0.0/8

        # 419 lines
        home_mailbox = Maildir/
        ```

        `systemctl start postfix`

        `systemctl status postfix`

    2. 유저 추가

        `useradd {username}`

        `passwd {password}`

    3. 메일서버 작동 테스트

        ```bash
        telnet stmail01 25
        220 stmail01.stratos.xfusioncorp.com ESMTP Postfix
        EHLO localhost
        250-stmail01.stratos.xfusioncorp.com
        250-PIPELINING
        250-SIZE 10240000
        250-VRFY
        250-ETRN
        250-ENHANCEDSTATUSCODES
        250-8BITMIME
        250 DSN
        mail from:username@stratos.xfusioncorp.com
        250 2.1.0 Ok
        rcpt to:username@stratos.xfusioncorp.com
        250 2.1.5 Ok
        DATA
        354 End data with <CR><LF>.<CR><LF>
        test mail
        .
        250 2.0.0 Ok: queued as DBD7E11F7418
        quit
        221 2.0.0 Bye
        ```

        메일은 해당 계정으로 로그인하여 위에서 설정한 `Maildir` 폴더의 `new` 폴더에 있을 것이다.

    4. `devocat` 설치 및 설정

        ```bash
        # /etc/dovecot/dovecot.conf

        # 24 lines uncomment
        ```

        ```bash
        # /etc/dovecot/conf.d/10-mail.conf

        # 24 lines uncomment
        ```

        ```bash
        # /etc/dovecot/conf.d/10-auth.conf

        # 10 lines uncomment

        # 100 lines
        auth_mechanisms = plain login
        ```

        ```bash
        # /etc/dovecot/conf.d/10-master.conf

        # 89-92 lines
        unix_listener auth-userdb {
          #mode = 0666
          user = postfix
          group = postfix
        }
        ```

        `systemctl start dovecot`

        `systemctl status dovecot`

    5. `dovecot` 작동 테스트

        ```bash
        telnet stmail01 110
        +OK Dovecot ready.
        user {username}
        +OK
        pass {password}
        +OK Logged in.
        retr 1
        +OK 513 octets
        """
        mail
        """
        quit
        ```

    6. 열려있는 포트 확인

        `ss -tulnp`

    검색해보니 `postfix` 와 `dovecot` 을 이용해서 서버를 구축하는 내용들이 많이 나와서 해당 방법을 이용하여 시도해보았으나 실패하여 다음 영상을 보고 해결했다.

    참고자료 : [https://www.youtube.com/watch?v=kdcUfw5vJKY&t=4s](https://www.youtube.com/watch?v=kdcUfw5vJKY&t=4s)
    
- Install and Configure PostgreSQL

    PostgreSQL 을 설치하고 기본 설정을 하는 문제

    - 해결해야 할 조건
        - db 서버에 PostgreSQL 설치

            ```bash
            yum install postgresql-server postgresql-contrib
            postgresql-setup initdb
            systemctl enable postgresql && sudo systemctl start postgresql
            systemctl status postgresql

            sudo -u postgres psql postgres
            ```

            첫 로그인은 `postgres` 라는 유저로 로그인 하여 PostgreSQL에 접속한다.

        - 패스워드가 있는 유저 생성

            ```sql
            CREATE USER kodekloud_aim WITH PASSWORD 'dCV3szSGNA';
            ```

        - 생성된 유저가 모든 권한을 가지고 있는 DB 생성

            ```sql
            CREATE DATABASE kodekloud_db8;
            GRANT ALL PRIVILEGES ON DATABASE "kodekloud_db8" to kodekloud_aim;
            ```

        - [localhost](http://localhost) 에 DB 연결

            `sudo vi /var/lib/pgsql/data/postgresql.conf` 파일 수정

            Uncomment `listen_address=localhost`

        - md5를 이용한 암호화

            `sudo vi /var/lib/pgsql/data/pg_hba.conf` 파일 수정

            ```bash
            local all all md5
            host all all 127.0.0.1/32 md5
            ```

        설정 완료 후 서비스 재시작하면 다음 명령어로 접속이 정상적으로 되는지 확인할 수 있다.

        `psql -U kodekloud_aim -d kodekloud_db8 -h 127.0.0.1 -W`

        `psql -U kodekloud_tim -d kodekloud_db8 -h localhost -W`
        
- Install And Configure SFTP

    sftp를 위한 계정을 만들고 설정하는 문제

    CentOS에는 기본적으로 ssh와 같이 sftp도 설치되어 있기 때문에 별도로 설치할 필요가 없다.

    1. 계정 생성
        - `useradd -s /sbin/nologin -G ftp {username}`
    2. 패스워드 변경
        - `passwd {username}`
        - `echo 'password' | passwd --stdin username`
    3. chroot 적용 & Password authentication
        - `/etc/sshd/sshd_config` 파일을 다음과 같이 수정한다.

            ```bash
            Subsystem	sftp	internal-sftp
            Match User {username}
            ChrootDirectory /var/www/nfsshare
            ForceCommand internal-sftp
            PasswordAuthentication yes
            ```

    4. 서비스 재시작

        `systemctl restart sshd`

    참고자료 : [https://zetawiki.com/wiki/SFTP만_되는_계정_생성](https://zetawiki.com/wiki/SFTP%EB%A7%8C_%EB%90%98%EB%8A%94_%EA%B3%84%EC%A0%95_%EC%83%9D%EC%84%B1)
    
- Install and Configure Tomcat Server

    Apache Tomcat을 설치하고 설정하는 문제

    1. App Server에 Tomcat 설치

        `yum install tomcat` 명령어로 Tomcat을 설치하면 `/usr/share/tomcat` 에 설치가 완료된다.

    2. 포트 설정

        `/usr/share/tomcat/conf/server.xml` 파일의 `<Connector port="6400"` 부분을 원하는 포트로 변경한다.

    3. war 파일 이동

         jump host에 있는 `ROOT.war` 파일을 앱서버로 복사한 후, Apache Tomcat을 설치하여 배포할 수 있도록 설정해야 한다. 따라서 `scp` 명령어를 이용해 먼저 앱서버로 해당 파일을 복사해준다.

        `/usr/share/tomcat/webapps` 경로에 war 파일을 넣으면 해당 파일을 이용하여 해당 프로젝트를 배포할 수 있다. 파일 명이 곧 URL이 되지만, `ROOT.war` 로 할 경우에는 최상위 도메인으로 연결된다.

    4. 서비스 실행

        `systemctl enable tomcat`

        `systemctl start tomcat`

    참고자료 : [https://its-easy.tistory.com/4](https://its-easy.tistory.com/4)

- IPtables Installation And Configuration

    `iptables`를 이용하여 네트워크 정책을 설정하는 문제

    기존에는 외부에서 앱서버에 직접적으로 접근이 가능했으나, 설정을 통해 로드밸런서를 통하여 통신을 하게 만드려고 한다. 따라서 각 앱서버에서 로드밸런서의 IP 주소의 접근만 허용하고 나머지는 거부하도록 설정해야 한다.

    `iptables -L` 명령어로 현재 설정된 규칙을 확인해보면 기본적으로 REJECT rule이 설정되어 있기 때문에 ACCEPT rule을 REJECT rule 보다 상위에 설정해주어야 한다.

    ```bash
    # install package
    yum install -y iptables-services

    # start service
    systemctl enable iptables
    systemctl start iptables

    # rule setting
    iptables -I INPUT 5 -p  tcp --dport 8084 -s 172.16.238.14 -j ACCEPT
    iptables -A INPUT -p  tcp --dport 8084 -j DROP

    service iptables save
    systemctl restart iptables
    ```

    위와 같이 설정한 후 해당 앱서버로 접근은 불가하지만 로드밸런서를 통한 접근은 가능한 것을 확인할 수 있다.
