# 아빠로그 외부 약관 페이지 배포 가이드

이 폴더의 파일들은 **GitHub Pages**로 공개되어 Play Store 등록·앱 내 약관 외부 링크용으로 사용됩니다.

## 파일 구성

| 파일 | 역할 |
|---|---|
| `index.html` | 약관/정책 포털 (입구) |
| `terms.html` | 이용약관 |
| `privacy.html` | 개인정보처리방침 |
| `style.css` | 공통 스타일 (Pretendard 폰트 + 앱 톤) |

앱 내 `lib/features/legal/legal_screen.dart`의 본문과 **100% 동일한 내용**으로 유지해야 합니다. 한쪽만 갱신되면 사용자 신뢰도가 떨어집니다.

---

## 배포 방법 — 신규 레포 `Appalog-Team.github.io`

### 1단계: 신규 레포 생성 (5분)

1. https://github.com/organizations/Appalog-Team/repositories/new 접속
2. **Repository name**: `Appalog-Team.github.io` (정확히 이 이름이어야 organization site로 자동 인식됨)
3. **Public** 선택
4. README 자동 생성 체크
5. Create repository

### 2단계: 이 폴더 파일 4개 push

로컬에서:

```powershell
# 새 레포 clone
cd C:\projects
git clone https://github.com/Appalog-Team/Appalog-Team.github.io.git
cd Appalog-Team.github.io

# Appalog 레포의 web-pages 폴더 내용을 이쪽 레포 루트로 복사
copy C:\projects\appalog\web-pages\*.* .

# Push
git add .
git commit -m "feat: 아빠로그 약관 및 개인정보처리방침 페이지"
git push
```

### 3단계: GitHub Pages 자동 활성화

`Appalog-Team.github.io` 이름의 레포는 push만 하면 **자동으로 GitHub Pages가 활성화**됩니다. 별도 설정 불필요.

1~2분 후 다음 URL에서 접속 가능:

| 페이지 | URL |
|---|---|
| 포털 | https://appalog-team.github.io |
| 이용약관 | https://appalog-team.github.io/terms.html |
| 개인정보처리방침 | https://appalog-team.github.io/privacy.html |

### 4단계: 모바일 미리보기 + 검증

- 모바일에서 위 URL 접속해서 가독성 확인
- Pretendard 폰트 로드 OK인지
- 이메일 링크 `mailto:` 동작 OK인지
- 내부 링크(index ↔ terms ↔ privacy) OK인지

---

## Play Store 등록 시 사용할 URL

Play Console → 앱 설정 → 개인정보처리방침에 입력:

```
https://appalog-team.github.io/privacy.html
```

`https://appalog-team.github.io` 도 OK (포털에서 클릭 가능). Play Store는 보통 `privacy.html` 직접 링크를 권장.

---

## 앱 내 링크 추가 (선택 — 다음 작업)

`my_screen.dart`의 "약관 및 정책" 메뉴 옆에 작은 외부 링크 아이콘 추가 가능:

> 앱 내 약관 화면에서 "웹에서 보기" 버튼 → 외부 URL 새 창

베타 1.2 후속 작업으로 진행 가능 (필수 아님).

---

## 약관 본문 갱신 절차

약관 내용이 바뀔 때:

1. `lib/features/legal/legal_screen.dart` 본문 수정 (앱 내용)
2. 이 폴더의 `terms.html` / `privacy.html` 본문도 동일하게 수정 (외부 페이지)
3. Appalog 레포에 commit
4. `Appalog-Team.github.io` 레포에도 같은 변경 commit + push

자동 동기화 스크립트는 베타 단계엔 불필요. 정식 출시 후 GitHub Actions로 자동화 가능.

---

## 다음 단계

이 폴더는 `web-pages/`라는 임시 이름으로 Appalog 레포에 보관되어 있습니다. 실제 배포는 별도 레포 `Appalog-Team.github.io`로 분리되니, Appalog 레포의 `web-pages/` 폴더는 **원본 보관용**으로 유지하시면 됩니다. 다음에 약관 변경 시 양쪽 다 갱신.
