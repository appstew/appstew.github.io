1.abcd // VS code에서 저장 후 marktext 에서 불러오기 테스트

-marktext 에서 알림창이 뜨면서 불러올거냐고 알려줌

2.abcd // marktext에서 저장 후 VS code 에서 불러오기 테스트

--marktext 에서는 저장(Ctrl+s) 하면 확실하게 vs code 에서 로드됨.

-3.abcd // VS code에서 수정 후 저장 안눌러도 저장되는지 테스트

-vs code에서 수정한 내용은 저장하지 않아도 자동으로 저장이 됨

4.marktext 나 외부에서 수정 후 저장해도 vs code 껐다 켜도 로드되지 않는 문제점 발견.

-vs code 에서는 이를 git change 방식으로 처리하려는 듯한데, 여러번 저장해서 수정버전이 여러개 일 경우 잘 로드하지 못하고, 불편함

{TOC}

{:toc}

------------------------

## ##터득한 방법

- 통일성을 위해 marktext 에서 작업하자.

- marktext 설정 이미지 탭에서 prefer relative path 로 설정 후, 연 폴더를 root 로 생각했을 때 상대적인 경로, 가령 img/windows_capture 등으로 설정

- 윈도우에서 캡쳐 단축키는 Win+Shift+s 이고, 이 버튼으로 창 캡쳐 후 marktext 에서 붙여넣기를 하면 자동으로 위에 설정된 경로, 가령 img/windows_capture 에 파일 저장 후 이미지를 잘 붙여줌. 

- 하지만 VS code 에서는 위 방법으로 붙여넣기를 해도 그냥 image.png 텍스트만 달랑 붙여줌

![](../img\windows_capture\2022-07-12-08-31-13-image.png)

![](../img/windows_capture/2022-07-12-08-43-47-image.png)

## ## marktext 사용 후 장점

- 막상 써보니 너무 많은 장점이 있지만, 