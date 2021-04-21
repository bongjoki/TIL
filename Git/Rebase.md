# Git rebase하는 방법

### merge와 rebase 비교

-   `git-merge` : Join two or more development histories together.
-   `git-rebase`: Forward-port local commits to the updated upstream head.

`merge`는 커밋 이력을 그대로 두고 개발 히스토리를 합치는 것이고,
`rebase`는 커밋 이력을 한개의 이력으로 바꾸는 것이다. (극히 주관적)

> git의 merge와 rebase 비교하기 : https://blog.outsider.ne.kr/666

![git merge와 rebase 차이](https://images.velog.io/images/bongjoki/post/555e67a2-7b82-4f35-b927-ccba5dfb5cad/1_eZrqyYU4d-M92fvN95L5jw.png)

### git rebase하는 방법

1. 장바구니 페이지 구현을 해야한다고 가정하고, 다음과 같이 작업을 세분화 하겠다.

    - UI 컴포넌트 구현
    - 장바구니 관련 기능 구현
    - 코드 리팩토링

2. master에서 dev branch를 만들고, 'UI 컴포넌트 구현' 작업을 했다고 가정하고, 다음과 같이 커밋을 남긴다.

```shell
master > git checkout -b dev
dev > git add .
dev > git commit -m 'UI 컴포넌트 구현'
```

3. '장바구니 관련 기능 구현' 작업을 하고, 다음과 같이 커밋을 남긴다.

```shell
dev > git add .
dev > git commit -m '장바구니 관련 기능 구현'
```

4. '코드 리팩토링' 작업을 하고, 다음과 같이 커밋을 남긴다.

```shell
dev > git add .
dev > git commit -m '코드 리팩토링'
```

5. origin에 push 하기 전에 rebase로 불필요한 commit을 squash해준다.

```shell
dev > git rebase -i @~3
(참고: -i는 --interactive 옵션이고, @~3은 HEAD 기준으로 최근 3개의 commit을 rebase하겠다는 뜻이다.)
```

6. 다음과 같은 vi 창이 뜬다. 사용할 vi 명령어는 다음과 같다.
    > i : 입력 모드 진입
    > esc : 명령모드로 돌아가기
    > dd : 해당 라인 지우기
    > :wq : 저장하고 vi 종료하기
    > vi 명령어 정리 : https://blockdmask.tistory.com/25

첫번째 줄을 제외하고, pick -> s 로 바꿔준 후, 저장후 vi를 종료한다.

```shell
pick 1365eff UI 컴포넌트 구현
s f252a5a 장바구니 기능 구현
s c28ada8 코드 리팩토링

# Rebase 50409e0..c28ada8 onto 50409e0 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
"~/Documents/test/rebase_test/.git/rebase-merge/git-rebase-todo" 29L, 1245C
```

7. 바꾸고 싶은 커밋 명으로 바꾼다.

```shell
장바구니 페이지 구현

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Wed Apr 14 11:11:51 2021 +0900
#
# interactive rebase in progress; onto 50409e0
# Last commands done (3 commands done):
#    squash f252a5a 장바구니 기능 구현
#    squash c28ada8 코드 리팩토링
# No commands remaining.
# You are currently rebasing branch 'main' on '50409e0'.
#
# Changes to be committed:
#       modified:   README.md
#

```

8.  dev로 push 해준다.

```
git push origin dev  // 로컬에만 commit한 경우
git push origin +dev // 이미 원격저장소에 push를 한 경우
```

### 참조

> [git rebase 하는 방법](https://flyingsquirrel.medium.com/git-rebase-%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-ce6816fa859d)
