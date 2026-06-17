# lectures

김태열의 외부 강의 자료 사전 공유 페이지.

🔗 공개 URL: https://zzazzaroni.github.io/lectures/

## 구조

```
lectures/
├── index.html          ← 랜딩 페이지 (자료 목록)
├── README.md
└── [기관코드]-[연도]-[월]/
    └── index.html      ← 개별 강의 자료
```

## 네이밍 규칙

- `pipc-2026-06` — 개인정보보호위원회 2026년 6월
- `wiset-2026-07` — WISET 2026년 7월
- `kocca-2026-08` — 한국콘텐츠진흥원 2026년 8월
- `daebichi-2026-09` — 다비치안경 2026년 9월

## 새 자료 추가 방법

1. 새 폴더 생성: `mkdir [기관코드]-[연도]-[월]`
2. 폴더 안에 `index.html` 추가
3. 루트 `index.html`의 자료 목록 섹션에 카드 추가:

```html
<a href="./기관코드-연도-월/" class="card">
  <span class="tag preview">사전 공유본</span>
  <h3>기관명 · 강의 제목</h3>
  <p class="desc">강의 한 줄 설명.</p>
  <div class="meta">
    <span>📅 2026년 X월</span>
    <span>⏱ X분</span>
    <span>👥 대상</span>
    <span>🖥 X장</span>
  </div>
  <div class="arrow">→</div>
</a>
```

4. 커밋·푸시:

```bash
git add .
git commit -m "Add [기관코드] lecture"
git push
```

## 사전 공유본 만들 때 고려사항

- 영상 클립은 안내 박스로 교체
- 우클릭·복사·드래그·인쇄 차단
- 워터마크 표시
- 우상단 발표자 모드 버튼 제거

## 라이선스

본 자료의 무단 복제·배포·외부 유출을 금합니다.
© 2026 김태열
