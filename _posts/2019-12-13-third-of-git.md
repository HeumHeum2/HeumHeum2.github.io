---
layout: post
title: "Git 공부 3일차"
lang: ko
categories: git 공부
---

이번 세미나는 `git merge`, `git remote add`, `git push`, `git pull` 명령어와 **협업**이 중심 내용이였다.

### $ git merge
`git merge`는 작업하고 있는 **branch** 들을 합치고 싶을 때 사용하는 명령어다.

먼저 **master**에는 m_work.txt 파일을 **exp**에는 e_work.txt 파일을 만들어 서로 다르게 해주었다.

{% highlight bash %}
# master files
work.txt
m_work.txt

# exp
work.txt
e_work.txt

# log
$ git log --oneline --all --graph
* 63d2d07 (exp) working e2
* 682767a working e1
| * 3dd3a20 (HEAD -> master) working m2
| * 5836424 working m1
|/
* 5bd3f73 working 3
* b023f81 working 2
* 247a290 working 1
{% endhighlight %}

`--oneline` 옵션은 한 줄로 보겠다는 옵션이고, `-all`은 모든 branch 및 tag의 기록을, `--graph`는 그래프로 보여주는 옵션이다.

`git log`를 보면 commit ID **5bd3f73** 이후로 서로 다른 길을 가고 있음을 보여준다. 이 둘을 한번 합쳐보겠다.

{% highlight bash %}
(master) # 현재 HEAD가 위치한 곳은 master이다.

$ git merge exp
Merge made by the 'recursive' strategy.
 e_work.txt | 2 ++ 
 1 file changed, 2 insertions(+)
 create mode 100644 e_work.txt

$ git log --oneline --all --graph
*   81b2063 (HEAD -> master) Merge branch 'exp'
|\
| * 63d2d07 (exp) working e2
| * 682767a working e1
* | 3dd3a20 working m2
* | 5836424 working m1
|/
* 5bd3f73 working 3
* b023f81 working 2
* 247a290 working 1
{% endhighlight %}

`git merge`를 사용하고 `create mode 100644 e_work.txt` 부분을 보면, e_work.txt가 **master**에 새로 생겼음을 알 수 있다. 이로써 다른 파일은 순조롭게 합쳐지는 것을 알 수 있었다.

만약 같은 파일에서 **branch**들을 합치고 싶을 때는 어떻게 적용되는지 해보자.

{% highlight txt %}
(parent)    (master)      (exp)
0               0           0
0               0           0
0               m1          0
0               0           0
0               0           e1
0               0           0
0               m1          0
0               0           e1
0               0           0
0               m1          e1
{% endhighlight %}

우선 work.txt 파일을 만들고, **master**와 **exp**를 파일을 변경해 `git commit`해보았다.  
합치기 전에 HEAD가 누구를 가르키고 있는지에 따라서 `git merge <branch name>`의 branch name을 신경써줘야한다.

**master** 에서 **exp**를 합쳐보자.

{% highlight bash %}
$ git merge exp
Auto-merging work.txt # 자동으로 합쳐준다.
CONFLICT (content): Merge conflict in work.txt
Automatic merge failed; fix conflicts and then commit the result.
{% endhighlight %}

**conflict**이 났다고 알려준다. 왜 그런지 살펴보자.

{% highlight txt %}
(master|MERGING)
0
0
m1
0
0
e1
0
m1
0
e1
0
<<<<<<< HEAD
m1
=======
e1
>>>>>>> exp
{% endhighlight %}

다른 것들은 자동으로 합쳐줬지만 마지막 행은 **parent**와 비교했을 때 둘다 변경이 되었으니 개발자가 변경해달라고 요청하는 것이다.  
**branch**를 보면 **master|MERGING** 로 되어있어, 합성중인 상태라는 것을 알 수 있다.  
만약 합성을 취소하고 싶다면 `git merge --abort`명령어를 사용하면 합성 전으로 돌아갈 수 있다.  
충돌 내용을 변경 후, 합성을 다시 진행하고 싶다면 `git commit`을 하면 새로운 `commit ID`를 만들어 완성본을 보여준다.

{% highlight bash %}
(master|MERGING)
$ git commit -am "working merge"
[master dfdca9c] working merge

(master)
$ git log --oneline --all --graph
*   dfdca9c (HEAD -> master) working merge
|\
| * 4708c05 (exp) working e1
* | ecae6e2 working -m1
|/
* aec874d working 1
{% endhighlight %}

`git log`를 찍어서 보면 제대로 합성되었음을 확인 할 수 있다.

## GitHub
지금까지 내용들은 모두 local에서 이뤄진 것!  
혹여나 노트북이 말썽을 일으켜 포맷을 해야된다면 지금까지 작업했던 것이 다 날아가게 된다.  
그래서 우리는 [GitHub][GitHub] 같은 원격 저장소를 이용해 백업을 해야한다.

![텍스트](/home/heumheum2/login_github.png)

Github를 가입하고 setting을

[GitHub]: https://github.com