# payroll — 급여관리

이지산업/철기시대/지에스시엔티 급여관리 웹앱. Firebase Firestore로 데이터를 저장하고, Firebase Hosting으로 배포합니다.

## 구조

```
payroll/
├─ public/
│  └─ index.html          # 실제 앱 (Firebase 연결 코드 포함)
├─ firebase.json          # Hosting 설정 (public 폴더를 배포)
├─ .firebaserc            # Firebase 프로젝트 지정 (payroll-dbcb0)
└─ .github/workflows/     # GitHub에 push하면 자동 배포
```

## 코드 수정 → 자동 반영 흐름

1. `public/index.html` 을 수정한다
2. GitHub의 `main` 브랜치에 반영한다 (직접 push 하거나 PR을 만들어 merge)
3. GitHub Actions가 자동으로 Firebase Hosting에 배포한다
4. 몇십 초 뒤 `https://payroll-dbcb0.web.app` 에 반영됨

PR을 올리면 merge 전에 **미리보기 URL**이 댓글로 자동 생성됩니다.

## 최초 1회 설정 (자동배포를 켜기 위해 필요)

GitHub Actions가 Firebase에 배포하려면 인증 키(Secret) 하나를 등록해야 합니다.
가장 쉬운 방법은 로컬 PC에서 아래 명령을 한 번 실행하는 것입니다.

```bash
npm install -g firebase-tools     # 최초 1회만
firebase login                    # 브라우저로 구글 로그인
firebase init hosting:github      # 안내에 따라 이 레포(sangeon23/payroll) 선택
```

`firebase init hosting:github` 을 실행하면 필요한 GitHub Secret
(`FIREBASE_SERVICE_ACCOUNT_PAYROLL_DBCB0`)이 자동으로 등록됩니다.
이미 이 레포에 workflow 파일이 있으므로 "덮어쓸까요?"를 물으면 **No** 를 선택하세요.

## 수동 배포 (선택)

```bash
firebase deploy --only hosting
```
