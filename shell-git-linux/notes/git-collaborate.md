# Git Collaborate

## 1. invite collaborators

팀원 모두가 하나의 repo에서 작업하는 방법.

**팀장**

1. repo 생성
2. 팀원 초대
   1. Settings
   2. Manage access
   3. Invite a collaborator

**팀장, 팀원**

add, commit, push 끝

**주의**

* 다른 사람의 코드를 지우고 push할 경우, 해당 코드는 사라집니다.
* 물론 이전 commit을 통해 복구가 가능하나 비효율적입니다.
* merge conflict가 자주 발생합니다.

---

## 2. Fork & Pull request

팀장의 repo를 팀원이 fork하여 작업한 후 pull request를 생성하는 방법.

**팀장**

1. repo 생성
2. pull request 검토 후 merge

**팀원**

1. 팀장의 repo를 fork
2. fork한 repo를 로컬에 clone
3. 팀장의 repo 주소와 본인의 repo 주소를 분리 (pull, 최신화 용도)
   1. 

팀장의 repo를 팀원이 fork(복사, clone과는 다른 개념)하여 또 다른 repo를 생성. 팀원은 각자 fork한 repo에 add, commit, push하여 팀장의 repo에 pull request를 생성한다. 