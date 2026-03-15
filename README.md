# knowmore-data

아만보 앱의 카드 콘텐츠 데이터 레포입니다.
앱 업데이트 없이 이 레포만 수정하면 사용자에게 새 카드가 반영됩니다.

---

## 파일 구조

```
knowmore-data/
├── ai.json              # AI
├── economy.json         # 경제
├── fashion.json         # 패션
├── global.json          # 글로벌
├── health.json          # 의학/건강
├── hot_issues.json      # 이슈 🔥
├── it.json              # IT/개발
├── korean_history.json  # 한국사
├── law.json             # 법률
├── mz.json              # MZ
├── psychology.json      # 심리학
├── real_estate.json     # 부동산
├── science_tech.json    # 과학기술
└── stock.json           # 주식
```

---

## 카드 JSON 형식

각 파일은 카드 객체의 **배열**입니다.

```json
[
  {
    "id": "ai_001",
    "topic": "AI",
    "level": "하",
    "word": "인공지능",
    "summary": "인간의 지능을 모방해 학습·판단·예측할 수 있도록 만든 컴퓨터 시스템",
    "description": "인공지능(AI)은 컴퓨터가 스스로 학습하고 문제를 해결할 수 있도록 만든 기술이에요. 얼굴 인식, 번역, 추천 알고리즘 등 일상 곳곳에 이미 쓰이고 있어요.",
    "example": "예를 들어 유튜브가 내 취향에 맞는 영상을 추천해주는 것도 인공지능 알고리즘 덕분이에요.",
    "related_words": ["머신러닝", "딥러닝", "LLM"],
    "active": true
  }
]
```

### 필드 설명

| 필드 | 필수 | 설명 |
|------|------|------|
| `id` | ✅ | 고유 식별자. `{파일명}_{번호}` 형식 권장 (예: `ai_042`) |
| `topic` | ✅ | 주제 이름. 파일별 고정값 사용 (아래 표 참고) |
| `level` | ✅ | 난이도: `하` / `중` / `상` |
| `word` | ✅ | 카드 제목 (단어/용어) |
| `summary` | ✅ | 한 줄 요약 (40자 이내 권장) |
| `description` | ✅ | 본문 설명 (3~5문장 권장, 구어체 사용) |
| `example` | ✅ | 실생활 예시 문장 |
| `related_words` | ✅ | 관련 단어 배열 (앱 내 다른 카드로 연결됨) |
| `active` | ✅ | `true`면 앱에 노출, `false`면 숨김 |

### 파일별 topic 값

| 파일 | topic 값 |
|------|----------|
| hot_issues.json | `이슈` |
| real_estate.json | `부동산` |
| stock.json | `주식` |
| economy.json | `경제` |
| ai.json | `AI` |
| mz.json | `MZ` |
| fashion.json | `패션` |
| law.json | `법률` |
| health.json | `의학/건강` |
| it.json | `IT/개발` |
| korean_history.json | `한국사` |
| psychology.json | `심리학` |
| science_tech.json | `과학기술` |
| global.json | `글로벌` |
| current_affairs.json | `시사` |

---

## 주간 업데이트 방법

### 방법 1: Claude에게 요청 (권장)

이 README를 Claude에게 첨부하고 아래처럼 요청하세요:

```
[파일명].json에 카드 [N]개 추가해줘.
주제: [주제명]
난이도: [하/중/상]
추가할 단어들: [단어1, 단어2, ...]
```

예시:
```
hot_issues.json에 카드 5개 추가해줘.
주제: 이슈
난이도: 하~중
추가할 단어들: 탄핵, 비상계엄, 헌법재판소, 국회 해산, 내란죄
```

Claude가 JSON 형식에 맞게 카드를 생성해주면, 해당 JSON을 복사해서 파일에 붙여넣고 커밋하면 됩니다.

### 방법 2: GitHub 웹에서 직접 수정

1. [github.com/dogyuHwang/knowmore-data](https://github.com/dogyuHwang/knowmore-data) 접속
2. 수정할 파일 클릭 → 연필(✏️) 아이콘 클릭
3. 배열 맨 뒤에 새 카드 객체 추가
4. "Commit changes" 클릭

### 방법 3: 로컬에서 수정 후 push

```bash
# 파일 수정 후
git add hot_issues.json
git commit -m "이슈: 탄핵 관련 카드 5개 추가"
git push
```

---

## 주의사항

- `id`는 전체 데이터에서 **유일**해야 합니다. 중복 시 앱에서 오동작할 수 있어요.
- `related_words`에 적은 단어가 앱에 카드로 존재해야 연결이 됩니다. 없으면 그냥 텍스트로 표시돼요.
- `active: false`로 설정하면 앱에서 숨겨지므로, 삭제 대신 이 방법을 권장합니다.
- 앱은 **24시간마다** GitHub에서 새 데이터를 fetch합니다. 업데이트 후 최대 하루 뒤 반영됩니다.
