## git commit 취소하기 (이미 push 된)

1.  `git status ` : 현재 commit 상태 확인
2.  `git log --oneline` : 커밋 목록 요약본 확인
3.  `git reset —soft HEAD^` : 가장 최신 commit 한개(꺽쇠(^)가 하나)를 취소
    when I run this git command, 
    git reset --soft HEAD^ 
    I get this back  `zsh: no matches found: HEAD^`
    해결방법

```
git reset --soft HEAD\^
```

4. "git status" | 다시 현재 커밋 상태 확인

## Pull Request 커밋 삭제?

git 레파지토리로 사이드프로젝트 진행 중
develop 브랜치에 풀리퀘하던 중 실수가 있었다.

커밋 삭제 삭제 방식 대로 하니까 되길래 그렇게 함
근데 진짜 풀리퀘 삭제하는 방법이 맞는지?
