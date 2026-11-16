# SJ모터스 차량 입출고 현황 (Android APK)

GitHub에 올리면 자동으로 APK 파일이 만들어집니다. PC에 개발 도구를 설치할 필요가 없습니다.

## 1단계. Firebase 만들기 (직원 간 데이터 공유용)
1. https://console.firebase.google.com 접속 → 프로젝트 추가 (이름 예: sj-motors)
2. 왼쪽 메뉴 **빌드 → Firestore Database → 데이터베이스 만들기** (위치: asia-northeast3 서울 권장, 시작 모드는 프로덕션 모드)
3. Firestore **규칙** 탭에서 아래 내용으로 바꾸고 게시:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /vehicles/{id} {
      allow read, write: if true;
    }
  }
}
```
4. 프로젝트 설정(톱니바퀴) → 일반 → 내 앱 → **웹 앱(</>) 추가** → 표시되는 `firebaseConfig` 값 6개를 복사
5. `www/index.html` 안의 `firebaseConfig` 부분(파일 아래쪽)에 복사한 값으로 교체

> 보안 안내: 위 규칙은 APK를 가진 사람이면 누구나 읽고 쓸 수 있습니다. APK 파일을 외부에 공유하지 마세요. 로그인(직원 인증)이 필요하면 추가할 수 있습니다.

## 2단계. GitHub에 올리기
1. https://github.com 에서 새 저장소 만들기 (**Private** 권장)
2. 이 폴더의 파일 전체를 업로드 (Add file → Upload files). `.github` 폴더도 반드시 포함
3. 업로드(커밋)하면 자동으로 빌드가 시작됩니다

## 3단계. APK 받기
1. 저장소의 **Actions** 탭 → 가장 최근 "Build APK" 실행 클릭 (초록 체크가 될 때까지 약 5~10분)
2. 맨 아래 **Artifacts → SJ-Motors-apk** 다운로드 (zip 안에 app-debug.apk)
3. 안드로이드 폰으로 옮겨 설치 ("알 수 없는 앱 설치 허용" 필요)

## 수정할 때
`www/index.html`을 고쳐서 다시 업로드하면 새 APK가 만들어집니다.
