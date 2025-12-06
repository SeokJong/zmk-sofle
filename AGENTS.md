# 에이전트 지침

## Git 작업 규칙

### 푸시 전 필수 사항
푸시하기 전에 항상 최신 변경사항을 먼저 가져와야 합니다:

```bash
git pull --rebase origin <branch> && git push
```

또는:

```bash
git fetch origin
git rebase origin/<branch>
git push
```

### 이유
- GitHub Actions (keymap-drawer 등)가 자동으로 커밋을 생성할 수 있음
- 원격 저장소와 로컬 저장소의 충돌 방지
- 강제 푸시(force push) 사용 최소화
