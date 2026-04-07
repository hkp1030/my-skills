---
name: django-orm-query-tuning
description: Django ORM QuerySet 성능 최적화, django shell 재현, PostgreSQL EXPLAIN/EXPLAIN ANALYZE 비교, 인덱스 추가 여부 판단, 결과 동일성 검증이 필요한 작업에 사용.
---

# Django ORM Query Tuning

Django ORM queryset의 성능을 개선하되 결과 동일성을 유지해야 하는 작업에 사용한다. `django shell`과 `QuerySet.explain()`을 기본 도구로 삼고, 구체적인 최적화 방식은 실제 plan을 보고 결정한다.

## 기본 워크플로

1. 대표 queryset을 django shell에서 그대로 재현한다.
   - 프로젝트 루트의 `tmp/` 폴더에 스크립트 파일(`.py`)을 작성한 뒤 `uv run python manage.py shell < tmp/스크립트.py`로 실행한다.
   - base와 실제 병목이 발생하는 경로를 기준으로 측정한다.
2. `explain(analyze=True, buffers=True)`로 baseline을 남긴다.
3. 후보 변경안을 적용하고, 같은 조건에서 다시 측정한다.
4. 인덱스 변경이 필요한 경우, 아래 원칙을 따른다.
   - 스키마 변경은 인덱스에 한정한다.
   - 마이그레이션 수를 최소화하고, 인덱스 설계가 바뀌면 기존 migration을 되돌린 뒤 다시 생성한다.
5. 독립 기준으로 결과를 검증한다.
6. 최종 보고에는 baseline 대비 배수와 검증 범위를 함께 남긴다.

## 작업 원칙

- 로직 변경과 단순 성능 최적화를 구분한다.
- 기존 코드를 크게 훼손하지 말고 병목 지점만 좁게 수정한다.
- 인덱스 추가·삭제, 데이터 수정 등 DB에 쓰기가 발생하는 작업은 반드시 트랜잭션 안에서 수행하고, 검증이 끝나면 롤백하여 실제 DB에 반영되지 않도록 한다.

## 체크포인트

- 기준 queryset 실행 시간
- 결과 동일성 비교 건수와 mismatch 수
