---
layout: post
title: 페도라 기타 설정하기(gnome-extensions)
category: JAVA
tags: journal
---
# 페도라 기타 설정하기

```bash
// 페도라 워크스테이션에는 윈도우나 우분투처럼 앱 최소화 버튼이 없다. 
sudo dnf install gnome-tweaks
gnome-tweaks
// gnome-extentions 사용을 추천함
sudo dnf remove gnome-tweaks
// Flatpak 리포지토리에서 Extensions를 gui 로 설치함
```

![](../../../img/fedora/Screenshot%20from%202022-08-13%2012-52-09.png)

- 그 후
- Extensions 를 연다. Extensions 는 Apps 목록에 gui 아이콘이 있기도 하고, 커맨드로는 gnome-extensions 하면 된다.

![](../../../img/fedora/Screenshot%20from%202022-08-13%2013-02-14.png)

- Applications Menu 를 On 으로 두면 위와 같이 카테고리 별로 앱리스트 버튼이 생긴다.

![](../../../img/fedora/Screenshot%20from%202022-08-13%2013-03-27.png)

- Windows List 를 On 으로 두면 위와 같이 작업표시줄이 생긴다.
