

# Git Branch 전략

이 문서는 프로젝트에서 사용할 Git 브랜치 전략을 설명합니다. `main` 브랜치를 중심으로 기능 개발과 오류 수정 작업을 체계적으로 관리하기 위한 전략입니다.

## 1. 브랜치 구조

### 1.1. Main 브랜치
- **역할**: 배포 가능한 안정적인 코드를 유지합니다.
- **특징**:
  - 항상 프로덕션 환경에 배포 가능한 상태로 유지됩니다.
  - 모든 변경 사항은 다른 브랜치에서 개발 후 `main` 브랜치로 병합됩니다.
  - 직접적인 커밋은 금지되며, Pull Request(PR)를 통해 코드 리뷰 후 병합됩니다.

### 1.2. Feature 브랜치
- **역할**: 새로운 기능 개발을 위해 사용됩니다.
- **명명 규칙**: `feature/기능이름` (예: `feature/login-system`)
- **특징**:
  - `main` 브랜치에서 분기됩니다.
  - 기능 개발 완료 후 `main` 브랜치로 병합됩니다.
  - 작업 완료 후 브랜치는 삭제 가능합니다.

### 1.3. Bugfix 브랜치
- **역할**: `main` 브랜치에서 발견된 버그를 수정합니다.
- **명명 규칙**: `bugfix/버그설명` (예: `bugfix/fix-login-error`)
- **특징**:
  - `main` 브랜치에서 분기됩니다.
  - 버그 수정 완료 후 `main` 브랜치로 병합됩니다.
  - 작업 완료 후 브랜치는 삭제 가능합니다.

## 2. 워크플로우

1. **기능 개발**:
   - `main` 브랜치에서 `feature/기능이름` 브랜치를 생성합니다.
   - 기능을 개발하고 커밋합니다.
   - 개발 완료 후 `main` 브랜치로 Pull Request를 생성하여 코드 리뷰를 진행합니다.
   - 최소 2명의 팀원에게 승인 받은 후 `main` 브랜치로 병합하고, `feature` 브랜치는 삭제합니다.

2. **버그 수정**:
   - `main` 브랜치에서 `bugfix/버그설명` 브랜치를 생성합니다.
   - 버그를 수정하고 커밋합니다.
   - 수정 완료 후 `main` 브랜치로 Pull Request를 생성하여 코드 리뷰를 진행합니다.
   - 최소 2명의 팀원에게 승인 받은 후 `main` 브랜치로 병합하고, `bugfix` 브랜치는 삭제합니다.

## 3. 브랜치 관리 규칙
- **커밋 메시지**:
  - 명확하고 간결하게 작성합니다.
  - 예: `[Feature] 로그인 기능 추가`, `[Bugfix] 로그인 에러 수정`
- **Pull Request**:
  - PR 생성 시 작업 내용과 변경 사항을 명확히 설명합니다.
  - 최소 2명 이상의 리뷰어의 승인이 필요합니다.
- **충돌 해결**:
  - 병합 시 충돌이 발생하면, 해당 브랜치에서 충돌을 해결한 후 다시 PR을 업데이트합니다.
- **브랜치 삭제**:
  - 병합 완료 후 불필요한 브랜치는 삭제하여 저장소를 깔끔하게 유지합니다.

## 4. Git 명령어 예시

### 4.1. Feature 브랜치 작업
```bash
# main 브랜치에서 시작
git checkout main
git pull origin main

# 새로운 feature 브랜치 생성 및 이동
git checkout -b feature/login-system

# 작업 후 커밋
git add .
git commit -m "[Feature] 로그인 기능 추가"

# 원격 저장소로 푸시
git push origin feature/login-system

# Pull Request 생성 (GitHub/GitLab UI에서 진행)
# 병합 후 브랜치 삭제
git push origin --delete feature/login-system
```

### 4.2. Bugfix 브랜치 작업
```bash
# main 브랜치에서 시작
git checkout main
git pull origin main

# 새로운 bugfix 브랜치 생성 및 이동
git checkout -b bugfix/fix-login-error

# 작업 후 커밋
git add .
git commit -m "[Bugfix] 로그인 에러 수정"

# 원격 저장소로 푸시
git push origin bugfix/fix-login-error

# Pull Request 생성 (GitHub/GitLab UI에서 진행)
# 병합 후 브랜치 삭제
git push origin --delete bugfix/fix-login-error
```
