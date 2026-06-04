# cursorsite

Cursor **서브에이전트·스킬·산출물** 모음 (AI Edu / 팀플 실습용).

## 구조

```
.cursor/
├── agents/          # 서브에이전트 7명 (ad-agency)
│   ├── ad-ae.md
│   ├── ad-copywriter.md
│   ├── ad-image-team.md
│   ├── ad-video-team.md
│   ├── ad-outdoor-team.md
│   ├── ad-creative-team.md
│   └── ad-ceo-review.md
└── skills/
    ├── ad-agency/   # /ad-agency 오케스트레이션
    ├── report-writer/
    └── dot-skill/   # /dot-skill (from titanwings/colleague-skill dot-skill branch)

ad_campaign/         # 광고 캠페인 산출물 (01~08)
reports/             # report-writer 보고서 초안
```

## 사용 방법

1. 이 저장소를 클론한 뒤 **Cursor로 폴더를 엽니다.**
2. 채팅에서 **`/ad-agency`** — 브랜드·목표·타겟 입력 후 7인 팀 캠페인 실행
3. 채팅에서 **`/report-writer`** — 보고서 챕터 초안 작성
4. 채팅에서 **`/dot-skill`** — 동료·관계·셀럽 등 캐릭터 Skill 생성 ([upstream](https://github.com/titanwings/colleague-skill/tree/dot-skill))

## 경로 주의

워크스페이스 폴더 이름이 **`.cursor`** 인 경우, 에이전트는 루트의 `agents/`를 사용해야 할 수 있습니다.  
일반 프로젝트에서는 `.cursor/agents/` 가 표준입니다.

## 포함된 실습 산출물

- **ad_campaign/** — 루키 × 일본 재난 대피 캠페인 바이블
- **reports/** — AI 핫 트렌드 분석 (스킬 / 서브에이전트)
