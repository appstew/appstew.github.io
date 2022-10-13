---
---


## docker 설치
- 페도라36 에서 https://docs.docker.com/desktop/install/linux-install/ 참고하여 진행
- 관리를 위해 dnf repository 방식으로 설치
- docker engine 과 docker desktop 차이
- docker desktop 은 rpm 으로 설치했고 docker-desktop 이름으로 dnf 에 등록되어 있다.

```bash
 sudo dnf -y install dnf-plugins-core

 sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo

```
```bash
// 설치시
sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin
// 제거시
sudo dnf remove docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo rm -rf /var/lib/docker \

sudo rm -rf /var/lib/containerd


```
```
Total download size: 96 M
Installed size: 388 M
Is this ok [y/N]: y
Downloading Packages:
(1/7): docker-ce-20.10.18-3.fc36.x86_64.rpm                                                                                                         5.4 MB/s |  21 MB     00:03    
(2/7): docker-ce-rootless-extras-20.10.18-3.fc36.x86_64.rpm                                                                                         1.8 MB/s | 3.7 MB     00:02    
(3/7): docker-ce-cli-20.10.18-3.fc36.x86_64.rpm                                                                                                     4.6 MB/s |  29 MB     00:06    
(4/7): docker-scan-plugin-0.17.0-3.fc36.x86_64.rpm                                                                                                  2.5 MB/s | 3.6 MB     00:01    
(5/7): docker-compose-plugin-2.10.2-3.fc36.x86_64.rpm                                                                                               3.2 MB/s | 7.0 MB     00:02    
(6/7): libcgroup-2.0-4.fc36.x86_64.rpm                                                                                                              179 kB/s |  73 kB     00:00    
(7/7): containerd.io-1.6.8-3.1.fc36.x86_64.rpm                                                                                                      3.6 MB/s |  32 MB     00:08    
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                               9.2 MB/s |  96 MB     00:10     
Docker CE Stable - x86_64                                                                                                                            40 kB/s | 1.6 kB     00:00    
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35
 From       : https://download.docker.com/linux/fedora/gpg
Is this ok [y/N]: 
```

## kvm, type1 hypervisor, docker 등 차이
- 기존에 사용하던 kvm(kernel-based virtual machine) 은 type1 하이퍼바이저 라는 것을 알고 있었다.

## 커널과 내 페도라 환경 정리
- /nvme0n1p3/boot/ 안의 vmlinuz 및 initrd, bootloader 등 관계
- /usr/src/kernels 안의 소스

- myreact2 등 기존 문서
![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/DhSHvnlg6-1622776255323.png)

## 현재 사용자 docker 그룹에 등록(sudo 없이 사용)
sudo usermod -aG docker 사용자이름

## 코테 컨텐츠

```
sudo docker image pull docker/whalesay:latest

[dami@fedora multiverse]$ sudo docker container run --help

Usage:  docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]

docker container run --name whalesay docker/whalesay:latest cowsay boo

docker container ps -a 
// 익숙한 ls -a 를 해도 된다.

docker container rm 컨테이너 이름

docker container run -it --rm danielkraic/asciiquarium:latest


```


## 방법1. 구동중인 docker contaianer 를 이미지로 만들기
```
// systemctl httpd 가 아닌, docker image library/httpd 사용
// section4/docker 폴더에서 다음 명령어 실행
git clone git@github.com:codestates-seb/be-pacman-canvas.git


docker container run --name 컨테이너_이름 -p 818:80 httpd
// 818 이 로컬호스트의 포트
// 80 은 컨테이너의 포트
// lsof -i:818 이 아닌 lsof -i:80 해야 확인됨

docker container run -d --name httpdserver --rm -p 818:80 httpd
// -d 는 백그라운드에서 실행하게 함

//지정된 경로에서 명령어를 입력해주세요 

//src/main/resource/template
docker container cp ./ 컨테이너_이름:/usr/local/apache2/htdocs/

//src/main/resource/static
docker container cp ./ 컨테이너_이름:/usr/local/apache2/htdocs/

//localhost:818 에서 pacman 게임 실행이 됨

//지금까지 실행한 container 를 docker image 로 변환
docker container commit httpdserver my_pacman:1.0


// 생성된 이미지를 900 포트에서 실행
docker run --name my_web2 -p 900:80 my_pacman:1.0
//이후 lsof i:80 하면 두개가 실행되고
//localhost:818 및 localhost:900 모두 실행되는 것을 알 수 있다.
```

## 방법2. dockerfile 로 docker image build
```
// section4/docker/be-pacman-canvas/src/main/resources/ 안의 static templates 폴더를 안 폴더안에 옮기고
// 그 폴더 안에 Dockerfile 생성
FROM httpd:2.4 # 베이스 이미지를 httpd:2.4 로 사용합니다.
COPY ./ /usr/local/apache2/htdocs/ # 호스트의 현재 경로에 있는 파일을 생성할 이미지 /usr/local/apache2/htdocs/ 에 복사합니다.
// 그 폴더에서 터미널 실행
docker build --tag my_pacman:2.0 .

docker run --name my_web3 -p 901:80 my_pacman:2.0

// 이후 901포트, lsof -i:80 docker image ls docker container ls 확인


```

## sudo ln -s /usr/local/bin/docker /usr/local/bin/d
- docker image ls 대신 d image ls



## 이미지 실습1. 
```
git clone git@github.com:codestates-seb/SpaceInvaders.git

sudo vi Dockerfile


FROM httpd:2.4
COPY ./ /usr/local/apache2/htdocs/

//이미지 빌드
docker build -t sp1:1.0

//이미지 확인
docker image ls

//컨테이너 확인
docker container ls -a

//같은 이름으로 실행 중인 컨테이너 삭제
docker container rm sp1

//컨테이너 생성 및 실행
docker run --name sp1 -d -p 3000:80 sp1:1.0

//Lives:3

// 컨테이너 실행 후, 그 안에서 bash 실행
docker exec -it sp1 bash

// 그 bash 안에서 다음 명령어 실행
echo Lives > /data/quiz2.txt

```

portainer
//

lsof -i:80

## part2

```
// 이미지 풀 하고
d image pull sebcontents/client
d image pull 0xnsky/server-spring

// 아무 폴더에서 docker-compose.yml 만들고
// section4/docker/part2 안에 만들었다.
// 그 안에서 다음 명령어 실행

docker compose up -d
// 이후 localhost:8080 들어가면 정상적으로 실행이 된다.
// quiz3 정답은: 노트북
docker compose down


cd /

http://localhost:8080
```

## Differences between Docker Desktop for Linux and Docker Engine
-https://docs.docker.com/desktop/install/linux-install/

- While it’s possible to run both Docker Desktop and Docker Engine simultaneously, there may be situations where running both at the same time can cause issues. For example, when mapping network ports (-p / --publish) for containers, both Docker Desktop and Docker Engine may attempt to reserve the same port on your machine, which can lead to conflicts (“port already in use”).

sudo systemctl stop docker docker.socket containerd

sudo systemctl disable docker docker.socket containerd

### Switch between Docker Desktop and Docker Engine

docker context ls

If you have both Docker Desktop and Docker Engine installed on the same machine, you can run the docker context use command to switch between the Docker Desktop and Docker Engine contexts. For example, use the “default” context to interact with the Docker Engine;

docker context use desktop-linux

sudo rm /usr/local/bin/docker 

// 현재 /usr/bin/docker 를 쓰고 있고 sudo 없이 docker-desktop(gui) 및 /var/run/docker.sock 이 아닌 ~/.docker/desktop/docker.sock 으로 잘 실행된다.

docker 명령으로 하면 docker desktop 과 연동되어서 실행되고
sudo docker 명령으로 하면 docker desktop 과 연동도 안되고 나중에 port 가 이중으로 실행된다거나 container, volume 을 관리하는 폴더도 다르고 문제가 생긴다.

더 자세히 알기 전까지 일단은 sudo 없이 써야겠다. 

## gnome-software qt5 관련 에러
```
sudo dnf update qt5-qtbase
sudo dnf update gt5-gtquickcontrols
sudo dnf update gt5-gtquickcontrols2

```

## zsh 설치 with oh my zsh , and some plugins
- ~/.zshrc
- ~/.oh-my-zsh/...
```
sudo dnf install zsh

zsh

sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

Cloning Oh My Zsh...
remote: Enumerating objects: 1276, done.
remote: Counting objects: 100% (1276/1276), done.
remote: Compressing objects: 100% (1232/1232), done.
remote: Total 1276 (delta 24), reused 1195 (delta 24), pack-reused 0
Receiving objects: 100% (1276/1276), 1.06 MiB | 1.46 MiB/s, done.
Resolving deltas: 100% (24/24), done.
From https://github.com/ohmyzsh/ohmyzsh
 * [new branch]      master     -> origin/master
branch 'master' set up to track 'origin/master'.
Already on 'master'
/home/dami

Looking for an existing zsh config...
Found ~/.zshrc. Backing up to /home/dami/.zshrc.pre-oh-my-zsh
Using the Oh My Zsh template file and adding it to ~/.zshrc.

Time to change your default shell to zsh:
Do you want to change your default shell to zsh? [Y/n] ^C
y
Do you want to change your default shell to zsh? [Y/n] y
Changing your shell to /usr/bin/zsh...
[sudo] password for dami: 
Changing shell for dami.
Shell changed.
Shell successfully changed to '/usr/bin/zsh'.

         __                                     __   
  ____  / /_     ____ ___  __  __   ____  _____/ /_  
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \ 
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / / 
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/  
                        /____/                       ....is now installed!


Before you scream Oh My Zsh! look over the `.zshrc` file to select plugins, themes, and options.


```

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
// 그리고 ~/.zshrc 에서 활성화
// plugins=( [plugins...] zsh-syntax-highlighting)

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
// 마찬가지
// plugins=( 
    # other plugins...
    zsh-autosuggestions
)

// theme 설치
vi ~/.oh-my-zsh/custom/themes/passion.zsh-theme

```


## default wayland to x11
```
vi /etc/gdm/custom.conf

# GDM configuration storage

[daemon]
# Uncomment the line below to force the login screen to use Xorg
WaylandEnable=false

DefaultSession=gnome-xorg.desktop

```

