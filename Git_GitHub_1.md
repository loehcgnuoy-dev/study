# Git & GitHub 학습 정리

> **핵심 한 줄**: Git은 내 컴퓨터에서 동작하는 **버전 관리 도구**, GitHub는 Git 저장소를 올려두고 **협업·공유**하는 웹 서비스다.

---

## 1. Git / GitHub

### 1-1. Git & GitHub를 사용해야 하는 이유

**버전 관리(Version Control)란?**
파일이나 코드의 변경 이력을 체계적으로 기록·관리하는 것. 언제, 누가, 무엇을 바꿨는지 알 수 있고 필요하면 과거 상태로 되돌릴 수 있다.

**버전 관리가 필요한 이유**

- 변경 이력을 추적할 수 있다
- 실수를 복구할 수 있다 (기능 추가 후 버그가 생기면 이전 정상 버전으로 되돌리기)
- 여러 사람이 충돌 없이 협업할 수 있다 (같은 파일을 동시에 수정해도 누가 무엇을 바꿨는지 확인하고 충돌 해결)
- `최종_진짜최종_v3` 같은 파일을 만들지 않아도 된다

**Git vs. 파일 복사 방식**

| 구분 | 파일 복사 방식 | Git 사용 |
| --- | --- | --- |
| 파일 관리 | `final.py`, `final_v2.py`, `진짜최종.py`처럼 파일이 계속 늘어남 | 하나의 프로젝트에서 커밋 단위로 기록 |
| 변경 이력 | 변경 이유와 내용이 남지 않음 | 변경 내용과 메시지, 책임이 명확함 |
| 되돌리기 | 어려움 | 언제든 특정 시점으로 되돌릴 수 있음 |
| 협업 | 어떤 파일이 최신인지 알기 어려움 | 여러 사람이 동시에 작업 가능 |

### 1-2. Git과 GitHub의 차이

| 구분 | Git | GitHub |
| --- | --- | --- |
| 정체 | 버전 관리를 위한 **도구(프로그램)** | Git 저장소를 올려두는 **웹 서비스** |
| 동작 위치 | 내 컴퓨터(로컬) | 인터넷(원격 서버) |
| 역할 | 버전 관리 엔진 | 코드 공유 및 협업 플랫폼 |
| 제공 기능 | commit, branch, merge 등 | Pull Request, Issue, Review 등 |

→ **Git은 버전 관리 엔진, GitHub는 협업과 공유를 위한 서비스**

### 1-3. Repository (레포지토리)

- 파일과 그 변경 이력을 함께 관리하는 **저장소**
- 프로젝트 전체와 모든 버전 기록이 들어 있다

| 종류 | 설명 | 만드는 방법 |
| --- | --- | --- |
| 로컬 저장소 | 내 컴퓨터에 있는 저장소 | 프로젝트 폴더에서 `git init` → 해당 폴더가 Git 레포지토리가 됨 |
| 원격 저장소 | GitHub 같은 서버에 있는 저장소 | GitHub에서 새 Repository 생성 → `git clone`으로 내 컴퓨터에 복사 |

**원격 저장소의 역할**: 여러 사람이 같은 코드를 공유, 백업, 협업의 기준점

### 1-4. Commit (커밋)

- 변경 사항을 하나의 기록으로 저장하는 단위 (= **하나의 버전**)
- "무엇을 왜 바꿨는지"를 **메시지**로 남긴다
- 특정 시점의 프로젝트 상태를 저장 → **되돌아갈 수 있는 기준점** (게임의 save file과 비슷)

```bash
git commit -m "회원가입 기능 추가"
```

**커밋 메시지 작성 규칙**: 명확하고 간결하게 / 동사로 시작 / 한 커밋 = 한 작업

```text
Add login API
Fix password validation bug
Refactor user service
```

### 1-5. Branch (브랜치)

- 독립적으로 작업할 수 있는 **작업 공간(작업 흐름)**
- 기존 코드를 건드리지 않고 기능 개발·실험·수정을 안전하게 진행
- 여러 기능을 동시에 개발하고, 작업이 끝나면 병합(merge)

```bash
git branch feature/login      # 브랜치 생성
git switch feature/login      # 브랜치 전환
```

### 1-6. 함께 알아둘 개념

**HEAD**: 현재 내가 작업 중인 위치를 가리키는 포인터. 보통 현재 브랜치의 최신 커밋을 가리키며, HEAD가 움직이면 작업 기준이 바뀐 것이다.

**Git의 3가지 영역**

```text
Working Directory  --git add-->  Staging Area  --git commit-->  Repository
```

| 영역 | 설명 |
| --- | --- |
| Working Directory | 실제로 파일을 수정하는 공간 (아직 Git에 기록되지 않은 변경 사항) |
| Staging Area | 다음 커밋에 포함할 변경 사항을 미리 모아두는 공간 |
| Repository | 커밋으로 기록된 버전들이 저장되는 곳 |

---

## 2. git 기본 명령어

### 2-0. 설치 및 GitHub 가입

- macOS: `brew install git` / Windows: Git for Windows 설치
- 설치 확인: `git --version`
- https://github.com 에서 회원가입 (name, email 기록해 두기)

### 2-1. git config

Git의 기본 동작(사용자 정보 등)을 설정하는 명령어

| 구분 | 적용 범위 | 명령어 |
| --- | --- | --- |
| 전역 설정 | 모든 저장소에 적용 | `git config --global user.name "홍길동"` / `git config --global user.email "hong@example.com"` |
| 로컬 설정 | 특정 저장소에만 적용 (회사/개인 프로젝트 구분 시 사용) | `git config user.name "홍길동"` / `git config user.email "hong@example.com"` |

### 2-2. git init

현재 폴더를 Git 레포지토리로 초기화

```bash
git init
```

- `.git` 폴더가 생성된다
- 현재 폴더를 기준으로 버전 관리가 시작된다

### 2-3. git status

현재 레포지토리의 상태를 확인

```bash
git status
```

- 수정된 파일, 스테이징 여부, 커밋 가능한 변경 사항을 확인

### 2-4. git add

변경된 파일을 **Staging Area**로 올리는 명령어

```bash
git add 파일명
git add .          # 변경된 모든 파일
```

- 커밋에 포함할 변경 사항을 선택하는 단계
- **아직 커밋이 생성된 것은 아니다**

### 2-5. git commit

Staging Area에 있는 변경 사항을 하나의 버전으로 기록

```bash
git commit -m "커밋 메시지"
```

### 2-6. git push

로컬 커밋을 **원격 저장소로 올리는** 명령어

```bash
git remote add origin 원격주소    # 원격 저장소 연결
git remote -v                     # 연결 확인
git push -u origin main           # 최초 push (upstream 설정)
```

### 2-7. git pull

원격 저장소의 변경 사항을 **내려받아 로컬에 반영**하는 명령어

```bash
git pull
```

### 2-8. 기본 흐름 한눈에 보기

```bash
git init                          # 1. 저장소 초기화
git add .                         # 2. 변경 사항 스테이징
git commit -m "first commit"      # 3. 커밋
git remote add origin 원격주소     # 4. 원격 저장소 연결
git push -u origin main           # 5. 원격에 업로드
git pull                          # 6. 원격 변경 사항 내려받기
```

### 2-9. .gitignore

버전 관리에서 **제외할 파일**을 지정하는 설정 파일 (환경 변수 파일, 빌드 결과물, 개인 설정 파일 등)

```text
.env
__pycache__/
*.log
```

> **주의**: 이미 커밋된 파일은 Git이 계속 추적하므로 `git rm --cached 파일명`으로 추적을 해제해야 한다.

---

## 3. Branch

### 3-1. git branch 명령어

| 목적 | 명령어 |
| --- | --- |
| 브랜치 목록 확인 | `git branch` |
| 브랜치 생성 | `git branch feature/ui` |
| 브랜치 전환 | `git switch feature/ui` |
| 생성 + 전환 동시에 | `git switch -c feature/ui` |
| 브랜치 병합 | `git merge feature/ui` (현재 브랜치로 합침) |

### 3-2. 브랜치 관리 전략

어떻게 브랜치를 나누고 합칠지에 대한 **팀의 약속**

| 브랜치 | 역할 |
| --- | --- |
| `main` | 배포 가능한 안정 버전 |
| `develop` (dev) | 개발 중인 기능을 모아 테스트하는 버전 |
| `feature/*` | 기능 개발 (예: `feature/login`) |
| `hotfix/*` | 운영 중 발생한 긴급 수정 |
| `release/*` | 배포 준비 및 최종 점검 (강의 자료 외 보충) |

```text
main     ──●─────────────────────●──
            \                   /
develop      ●───●───●───●───●─
                  \     /
feature            ●───●
```

### 3-3. Fast-forward vs. 3-way merge

| 구분 | Fast-forward merge | 3-way merge |
| --- | --- | --- |
| 상황 | 브랜치가 **직선**으로 이어질 때 (분기 없음) | 브랜치가 **갈라졌다가** 다시 합쳐질 때 |
| 동작 | 단순히 커밋 포인터만 이동 | **병합 커밋**이 새로 생성됨 |

→ **분기가 없으면 Fast-forward, 분기가 있으면 3-way merge**

### 3-4. Merge conflict (병합 충돌)

같은 파일의 **같은 부분을 서로 다르게 수정**하면 충돌이 발생한다. Git은 자동 병합을 시도하고, 사람의 판단이 필요한 경우만 충돌로 알려준다.

**해결 방법**

1. 충돌 파일 확인
2. 충돌 코드 직접 수정
3. 새로운 커밋 생성

**실습 흐름**

```bash
# 1) 초기 커밋
git init
echo "hello" > test.txt
git add .
git commit -m "first commit"

# 2) feature 브랜치에서 같은 파일 수정
git branch feature
git switch feature
echo "hello from feature" > test.txt
git add .
git commit -m "update from feature"

# 3) main에서 같은 파일을 다르게 수정
git switch main
echo "hello from main" > test.txt
git commit -am "update from main"

# 4) 병합 시도 → 충돌 발생
git merge feature
cat test.txt                  # 충돌 내용 확인
vi test.txt                   # 충돌 부분 직접 수정
git commit -am "resolve merge conflict"
git log --oneline --graph     # 병합 결과 그래프로 확인
```

충돌 시 파일에는 아래처럼 표시된다. 마커(`<<<<<<<`, `=======`, `>>>>>>>`)를 지우고 최종 내용만 남긴 뒤 커밋한다.

```text
<<<<<<< HEAD
hello from main
=======
hello from feature
>>>>>>> feature
```

---

## 4. 보충: 협업 & 자주 쓰는 명령어

### 4-1. Clone vs. Fork

| 구분 | Clone | Fork |
| --- | --- | --- |
| 의미 | 원격 저장소를 그대로 내 로컬로 복사 | 다른 사람의 저장소를 **내 GitHub 계정으로 복사** |
| 사용 시점 | 같은 저장소에 push 권한이 있을 때 | 원본에 직접 push 권한이 없을 때 |
| 주 용도 | 팀 내부 협업 | 오픈소스 기여 |

### 4-2. Pull Request / Code Review / Issue

- **Pull Request(PR)**: 변경 사항을 원본 저장소에 반영해 달라고 요청하는 것 (변경 설명, 리뷰 요청, 병합 전 검증)
- **Code Review**: 병합 전에 함께 확인하는 과정 (버그 예방, 품질 유지, 팀 규칙 공유). 코드 중심 리뷰, 이유를 남긴 코멘트, 승인 후 병합
- **Issue**: 할 일, 버그 리포트, 기능 요청 관리. PR과 Issue를 연결해 작업 관리 (예: `Resolve: #1234`)

### 4-3. 협업 실습 흐름

**Fork & Clone 방식**

1. Issue 생성
2. 내 GitHub 계정으로 Fork
3. `git clone 내_포크_저장소_URL`
4. `git remote add upstream 원본_저장소_URL`
5. `git pull upstream main`
6. `git switch -c feature/add-my-name` → 작업 → 커밋 → push → PR

**Collaborator 방식**

1. Repository collaborator 등록
2. Branch protection rules 추가 (Require a pull request before merging)
3. `git clone 원본_저장소_URL`
4. `git switch -c feature/mybranch` + 커밋
5. `git push origin feature/mybranch`
6. GitHub에서 `feature/mybranch → main` PR 생성

### 4-4. 자주 사용하는 명령어

| 명령어 | 용도 |
| --- | --- |
| `git show [HEAD / 커밋해시]` | 특정 커밋의 변경 내용(diff), 메시지, 작성자, 날짜 확인 |
| `git diff` | Working Directory ↔ Staging Area 비교 |
| `git diff --staged` | Staging Area ↔ HEAD 비교 |
| `git diff HEAD~1 HEAD` | 커밋 ↔ 커밋 비교 |
| `git blame 파일명` | 파일의 각 줄을 누가, 언제, 어떤 커밋에서 수정했는지 추적 |
| `git stash` | 작업 중인 변경 사항을 임시 저장 (커밋 없이 브랜치 이동 시 유용) |
| `git stash list` | 저장된 stash 목록 확인 |
| `git stash pop` | 가장 최근 stash를 적용하고 목록에서 제거 |
| `git stash apply` | stash를 제거하지 않고 적용만 |
| `git reset --soft HEAD~1` | 커밋만 취소 (변경 내용 유지) |
| `git reset --mixed HEAD~1` | 커밋 + 스테이징 취소 (기본값) |
| `git reset --hard HEAD~1` | 커밋 + 스테이징 + 파일까지 모두 삭제 ⚠️ |
| `git revert 커밋해시` | 특정 커밋을 되돌리는 **새 커밋** 생성 (히스토리 보존) |
| `git commit --amend` | 마지막 커밋 수정 (메시지 변경, 파일 추가/제거) |
| `git commit --amend --no-edit` | 메시지는 그대로 두고 마지막 커밋에 변경만 반영 |

> **reset vs. revert**: `reset`은 히스토리를 **바꾸고**, `revert`는 히스토리를 **보존**한다. 협업 중인 브랜치에서는 `revert`가 더 안전하다.

---
