---
title: flowchart
author: appstew
categories: [gojs]
tags: [typography]
math: true
mermaid: true
flowchart: true
image:
  path: /commons/devices-mockup.png
  width: 800
  height: 500
  alt: Responsive rendering of Chirpy theme on multiple devices.
---
안녕하세요~


```mermaid
graph td
A --> B
```

<div id="sample">
  <div style="width: 100%; display: flex; justify-content: space-between">
    <div id="myPaletteDiv" style="width: 100px; margin-right: 2px; background-color: #282c34;"></div>
    <div id="myDiagramDiv" style="flex-grow: 1; height: 750px; background-color: #282c34;"></div>
  </div>
<button id="SaveButton" onclick="save()">Save</button>
<button onclick="load()">Load</button>
Diagram Model saved in JSON format:
<textarea id="mySavedModel" style="width:100%;height:300px">
{ "class": "go.GraphLinksModel",
"linkFromPortIdProperty": "fromPort",
"linkToPortIdProperty": "toPort",
"nodeDataArray": [
{"category":"Comment", "loc":"360 -10", "text":"Kookie Brittle", "key":-13},
{"key":-1, "category":"Start", "loc":"175 0", "text":"Start"},
{"key":0, "loc":"-5 75", "text":"Preheat oven to 375 F"},
{"key":1, "loc":"175 100", "text":"In a bowl, blend: 1 cup margarine, 1.5 teaspoon vanilla, 1 teaspoon salt"},
{"key":2, "loc":"175 200", "text":"Gradually beat in 1 cup sugar and 2 cups sifted flour"},
{"key":3, "loc":"175 290", "text":"Mix in 6 oz (1 cup) Nestle's Semi-Sweet Chocolate Morsels"},
{"key":4, "loc":"175 380", "text":"Press evenly into ungreased 15x10x1 pan"},
{"key":5, "loc":"355 85", "text":"Finely chop 1/2 cup of your choice of nuts"},
{"key":6, "loc":"175 450", "text":"Sprinkle nuts on top"},
{"key":7, "loc":"175 515", "text":"Bake for 25 minutes and let cool"},
{"key":8, "loc":"175 585", "text":"Cut into rectangular grid"},
{"key":-2, "category":"End", "loc":"175 660", "text":"Enjoy!"}
],
"linkDataArray": [
{"from":1, "to":2, "fromPort":"B", "toPort":"T"},
{"from":2, "to":3, "fromPort":"B", "toPort":"T"},
{"from":3, "to":4, "fromPort":"B", "toPort":"T"},
{"from":4, "to":6, "fromPort":"B", "toPort":"T"},
{"from":6, "to":7, "fromPort":"B", "toPort":"T"},
{"from":7, "to":8, "fromPort":"B", "toPort":"T"},
{"from":8, "to":-2, "fromPort":"B", "toPort":"T"},
{"from":-1, "to":0, "fromPort":"B", "toPort":"T"},
{"from":-1, "to":1, "fromPort":"B", "toPort":"T"},
{"from":-1, "to":5, "fromPort":"B", "toPort":"T"},
{"from":5, "to":4, "fromPort":"B", "toPort":"T"},
{"from":0, "to":4, "fromPort":"B", "toPort":"T"}
]}
</textarea>
      <button onclick="printDiagram()">Print Diagram Using SVG</button>
    </div>

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