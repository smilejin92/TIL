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

pull, add, commit pull, push 끝

**Merge Conflict**

코드를 합치는 과정에서 같은 파일의 코드가 다를 경우 생기는 현상

**주의**

* 다른 사람의 코드를 지우고 push할 경우, 해당 코드는 사라집니다.
* 물론 이전 commit을 통해 복구가 가능하나 비효율적입니다.

---

## 2. Fork & Create pull request

팀장의 repo를 팀원이 fork하여 작업한 후 pull request를 생성하는 방법.

**팀장**

1. repo 생성
2. pull, add, commit, pull, push
3. pull request 검토 후 merge

**팀원**

1. 팀장의 repo를 fork
2. fork한 repo를 로컬에 clone
3. 팀장의 repo 주소와 본인의 repo 주소를 분리 (pull, 최신화 용도)
   1. git remote add (forked-repo alias) 포크된레포url
   2. git remote get-url (forked-repo alias)
   3. git remote set-url origin 팀장레포url (origin 통일)
   4. git remote get-url origin
4. pull(팀장 repo), add, commit, pull(팀장 repo), push(개인 repo)
5. create pull request(팀원)

