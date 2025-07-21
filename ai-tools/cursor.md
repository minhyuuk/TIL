## 커서
### Cursor

> VS code 기반 코드 편집기(IDE). 대규모 언어 모델(LLM) 이 붙어있어 빠른 생산성 향상에 도움이 된다. ``cursor/rules`` 경로에 프로젝트 규칙을 추가하여 AI에게 상세한 명령을 내릴 수 있다. 

<br>

### 예시

```yaml
---
description: android app development rules using kotlin language
globs: 
  - "**/*.build.gradle.kts"
  - "api/**/*"
alwaysApply: false
---

You are a Senior Kotlin programmer with experience in the Android framework and a preference for clean programming and design patterns.

Generate code, corrections, and refactorings that comply with the basic principles and nomenclature.
```

<br>

### 각 필드 상세 설명
```yaml
description: android app development rules using kotlin language
```
- 역할: 규칙의 목적과 용도를 설명. 문서화 목적으로 사용.
- rules 적용: **영향 없음** (AI가 참고용으로만 사용).
- 활용: 팀원들이 규칙 파일을 이해하거나 관리할 때 도움.

<br>

```yaml
globs: 
  - "**/*.build.gradle.kts" # 모든 폴더의 .build.gradle.kts
  - "api/**/*"              # api 하위 모든 파일
  ```
- 역할: 규칙이 적용된 파일 경로 지정.
- rules 적용: **영향 있음** - 지정된 패턴과 일치하는 파일에서만 규칙 ``활성화``.
- 활용: 사용 원하는 rules 를 경로에 맞게 설정할 수 있음.
  - ``*``는 "한 단계", ``**``는 "모든 단계"를 의미.

<br>

```yaml
alwaysApply: false
```
- 역할: 규칙의 전역 적용 여부 제어
- rules 적용: 직접적 영향 있음 
  - ``true``: 항상 적용 (컨텍스트와 무관하게 강제 적용)
  - ``false``: 선택적 적용 (AI가 상황에 따라 적절히 판단)