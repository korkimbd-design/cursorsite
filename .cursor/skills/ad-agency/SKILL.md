---
name: ad-agency
description: AI 광고 대행사 7인 팀을 순서·병렬로 오케스트레이션한다. 브랜드 캠페인 기획, /ad-agency, adagency, 광고 대행사 실행 요청 시 사용한다.
---

# Ad Agency (진행 대본)

7명의 서브에이전트(AE → 카피 → 제작 4팀 병렬 → 대표 검수 → 바이블 통합)를 **정해진 순서**로 실행합니다.

## 사전 조건

- 서브에이전트: **`agents/ad-*.md`** (7명, 프로젝트 루트의 `agents/` 폴더)
- 산출물 폴더: `ad_campaign/` (없으면 생성)

> **경로 주의:** 이 워크스페이스 폴더 이름이 `.cursor`이므로 `.cursor/agents/`를 쓰면 ` ad-image-team.md`처럼 **공백이 끼는 잘못된 경로**로 저장될 수 있습니다. 반드시 `agents/ad-image-team.md` 형식을 사용하세요.

## 1단계: 브리프 수집

사용자에게 아래를 확인합니다. 이미 채팅에 있으면 생략합니다.

1. 브랜드 또는 제품 이름
2. 캠페인 목표 (인지도 / 구매 유도 / 리브랜딩 등)
3. 타겟 (나이, 성별, 관심사 등)
4. **전체 자동 실행** vs **단계마다 확인**

## 2단계: AE (순차 · `is_background: false`)

**서브에이전트 `ad-ae`** 호출.

- 입력: 1단계 브리프
- 출력: `ad_campaign/01_ae_brief.md`
- AE 완료 전까지 다음 단계로 넘어가지 않음

## 3단계: 카피라이터 (순차)

**서브에이전트 `ad-copywriter`** 호출.

- 입력: `01_ae_brief.md` 전체
- 출력: `ad_campaign/02_copy.md`

## 4단계: 제작팀 4개 (병렬 · 핵심)

**한 메시지에서 4개 서브에이전트를 동시에** 호출합니다.

| 서브에이전트 | 출력 파일 |
|-------------|-----------|
| `ad-image-team` | `ad_campaign/03_image_ad.md` |
| `ad-video-team` | `ad_campaign/04_video_ad.md` |
| `ad-outdoor-team` | `ad_campaign/05_outdoor_ad.md` |
| `ad-creative-team` | `ad_campaign/06_creative_ad.md` |

- 공통 입력: `01_ae_brief.md` + `02_copy.md`
- 각 팀 프로필에 **`is_background: true`** 가 설정되어 있어야 병렬 실행됨
- 스킬에서도 반드시 **같은 단계에서 4팀을 한꺼번에** 호출할 것 (한 팀씩 순차 호출 금지)

4팀 모두 완료될 때까지 대기한 뒤 5단계로 진행.

## 5단계: 대표 검수 (순차 · readonly)

**서브에이전트 `ad-ceo-review`** 호출.

- 입력: `01` ~ `06` 전체
- 출력: `ad_campaign/07_review.md`
- 대표는 **채점만** (산출물 수정 금지, `readonly: true`)

## 6단계: 캠페인 바이블

`07_review.md`에서 **총점 50점 이상(만점 70)** 이면:

- `01`~`07`을 통합해 `ad_campaign/08_campaign_bible.md` 생성

**50점 미만**이면:

- 검수서에 명시된 팀만 재실행 (해당 파일만 덮어쓰기)
- 수정 후 **5단계부터 반복** (최대 2회, 이후 사용자에게 보고)

## 실행 체크리스트

```
- [ ] ad_campaign/01_ae_brief.md
- [ ] ad_campaign/02_copy.md
- [ ] ad_campaign/03~06 (4개 병렬)
- [ ] ad_campaign/07_review.md
- [ ] ad_campaign/08_campaign_bible.md (통과 시)
```

## 주의 (교육 자료 기준)

- AI 크리에이티브는 **초안**입니다. 클리셰·과장을 사람이 검토하세요.
- 제출용 최종 산출물은 **`08_campaign_bible.md`** (또는 01~07 세트)를 md로 제출합니다.
