# lectures

김태열의 외부 강의 자료 사전 공유 페이지.

🔗 <https://zzazzaroni.github.io/lectures/>

## 구조

```
lectures/
├── index.html              ← 랜딩 (자료 목록, 공개)
├── pipc-2026-06/index.html ← 🔒 암호화된 강의자료
├── msit-2026-07/index.html ← 🔒 암호화된 강의자료
├── tools/                  ← 암호화 도구
│   ├── 비밀번호_설정.html    ← 브라우저로 열어서 비밀번호 변경
│   ├── encrypt.js          ← CLI 방식 (node)
│   └── lock_template.html  ← 잠금화면 템플릿
├── _평문원본/               ← 평문 (gitignore — 커밋 금지)
└── 배포하기.sh
```

## 보호 방식

강의자료 HTML은 **AES-256-GCM**으로 암호화되어 저장됩니다. 잠금 화면에서 올바른
비밀번호를 넣어야 브라우저가 본문을 복호화해 표시합니다. 저장소를 뒤지거나
개발자도구로 소스를 열어도 Base64 암호문만 보입니다.

- 키 유도: PBKDF2-HMAC-SHA256, 310,000회, 16바이트 랜덤 솔트
- 암호화: AES-256-GCM, 12바이트 랜덤 IV, 인증 태그 포함(변조 시 복호화 거부)
- 비밀번호는 파일 어디에도 저장되지 않습니다. 해시조차 없습니다.
- 자료마다 **다른 비밀번호**를 씁니다.

한계: 비밀번호를 받은 사람이 복호화된 화면을 저장·재배포하는 것까지는 막지 못합니다.
열람 제한이지 DRM이 아닙니다.

## 비밀번호 변경

**방법 A — 브라우저 (터미널 불필요)**

1. `tools/비밀번호_설정.html` 을 브라우저로 엽니다.
2. `_평문원본/<강의폴더>/index.html` 을 선택하고 새 비밀번호를 입력합니다.
3. 내려받은 `index.html` 로 `<강의폴더>/index.html` 을 덮어씁니다.
4. `git add . && git commit -m "비밀번호 변경" && git push`

**방법 B — 터미널**

```bash
node tools/encrypt.js \
  _평문원본/msit-2026-07/index.html \
  msit-2026-07/index.html \
  '새비밀번호' \
  '개인정보보호 실무 교육' \
  '과학기술정보통신부 · 개인정보취급자 교육'
```

> 비밀번호를 잊으면 복구할 수 없습니다. `_평문원본/` 으로 다시 만들어야 합니다.

## 새 자료 추가

```bash
mkdir -p _평문원본/기관코드-연도-월
cp /경로/강의자료.html _평문원본/기관코드-연도-월/index.html
node tools/encrypt.js _평문원본/기관코드-연도-월/index.html \
                      기관코드-연도-월/index.html '비밀번호' '제목' '하단문구'
# 루트 index.html 자료 목록에 a.card 추가
git add . && git commit -m "Add 기관코드 lecture" && git push
```

기관코드 예: `pipc`(개인정보보호위원회) · `msit`(과기정통부) · `wiset` · `kocca` · `daebichi`

## 라이선스

본 자료의 무단 복제·배포·외부 유출을 금합니다. © 2026 김태열
