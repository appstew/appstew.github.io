## java.fedora 에 asus-linux.org 세팅


1. Fedora 36 Workstation Setup Guide
2. General Asusctl Install
3. VFIO dGPU Passthrough Guide

- 나머지는 https://asus-linux.org/ 를 따라 하면 되는데,
  기존의 리눅스에서 kvm 가상머신을 사용하였고 리눅스를 새로 설치해서 kvm 환경을 구성하는 것이라면, 다음의 사항을 신경쓰자.
1. etc/default/grub 내의 nvidia-drm.modeset=1 과 supergfxctl -m vfio(또는 integrated, hybrid) 사이의 관계

2. 새로 설치한 리눅스의 /etc/libvirt/hooks/ 및 /etc/libvirt/qemu/ , /var/lib/libvirt/qemu/ 안의 내용, 이미지 경로(2TB/images/), acpitable.bin 파일

3. 하지만 위 두가지를 하고 virt-manager 에서 실행하면 virt-manager 가 멈추고 sudo systemctl irtqemud 를 하면

```
Aug 26 20:46:55 fedora systemd[1]: Starting virtqemud.service - Virtualization qemu daemon...
Aug 26 20:46:55 fedora systemd[1]: Started virtqemud.service - Virtualization qemu daemon.
Aug 26 20:46:56 fedora virtqemud[5550]: libvirt version: 8.1.0, package: 2.fc36 (Fedora Project, 2022-03-13-01:12:58, )
Aug 26 20:46:56 fedora virtqemud[5550]: hostname: fedora
Aug 26 20:46:56 fedora virtqemud[5550]: operation failed: domain 'win10_house' is already defined with uuid c49672a5-95>
Aug 26 20:46:56 fedora virtqemud[5550]: Failed to load config for domain 'test'
Aug 26 20:50:12 fedora virtqemud[5550]: End of file while reading data: Input/output error
```
의 에러가 뜨고 이때 그냥 컴퓨터를 끄면 커널패닉에 걸리고 꺼지지를 않는다. (Alt+PrtSc+REISUB 도 안먹힘)

- 그냥 현재 vfio 모드가 아닌 hybrid 모드에 그래픽카드를 다른 모니터로 출력 중이라서 그런가보다.
  lspci -nnv 와 neofetch 에서 둘다 외장그래픽카드가 안잡히는 걸로 나왔고 실제로 virt-manager 에서도 실행하면 그런 메시지가 뜬다.

- 어쩔 수 없이 vfio 모드로 설정하고 /etc/default/grub 과 grub2fedora 의 boot/grub2/grub.cfg 안의 설정을 nvidia-drm.modeset=0 으로 설정해주었고
  supergfxctl -m vfio 로 해주고 실행. 이주 될줄 알았으나 놓친 부분:<qemu:arg value="file=2TB/qemukvm.files/root/var/lib/libvirt/images/acpitable.bin"/>

- 결국 기존 가상머신 이미지 부팅 성공!

- 이건 좀 다른 얘기지만 sudo umount target is busy 인 경우:
    - 사용자 확인: fuser -cu (target)
    - 프로세스 강제 킬: fuser -ck (target)

## 설치 및 desktop entry 위치


| 디렉토리                          |                                  | 사용권한|     |
|-------------------------------|----------------------------------|---|-----|
| /bin                          | 기본적인 명령어                         |일반 사용자||
| /sbin                         | 시스템 관리를 위한 명령어                   |슈퍼유저(root)||
| /usr/bin                      | zoom, blender 등 다수의 심링크 또는 앱소스   |일반 사용자||
| /usr/sbin                     | /sbin에 있는 명령을 제외한 시스템 관리를 위한 명령어 |슈퍼유저(root)||
| /usr/share/applications       | most .desktop files              |
| /usr/local/share/applications | jetbrains-idea.desktop           |       |
|||
|||
```bash
// 인텔리제이 설치
sudo cp ~/Downloads/<extracted_intelliJ_folder>/usr/bin/idea_ultimate
sudo ln -s /usr/bin/idea_ultimate/bin/idea.sh /usr/bin/intellij

//blender 위치
/javatest/blender/blender-3.3.0-linux-x64/blender

//
```

## 유용 사이트

| 내용                    | url |
|-----------------------|-----|
| html to markdown      |https://www.browserling.com/tools/html-to-markdown|
| 한 줄로 된 html,css,js 정렬 |https://tools.arantius.com/tabifier|
|||
|||

## blender 에서 한글 입력이 안되거나 한글 상태일 때 단축키 먹히지 않는 현상
- 일단은 포기..
```java
sudo mv /usr/share/X11/xkb/symbols/kr /usr/share/X11/xkb/symbols/kr.bk
xmodmap -pk | grep Hangul
xev
ibus-setup
xmodmap
xkeycaps
xinput
```