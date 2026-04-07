# My Skills

Codex에서 사용하는 개인 스킬을 관리하는 저장소입니다.

## 포함된 스킬

### `django-orm-query-tuning`

Django ORM `QuerySet`의 성능을 개선하되 결과 동일성을 유지해야 하는 작업에 사용하는 스킬입니다.

- `django shell`에서 대표 쿼리를 재현
- `QuerySet.explain()`으로 실행 계획 비교
- 인덱스 변경 필요 여부 판단
- 결과 동일성 검증 범위 기록

### `readable-code-style`

코드 가독성을 높이기 위한 단순화와 정리에 사용하는 스킬입니다.

- 복잡한 분기와 중첩 축소
- 과도한 구조화와 불필요한 방어 코드 제거
- 직접적이고 읽기 쉬운 흐름 우선
- 명시적으로 `$readable-code-style`로 호출 가능

## 디렉터리 구조

```text
.
├── README.md
└── skills
    ├── django-orm-query-tuning
    │   ├── SKILL.md
    │   └── agents
    │       └── openai.yaml
    └── readable-code-style
        ├── SKILL.md
        └── agents
            └── openai.yaml
```

## 사용 방법

필요한 스킬 디렉터리를 Codex 스킬 디렉터리로 복사해서 사용합니다.

```bash
mkdir -p ~/.codex/skills
cp -R skills/django-orm-query-tuning ~/.codex/skills/
cp -R skills/readable-code-style ~/.codex/skills/
```

## 관리 원칙

- 스킬은 `skills/` 아래에서 디렉터리 단위로 관리합니다.
- 스킬 설명 변경은 `SKILL.md`에서 관리합니다.
- 에이전트 설정 변경은 `agents/` 아래에서 관리합니다.
