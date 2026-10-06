# 회의실 예약

링크만 있으면 로그인 없이 쓰는 회의실 예약 웹앱입니다.
월/주/일 시간표, 같은 시간 중복 예약 방지, 반복 예약(매주·격주·평일 매일), 예약 수정·취소를 지원합니다.
예약 내용은 Firebase(Firestore)에 저장되어 모두에게 실시간으로 보입니다.

## 파일 설명

| 파일 | 역할 |
| --- | --- |
| `index.html` | 앱 본체. 수정할 필요 없습니다. |
| `firebase-config.js` | Firebase 연결 값을 붙여 넣는 파일. **3단계에서 수정합니다.** |
| `firestore.rules` | Firebase 보안 규칙. **2단계에서 내용을 복사해 붙여 넣습니다.** |

## 설치 순서

### 1단계. Firebase 프로젝트 만들기
1. https://console.firebase.google.com 접속, Google 계정으로 로그인
2. **프로젝트 추가** → 이름 입력(예: meeting-room) → 계속
3. Google 애널리틱스는 **사용 안 함**으로 끄고 프로젝트 만들기

### 2단계. 예약 저장소(Firestore) 만들기
1. 왼쪽 메뉴 **빌드 → Firestore Database → 데이터베이스 만들기**
2. 위치는 **asia-northeast3 (서울)** 선택
3. **프로덕션 모드로 시작** 선택 → 만들기
4. 위쪽 **규칙** 탭을 열고, 기존 내용을 모두 지운 뒤 이 폴더의 `firestore.rules` 내용을 붙여 넣고 **게시**

### 3단계. 연결 값 복사하기
1. 왼쪽 위 톱니바퀴 → **프로젝트 설정** → **일반** 탭
2. 아래 **내 앱**에서 `</>`(웹) 아이콘 클릭 → 앱 닉네임 입력 → **앱 등록**
3. 화면에 나오는 `firebaseConfig` 안의 값 6개(apiKey, authDomain, projectId, storageBucket, messagingSenderId, appId)를 `firebase-config.js`의 같은 항목에 붙여 넣습니다. 따옴표는 지우지 마세요.
4. 이 값은 비밀번호가 아니라 앱 주소 같은 정보라서 공개 저장소에 올려도 됩니다.

### 4단계. GitHub에 올리기
1. GitHub에서 **New repository** → 이름 입력 → **Public** 선택 → 만들기
2. **uploading an existing file** 링크(또는 Add file → Upload files)에서 이 폴더의 파일 3개를 끌어다 놓고 **Commit changes**

### 5단계. 주소 만들기 (GitHub Pages)
1. 저장소 **Settings → Pages**
2. Source는 **Deploy from a branch**, Branch는 **main / (root)** 선택 → Save
3. 1~2분 뒤 `https://내계정.github.io/저장소이름/` 주소가 생깁니다. 이 주소를 팀원에게 공유하면 됩니다.

## 사용 방법
- 처음 예약할 때 예약자 이름을 한 번 입력하면 그 기기에 기억됩니다.
- 시간표의 빈 칸을 누르거나 오른쪽 위 **예약하기**를 누릅니다.
- 월간 화면에서 날짜를 누르면 그날 시간표가 열립니다.

## 알아둘 점
- 로그인이 없어서 링크를 아는 사람은 누구나 예약을 만들고 취소할 수 있습니다. 사내에서만 링크를 공유하세요.
- 운영 시간(09:00–19:00)과 30분 단위는 `index.html` 맨 위 `START`, `END` 값과 `firestore.rules`의 540, 1140(분 단위)을 함께 바꿔야 합니다.
- Firebase 무료 요금제로 소규모 팀이 쓰기에 충분합니다.
