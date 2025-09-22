## 안드로이드 터미널 명령어 

<br>

- 로컬, 원격 브랜치 삭제

```bash
# 1. 로컬 브랜치 삭제
git branch -d branchName

# 2. 원격 브랜치 삭제
git push origin --delete branchName

# 3. 원격 추적 브랜치 정리
git remote prune origin
```