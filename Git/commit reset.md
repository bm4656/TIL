## git commit 취소하기 (이미 push 된)

1.  `git status ` : 현재 commit 상태 확인한다.
2.  `git log --oneline` : 커밋 목록 요약본 확인한다.
3.  `git reset —soft HEAD^` : 가장 최신 commit 한개(꺽쇠(^)가 하나)를 취소한다.
    _when I run this git command, git reset --soft HEAD^ 
    I get this back  `zsh: no matches found: HEAD^`_
    해결방법 : `git reset --soft HEAD\^`를 사용해준다.

4.  `git status` : 다시 현재 커밋 상태 확인한다.
5.  `git push -f origin 브랜치명` : 강제로 push해준다. -> 잘못 커밋했던 내역이 사라진 것을 확인할 수 있다.

## Pull Request 커밋 삭제?

git 레파지토리로 사이드프로젝트 진행 중
develop 브랜치에 풀리퀘하던 중 실수가 있었다. 잘못 PR을 해버려서 잘못된 PR내역이 남아버린 것이다. 심지어 revert을 해서 두개나 커밋이 남아버려서 곤란한 상황이 되었다.

위에 적은 커밋 삭제 방식대로 해보니 잘 되길래 그렇게 두 개를 삭제 후 새롭게 PR했다. 비록 PR 번호가 삭제한 부분을 포함해서 숫자가 올랐지만 브랜치 작동에 문제가 없어보였다.

구글링을 해도 이 부분에 대해 설명하거나 알려주는 글을 찾지 못해서(PR revert 만 나옴 이건 revert 커밋내역도 남기에...) 이 방법이 맞는지 모르겠다.
PR도 제대로 삭제가 된건지, 진짜 풀리퀘 삭제하는 방법이 맞는지 의문이다. 아마 다른 정석적인 방법이 있을 것 같은데 알게 되면 내용을 추가해야겠다.

## git reset

다음과 같은 커밋 내역이 있다.
**C1 -> C2 -> C3 (HEAD)**
커밋 이전까지 생각 못했던 심각한 실수를 commit 해버린 상태이다.
이런 상황에서 **실수로 커밋한 부분을 되돌리기 위해 사용하는 것이 git reset 이다.**

```
git reset <option> <commit id or commit ref>
```

**C1(조상) -> C2(부모)-> C3(자식)**
만약 자식 commit에서 부모 commitd으로 이동하고 싶다면?
commit id 대신 HEAD~ or HEAD^ or HEAD^1 로 표현 가능하다.
조상 commit으로 가려면 HEAD~2 or HEAD^2로 표현 가능하다.
**즉 쉽게 `HEAD^(돌아갈 횟수)`라고 생각하면 된다.**

### git reset option

git reset 에는 3가지 옵션을 줄 수 있는데

1. --soft
   - 주로 branch 이동하는 용도로 사용할 수 있다.
2. --mixed(default)
   - Staging Area에 들어간 내용을 빼는 용도로 사용할 수 있다.
3. --hard

   - 커밋을 지정한 시점으로 완전히 돌려버릴떄 사용한다. 해당 커밋한 시점으로 돌아갔다고 보면 된다.

   (참고: https://antilog.tistory.com/29)
