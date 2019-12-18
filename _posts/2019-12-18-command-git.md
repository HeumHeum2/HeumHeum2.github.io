---
layout: post
title: "Git 명령어"
lang: ko
categories: Git 공부 명령어
---

{% highlight bash %}
git init
# 현재 디렉토리 위치에 .git 만듦.

git status
# 상태 확인.

git add <files name>
# working Directory에 있는 작업들을 Stage Area에 복사함.

git commit -m <message>
# Stage Area에 있는 작업들을 .git에 저장함.

git log
# commit 된 기록들을 보여줌.

git reset --hard <Commit ID>
# master의 내용을 입력한 Commit ID로 바뀌어 복원 및 삭제가 일어남.

git checkout <Commit ID or branch>
# HEAD가 입력한 Commit ID 또는 branch로 바뀌어 현재 작업하고 있는 버전이 바뀜.

git branch <branch name>
# 현재 위치한 곳에 branch를 만듬.

git merge <A branch located elsewhere>
# 현재 위치한 곳에서 다른 곳에 위치한 branch와 합침.

git remote add <remote name> <URL or SSH>
# 원격저장소 경로 지정.

git push -u <remote name> <branch>
# 원격저장소에 현재 branch로 파일들을 올림.

git pull
# 원격저장소에서 파일들을 가져옴.

{% endhighlight %}