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
