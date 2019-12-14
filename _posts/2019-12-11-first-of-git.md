---
layout: post
title: "Git 공부 1일차"
categories: git 공부
---

Git을 사용해 본 경험은 로컬 저장소에 진행하고 있는 프로젝트를 저장시키고, `push` 라는 명령어를 사용해 GitHub에 올리는게 전부였다.
Facebook 생활코딩 커뮤니티를 살펴보는 중 [KISA 핀테크 기술지원센터][KISA 핀테크 기술지원센터]에서 Git에 대한 세미나가 열린다는 글을 보았다.
가격은 **무료** 였기에 이 기회에 Git에 대해 배우고자 참석했다.

세미나 내용은 Git을 처음 만든 개발자, 배경, 구조, 흐름 순으로 진행되었다.

Git을 처음 만든 사람은 Linux를 만든 [리누스 토르발스][linus torvalds]라고 한다.  
~~Linux도 만들고 Git도 만든 이 사람은 천재가 아닐까 싶다..~~

Git이 처음 나온 배경은 버전을 만들 때마다, 버전의 이름들이 너무 지저분해지고, 또한 이전 버전의 자료들이 필요 할 경우 용량이 어마어마하게 커졌었다. 이러한 불편함을 해결하고자 Git이 나왔다고 한다.

구조적으론 사용자가 실제 작업을 하는 **Working Directory**, 실제 작업을 가상의 공간에 담는 **Stage Area**, Git에 작업이 기록 되어있는 **Repository**로 되어있다.

Git으로 버전관리를 하기 위해선 먼저 작업 공간을 알려줘야 한다. **Working Directory**에서 `git init`을 사용해 **.git** 디렉토리를 생성하면, Git은 '아 여기서 작업을 하는구나' 라고 인식하게 된다. 디렉토리 **.git**이 **Repository**이며, 기록을 위해 **Working Directory**의 작업들을 복사해 **Stage Area**에 넣어준 다음 **Stage Area** 작업들을 **Repository**에 기록하는 순서이다.

세미나에서 **git bash**를 사용해 ComendLine으로 Git을 다루었다.

### Git 명령어
{% highlight bash %}
git init # 작업 할 폴더에 .git 폴더 생성
git status # Git 상황 확인
git add <filename> # 가상환경에 담기
git commit -m <commit message> # Git에 기록하기
git log # 기록 확인
{% endhighlight %}

Git을 기록하기 위해서 가장 먼저 해야되는 것은 상태를 확인하는 것!! `git status`로 **Working Directory** 파일들의 생성, 수정, 삭제를 확인 할 수 있다.

**.git**에 기록 시키기 전 **Stage Area**에 담아야하니 `git add <filename>`을 사용하면 가상의 공간에 담을 수 있다.(파일 전부를 담으려면 `git add .`)
**Repository**에 기록하는 명령어는 `git commit -m <commit message>`을 사용해 가상의 공간에 담겨있는 작업들을 기록했다. `-m`옵션을 사용하지 않았을 때는 다른 입력창이 나왔는데 편의성과 세미나 시간으로 인해 자세한 건 따로 검색해봐야 할 것 같았다.(참고로 `commit -m`을 할 때 GitHub 로그인을 시켜줬어야 했다.)

이로써 Git으로 버전을 기록하는 것은 끝이 났다.

이후 `git status`로 상태를 확인하면 기록 파일들이 없는 것을 볼 수 있었고, 기록된 정보들을 보기 위해 `git log`를 사용했다.
`git log`에서 commit 옆에 숫자와 영어로 되어있는 **Commit ID**와 내가 입력한 **Commit Message** 그리고 **HEAD->master**를 볼 수 있었다.

세미나에서 **Commit ID**가 어떻게 만들어지는지도 알려주었는데, 나의 이메일과 기록한 파일, **Commit Message** 그리고 **Parent**를 합쳐 해쉬화 하여 **Commit ID**를 만든다고 한다.

## 마치며
내일은 `git reset` 명령어와 `git checkout` 그리고, **HEAD**와 **mater**에 대해서 알려준다고 한다.
살짝 맛보기로 Git은 불변하기에 파일들을 삭제하지도 변경하지도 않는다는 말로 호기심을 자극했다..

Git이 내부적으로 어떻게 돌아가는지 처음 알게 된 세미나였다. 앞으로도 Git을 써야하는 입장으로 굉장히 도움이 되었고, 같이 개발을 공부하는 사람들에게 Git을 전파해주고 싶어졌다.

[KISA 핀테크 기술지원센터]: https://onoffmix.com/event/203172
[linus torvalds]: https://ko.wikipedia.org/wiki/%EB%A6%AC%EB%88%84%EC%8A%A4_%ED%86%A0%EB%A5%B4%EB%B0%9C%EC%8A%A4