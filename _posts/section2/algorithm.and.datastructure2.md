---
layout: page
title: [자료구조/알고리즘] Graph/Tree/BST
description: >
hide_description: false
toc: true
---
{TOC}


## Tree

> 그래프의 여러 구조 중 단방향 그래프의 한 구조로, 하나의 뿌리로부터 가지가 사방으로 뻗은 형태가 나무와 닮아 있다고 해서 트리 구조라고 부릅니다.

> tree 마저 공부하고 마저 작성해야 한다!!

> 일단 자료구조의 6번 문제는 풀었다.

## Graph

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/eHIwtLm1M4UmTdAD0Dcid-1650937438049.png)


>그래프는 여러개의 점들이 서로 복잡하게 연결되어 있는 관계를 표현한 자료구조입니다.


Graph의 구조

    직접적인 관계가 있는 경우 두 점 사이를 이어주는 선이 있습니다.
    간접적인 관계라면 몇 개의 점과 선에 걸쳐 이어집니다.
    하나의 점을 그래프에서는 정점(vertex)이라고 표현하고, 하나의 선은 간선(edge)이라고 합니다.

다음 그림은 간단한 그래프입니다. 각각이 무엇인지 살펴보세요.

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/128AtfMJZjREQIECmElfn-1650937578560.png)

Graph의 표현 방식
인접 행렬

두 정점을 바로 이어주는 간선이 있다면 이 두 정점은 인접하다고 이야기합니다. 인접 행렬은 서로 다른 정점들이 인접한 상태인지를 표시한 행렬로 2차원 배열의 형태로 나타냅니다. 만약 A라는 정점과 B라는 정점이 이어져 있다면 1(true), 이어져 있지 않다면 0(false)으로 표시한 일종의 표입니다. 만약 가중치 그래프라면 1 대신 관계에서 의미 있는 값을 저장합니다. 위의 내비게이션 예제라면, 거리를 입력하면 좋습니다. 내비게이션 그래프를 인접 행렬로 표현하면 하단의 그림과 같습니다.

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/SAyWmBktc0YYZJsLYCd0N-1650937591858.png)


    A의 진출차수는 1개 입니다: A —> C
        [0][2] == 1
    B의 진출차수는 2개 입니다: B —> A, B —> C
        [1][0] == 1
        [1][2] == 1
    C의 진출차수는 1개입니다: C —> A
        [2][0] == 1


> Graph 마저 공부하고 마저 작성해야 한다!!

> 일단 자료구조의 7번 문제는 풀었다.


## Binary Search Tree, BST

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/5lXkI_8o71lBwRVf5fTgB-1650946641030.png)

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/zRihdNGiisf7VFn40nuoZ-1650946558070.png)

> node가 뭐고, bst 가 뭐고, 챕터 설명도 없다시피하고,
8번은, 뭐 어쩌라는건지..
BST 처음이고 뭔지..어쩌라고..
시간도 없고,,아프고