---
title: 20190902 note
date: 2019-09-03 17:11:36
tags:
---
# Shell Command, Vim, and Git

### Goal

- Linux의 역사를 이해한다
- CLI에 대한 공포를 극복하고 Shell과 친구가 된다
- Linux Shell 커맨드를 학습하여 능숙하게 이를 활용할 수 있다
- Vim 텍스트 에디터를 통해 파일을 작성하고 매크로를 만들 수 있다
- git을 이해하고, git과 github이 다름을 인지한다
- git을 활용하여 나의 소스코드를 관리할 수 있다
- 나의 커리어를 Swag 할 수 있는 블로그를 git을 활용하여 관리할 수 있다.
- git의 branch model을 활용해 능숙하게 코드관리할 수 있다
- git으로 타인과 협업하며, 다른 프로젝트에 기여할 수 있다

------

### Before Linux

![](http://www.unix.org/u30logo/unix_logo.gif)

- 1965년 데니스 리치, 켄 톰슨 외 x명이 AT&T Bell 연구소에서 PDP-7 기반 어셈블리어로 작성한 UNIX를 개발
- 1973년 데니스 리치와 켄 톰슨이 C를 개발한 뒤, C 기반 UNIX 재작성
- 1984년 리차드 스톨먼이 오픈 소프트웨어 자유성 확보를 위한 GNU (`G`NU is `N`ot `U`nix) 프로젝트 돌입. 하지만 GNU 프로젝트에는 커널이 없었음

------

### Kernel

![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Kernel_Layout.svg/380px-Kernel_Layout.svg.png)

- 하드웨어와 응용프로그램을 이어주는 운영체제의 핵심 시스템소프트웨어
- **OS >= kernel (system software)**

------

### Linus Torvalds

- 헬싱키 대학생이던 리누스 토발즈는 앤디 타넨바움의 MINIX를 개조한 Linux를 발표
- 0.1 - bash (GNU Bourne Again SHell), gcc(UNIX 기반 C 컴파일러)

------

### Linux

![](https://www.extremetech.com/wp-content/uploads/2012/05/Linux-logo-without-version-number-banner-sized.jpg)

- **리누스 토발즈가 작성한 커널 혹은 GNU 프로젝트의 라이브러리와 도구가 포함된 운영체제**
- PC와 모바일, 서버, 임베디드 시스템 등 다양한 분야에서 활용
- Redhat, Debian, Ubuntu, Android 등 다양한 배포판이 존재

------

### Shell

- **운영체제의 커널과 사용자를 이어주는 소프트웨어**
- sh (Bourne Shell): AT&T Bell 연구소의 Steve Bourne이 작성한 유닉스 쉘
- csh: 버클리의 Bill Joy가 작성한 유닉스 쉘(C언어랑 비슷한 모양)
- bash (Bourne Again Shell): Brian Fox가 작성한 유닉스 쉘
  - 다양한 운영체제에서 기본 쉘로 채택
- zsh: Paul Falstad가 작성한 유닉스 쉘
  - sh 확장형 쉘
  - 현재까지 가장 완벽한 쉘

------

### Shell Command Basic

- **[Download git-bash for Windows](https://gitforwindows.org/)**







```
$ [//]: # (Ready to take input)
$ exit = terminate shell
$ clear = clear CLI

Directory
$ ls = list segment (하위 파일/폴더 출력)
$ ls -a = show all including HIDDEN files
$ ls -l = list files by line
    (output)
    -rw-r--r--
    -drw-r--r--
$ cd directory_name = change directory
$ mkdir folder_name = make a new folder (directory) in current directory
$ rm -rf directory_name = remove directory

File
$ touch file_name = make a new file
$ mv file_name directory_name = move file to directory
$ mv file_name new_file_name = rename file
$ cp file_name directory_name = copy file to directory
$ rm file_name = remove file
$ cat file_name = concatnate text (files) and print

```

------

## chmod

> **파일의 권한을 설정할 때 사용**
> `d` or `-`: directory or file
> `r`: read
> `w`: write
> `x`: execute
> `-`: no permission

`drwxr - xr -   x`
(user)(group)(other)

------

## chmod

`$ chmod [옵션] (8진수) (파일명)`
8진수
0: 000
1: 001
2: 010
3: 011
4: 100
5: 101
6: 110
7: 111

------

## Vim

![](https://www.vim.sexy/img/Vimlogo.svg)

------

## Vim

![](http://www.vim.org/images/0xbabaf000l.png)
Copyright (c) 2007 Laurent Gregoire

- Vi improved Text Editor
- **CLI 환경에서 사용하는 editor**

------

## Vim Basic

Command

```
vim file_name - open file with Vim
h, j, k, l - move cursor
i - insert mode
v - visual (normal) mode
ESC - exit mode
d - delete
y - yank
shift + y = copy (cut) line
d d - paste line from shift + y
o - insert new line (below)
O - insert new line (above)
p - paste
u - undo
r - replace
$ - move end of line
^ - move start of line

:w - save
:q - quit
:q! - quit w/o write(no warning)
:wq - write and quit

:{number} - move to {number}th line
```

------

### write `hello.py` with Vim

`$ vim`
`$ vim hello.py`

`i`
`-- insert --`
type `print("hello python!")`
press `esc` to escape

`:wq`

`$ python hello.py`

------

### copy & paste

`$ vim hello.py`

`v`
`-- visual --`
블록지정 후 `y`
`p`

press `esc` to escape
`:wq`

`$ python hello.py`

------

### Use macro with Vim 

`$ vim hello.py`
`qa` - a라는 매크로를 생성

`--recording--`이 보이면 매크로 작성

`q` - 매크로 작성 종료

`@a` - a 매크로 실행
`10@a` - a 매크로 10회 실행

------

![](http://ipengineer.net/wp-content/uploads/2015/04/git-logo.jpg)

------

## VCS (Version Control System)

== SCM (Source Code Management)
< SCM (Software Configuration Management: 형상관리)

------

## chronicle of git

![](https://www.blogcdn.com/www.engadget.com/media/2009/10/linus-torvalds-gives-windows-7-a-big-thumbs-up.jpg)

------

## chronicle of git

- Linux Kernal을 만들기 위해 Subversion을 쓰다 화가 난 리누스 토발즈는 2주만에 git이라는 버전관리 시스템을 만듦
- [git official repo](https://github.com/git/git)

------

## Characteristics of git

- 빠른속도, 단순한 구조
- 분산형 저장소 지원
- 비선형적 개발(수천개의 브랜치) 가능

------

## Pros of git

- 소스코드 주고받기 없이 동시작업이 가능해져 생산성이 증가
- 수정내용은 **commit** 단위로 관리, 배포 뿐 아니라 원하는 시점으로 **Checkout** 가능
- 새로운 기능 추가는 **Branch**로 개발하여 편안한 실험이 가능하며, 성공적으로 개발이 완료되면 **Merge**하여 반영
- 인터넷이 연결되지 않아도 개발할 수 있음

------

## Open-source project

https://github.com/python/cpython
https://github.com/tensorflow/tensorflow

https://github.com/JuliaLang/julia
https://github.com/golang/go

------

## git inside

- Blob: 모든 파일이 Blob이라는 단위로 구성 
- Tree: Blob(tree)들을 모은 것
- Commit: 파일에 대한 정보들을 모은 것

------

## git Process and Command

![](https://i.stack.imgur.com/MgaV9.png)

------

## git is not equal to github

![](http://1.bp.blogspot.com/-WY2YpNr3W6g/UY6tZAc-H3I/AAAAAAAABLY/xJ9x3wIY8V8/s1600/Github2.png)

------

### sign up github

https://github.com/

**important!!**

- 가입할 `email`과 `username`은 멋지게
- private repo를 원한다면 $7/month

------

## Set configuration

terminal

```shell
$ git config --global user.name "username"
$ git config --global user.email "github email address"
$ git config --global core.editor "vim"
$ git config --list
```

------

## My First Repo

Let's make your first repo with github

------

## My First Repo - Method 1

After create new repo through github,

`$ git init`

`$ git remote add origin https://github.com/{username}/{reponame}.git`
(origin can be replaced with other name)

`$ git add .`

`$ git commit -m "some commit"`

`$ git push -u origin master`
(-u as upstream, only required for FIRST push)

------

## Second push to My First Repo

```
$ git add .
$ git commit
$ git push
```

------

## start project with clone - Method 2

- github에서 repo를 생성합니다.
- add description
- check for "initialize this repo with a readme"
- add .gitignore: node
- add a license: MIT License
- move to new repo and hit "clone" on top right (repo address)

```shell
$ git clone {repo address}
$ git add .
$ git commit
$ git push
```

------