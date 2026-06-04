# My Skills

Codex와 Claude Code에서 사용하는 개인 스킬을 관리하는 저장소입니다.

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
- 명시적으로 `$readable-code-style`(Codex) 또는 `/readable-code-style`(Claude Code)로 호출

### `write-polished-docs`

문서 초안과 검토 내용을 최종 독자가 읽을 수 있는 문장으로 정리하는 스킬입니다.

- 대화와 검토 흔적 제거
- 사실, 결정, 근거 중심의 문서 재구성
- 중복 설명 정리
- 요구사항, 설계 문서, 회의 메모 등 문서 유형별 구조화

## 디렉터리 구조

```text
.
├── README.md
└── skills
    ├── django-orm-query-tuning
    │   ├── SKILL.md
    │   └── agents
    │       └── openai.yaml
    ├── readable-code-style
    │   ├── SKILL.md
    │   └── agents
    │       └── openai.yaml
    └── write-polished-docs
        ├── SKILL.md
        └── agents
            └── openai.yaml
```

## 사용 방법

필요한 스킬 디렉터리를 각 도구의 스킬 디렉터리로 복사해서 사용합니다.

### Codex

```bash
mkdir -p ~/.codex/skills
cp -R skills/django-orm-query-tuning ~/.codex/skills/
cp -R skills/readable-code-style ~/.codex/skills/
cp -R skills/write-polished-docs ~/.codex/skills/
```

### Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R skills/django-orm-query-tuning ~/.claude/skills/
cp -R skills/readable-code-style ~/.claude/skills/
cp -R skills/write-polished-docs ~/.claude/skills/
```

Claude Code는 `SKILL.md`의 frontmatter(`name`, `description`)만으로 스킬을 인식하며, 함께 복사되는 `agents/openai.yaml`은 사용하지 않고 무시합니다.

## 관리 원칙

- 스킬은 `skills/` 아래에서 디렉터리 단위로 관리합니다.
- 스킬 설명 변경은 `SKILL.md`에서 관리합니다. `SKILL.md`는 Codex와 Claude Code가 공통으로 사용합니다.
- 에이전트 설정 변경은 `agents/` 아래에서 관리합니다. `agents/openai.yaml`은 Codex 전용 인터페이스 파일입니다.
