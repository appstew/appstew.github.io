한줄로 된 html,js,css 파일 정렬해주는 사이트  
https://tools.arantius.com/tabifier


    master branch를 pull땡겨서 동기화 git fetch origin
    master에 엎어쓸 branch(ex.dev)로 checkout( git checkout dev)
    dev branch에서 git merge —strategy=ours master 
    commit mesage 입력
    mastar branch로 checkout - git checkout master
    master branch에서 git merge —no-ff dev 입력
    commit message 입력
