---
layout: page
title: rails-pacman test
description: >
hide_description: false
toc: true

---


||||
|-|-|-|
|글 작성 출처 및 참고 링크|
|Summary|Link|etc|
|MSYS2 를 통해 MinGW-W64 설치하기 (윈도우에서 사용하는 GCC) |https://vl0011.tistory.com/14||
|msys2|https://www.msys2.org/||
||||
||||
||||
||||
||||
||||
||||
||||
||||

## MSYS2 를 통해 MinGW-W64 설치하기 (윈도우에서 사용하는 GCC) 

```
//윈도우즈 에서는 c:/msys64/ 를 root(/)로 하여 실행된다.
//MSYS2 터미널에서
pacman -Syu
//터미널을 재시작 후
pacman -Su
//필요에 따라 다음 패키지를 설치
pacman -S gcc
pacman -S flex
pacman -S bison
//vim 설치
pacman -S vim
//Mingw 설치
//x86 환경이면
pacman -S mingw-w64-i686-gcc
//x64 환경이면
pacman -S mingw-w64-x86_64-gcc

