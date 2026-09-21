# HarDoc

![HarDoc 코믹 배너](assets/hardoc-hero.png)

> **HarDoc! Your harness is dumb right now. Fix it now!**

## 원하는 언어로 읽기

아래 링크를 누르면 해당 언어로 작성된 README 페이지가 열립니다. 명령어와 스킬 이름은 복사해 실행할 수 있도록 원문 그대로 유지했습니다.

|  |  |  |
| --- | --- | --- |
| [العربية](README.ar.md) | [বাংলা](README.bn.md) | [简体中文](README.zh-CN.md) |
| [繁體中文](README.zh-TW.md) | [Nederlands](README.nl.md) | [Français](README.fr.md) |
| [Deutsch](README.de.md) | [Ελληνικά](README.el.md) | [हिन्दी](README.hi.md) |
| [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [日本語](README.ja.md) |
| [한국어](README.ko.md) | [Bahasa Melayu](README.ms.md) | [فارسی](README.fa.md) |
| [Polski](README.pl.md) | [Português](README.pt.md) | [Română](README.ro.md) |
| [Русский](README.ru.md) | [Español](README.es.md) | [Svenska](README.sv.md) |
| [ไทย](README.th.md) | [Türkçe](README.tr.md) | [Українська](README.uk.md) |
| [Tiếng Việt](README.vi.md) | [Kiswahili](README.sw.md) | [اردو](README.ur.md) |

목록에 없는 언어는 [Google Translate 웹사이트 번역](https://translate.google.com/)에서 `https://github.com/qjc-office/hardoc`를 붙여 넣어 읽을 수 있습니다. 검토된 번역을 추가하려면 `README.md`를 `README.<locale>.md`로 복사해 문장만 번역하고, 모든 코드 블록을 보존한 뒤 이 목록에 링크를 추가하세요.

HarDoc은 **Claude Code와 Codex**의 하네스를 읽기 전용으로 점검하는 플러그인입니다. AI가 엉뚱한 스킬을 고르거나, 같은 도구를 두 번 보거나, 매 요청마다 필요 없는 도구를 불러오는 원인을 찾아 근거와 최소 수정안을 보여줍니다.

## 30초 만에 이해하기

AI 코딩 환경을 공구 상자라고 생각하면 쉽습니다.

- **스킬(skill)**: 특정 업무를 하는 방법을 알려주는 작업 설명서입니다.
- **MCP 서버**: 외부 도구나 데이터에 연결하는 다리입니다.
- **플러그인(plugin)**: 스킬과 여러 구성요소를 묶은 패키지입니다.
- **훅(hook)**: 정해진 시점에 자동으로 실행되는 동작입니다.
- **규칙(rule)·에이전트(agent)**: 항상 적용되는 지침이나 전문 역할입니다.

구성요소가 많다고 AI가 자동으로 똑똑해지지는 않습니다. 비슷한 설명이 경쟁하거나 지시가 서로 충돌하면 스킬을 잘못 고르고, 매번 노출되는 도구가 요청에 불필요한 잡음을 더할 수 있습니다. HarDoc은 먼저 증거를 모은 다음 가장 작은 안전한 정리 후보를 제안합니다.

## 이런 순간에 사용하세요

- AI가 계속 엉뚱한 스킬을 고를 때
- 서로 다른 스킬이 같은 일을 하는 것처럼 보일 때
- 플러그인이나 MCP를 추가한 뒤 세션이 느려지거나 복잡해졌을 때
- 규칙·훅·에이전트의 지시가 서로 충돌하는 것 같을 때
- 무엇을 지워도 되는지 근거가 필요할 때
- 하네스를 바꾼 뒤 실제 업무가 퇴행하지 않았는지 확인할 때

## 안전 약속

HarDoc은 사용자가 승인하지 않은 변경을 하지 않습니다.

`skill-governor` 스킬은 읽기 전용입니다. 보고만 하고 삭제, 비활성화, 설치, 설정 수정, doctor 결과 자동 수정, 외부 메시지 발송을 하지 않습니다. “정리 후보”라는 표현은 사람이 검토할 제안입니다.

`trim` 스킬은 설정을 바꿀 수 있습니다. 단 먼저 보여준 변경 목록을 사용자가 승인한 뒤에만 적용합니다. 쓰기 전에 건드릴 파일을 모두 스냅샷으로 떠 두고, 끝나면 되돌리는 명령 한 줄을 알려줍니다. 설치는 하지 않고 프로젝트 소스도 건드리지 않으며, 훅과 에이전트는 사용자가 따로 지정할 때만 다룹니다.

## Claude Code에 설치하기

한 번만 다음 명령을 실행하세요.

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

새 Claude Code 세션을 열고 다음을 실행합니다.

```text
/skill-governor audit .
```

HarDoc에는 스킬이 두 개 있습니다. `skill-governor`는 진단하고 거기서 멈춥니다. `trim`은 그 진단을 사용자가 승인한 변경으로 옮기고 돌아갈 길을 남깁니다. 기존 설치와의 호환성을 위해 호출 이름은 `skill-governor`로 유지합니다.

## Codex에서 사용하기

Codex에 `skill-governor` 스킬이 이미 노출되어 있다면 다음을 실행하세요.

```text
$skill-governor audit .
```

로컬에서 설치하려면 저장소를 내려받은 뒤, Codex가 사용하는 skills 디렉터리에 `plugin/skills/skill-governor`를 복사하거나 연결합니다.

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

새 Codex 세션에서 `$skill-governor audit .`를 실행하세요. 스킬은 설치된 Codex 버전과 지원되는 도움말을 확인한 뒤, 사용할 수 있을 때 native `codex doctor`를 점검합니다.

## `audit`가 확인하는 것

HarDoc은 먼저 대상 디렉터리가 실제로 있는지 확인합니다. 그 다음 런타임 버전과 도움말에서 지원 범위를 확인하고, 해당 런타임의 doctor 명령을 시도합니다.

| 런타임 | doctor 점검 | 함께 보는 항목 |
| --- | --- | --- |
| Claude Code | `claude doctor` | 스킬, MCP, 플러그인, 훅, 규칙, 에이전트 |
| Codex | `codex doctor` | 스킬, MCP, 플러그인, 훅, 규칙, 에이전트 |

보고서에서는 다음 질문을 구분합니다.

1. 설치되어 있는가?
2. 활성화되어 세션에 노출되는가?
3. 실제로 선택되거나 호출되었는가?
4. 의존성이나 안전상 유지할 이유가 있는가?
5. 수정 후보를 적용했을 때 실제 업무가 통과했는가?

doctor가 성공해도 모든 업무가 정확하다는 뜻은 아닙니다. doctor는 하네스 건강 상태를 보여주는 사전 점검이고, 정확도는 실제 업무 회귀평가로 확인해야 합니다.

## 세 가지 모드

| 모드 | 하는 일 | 사용하는 시점 |
| --- | --- | --- |
| `audit` | 근거를 읽기 전용으로 수집하고 발견사항을 분류합니다. | 항상 여기서 시작합니다. |
| `propose` | 근거를 최소 수정안·검증 방법·복구 방법으로 정리합니다. | 실제 후보를 찾은 뒤 사용합니다. |
| `evaluate` | 기준본과 후보본을 같은 실제 업무로 비교합니다. | 개선을 주장하기 전에 사용합니다. |

평가할 때는 두 조건의 호스트·모델·권한·업무 입력을 맞춥니다. 오선택, 필수 스킬 누락, 지시 충돌, 업무 결과를 따로 기록합니다. 토큰 수나 응답 속도만 줄었다고 정확도가 좋아진 것으로 판정하지 않습니다.

## `trim`으로 정리하기

`skill-governor`는 제안까지 하고 멈춥니다. 그 제안을 실행하는 쪽이 `trim`입니다.

```text
/trim --dry-run
```

이 컴퓨터에서 어떤 일을 하는지 네 가지 이내로 묻고, 그 답을 기준으로 매 세션 항상 로드되는 항목을 무거운 순으로 줄 세운 다음, 아무것도 쓰기 전에 표로 보여줍니다. 승인한 항목만 적용합니다.

기본 처방은 삭제가 아닙니다. Claude Code는 스킬 이름만 남기고 설명을 감출 수 있어서, 스킬은 그대로 작동하고 슬래시 명령으로도 부를 수 있으면서 상시 토큰만 줄어듭니다. 이 단계에서 잘못 골라도 잃는 게 없습니다. 완전히 감추는 처방은 사용자가 직접 요청할 때만 적용합니다.

두 가지는 기본에서 빠져 있습니다. 훅과 에이전트는 공식 스위치가 없어서 끄려면 설정 파일에서 항목을 잘라내거나 파일을 옮겨야 하므로, `--include-hooks`를 줄 때만 다룹니다. 나머지는 전부 되돌릴 수 있는 플래그를 씁니다.

```text
/trim restore 20260922-101500
```

되돌릴 때는 값마다 스냅샷과 대조합니다. 스냅샷을 뜬 뒤에 사용자가 직접 고친 부분이 있으면 덮어쓰지 않고 충돌로 알립니다.

컨텍스트가 줄었다고 저절로 좋아진 것은 아닙니다. 정확도가 실제로 나아졌는지 알고 싶으면 실제 업무로 비교하는 `skill-governor evaluate`로 돌아가세요.

## 보고서 읽는 법

- **유지**: 계속 필요한 근거가 있습니다.
- **정리 후보**: 단순화 가능성이 있지만 의존성과 복구 방법을 사람이 검토해야 합니다.
- **고장 수정 후보**: 고장이나 재현 가능한 문제로 보입니다.
- **관측 부족**: 현재 자료만으로 결정할 수 없습니다.

doctor 상태도 별도로 기록합니다.

- `COMPLETED`: 명령이 끝났다는 뜻입니다. 하네스가 건강하다는 뜻은 아닙니다.
- `UNSUPPORTED`, `ERROR`, `TIMEOUT`, `NOT_RUN`: 해당 doctor 검증은 `UNVERIFIED`입니다.

경로가 없거나 디렉터리가 아닌 파일이면 오류로 보고하고, 상위 디렉터리나 홈 전체를 몰래 검사하지 않습니다.

## 처음 실행하는 순서

1. 점검할 프로젝트 폴더를 엽니다.
2. Claude Code에 HarDoc을 설치하거나 Codex에 스킬을 노출합니다.
3. 새 세션을 열어 스킬 목록을 다시 읽게 합니다.
4. Claude Code에서는 `/skill-governor audit .`, Codex에서는 `$skill-governor audit .`를 실행하고 보고서를 기다립니다.
5. 먼저 doctor 상태를 확인합니다.
6. 정리 후보의 근거와 영향 범위를 읽습니다.
7. 그 다음에만 수정안을 만들고 실제 업무로 평가합니다.
8. 실제로 정리할 때는 `/trim --dry-run`을 실행하고 표를 읽은 뒤에 승인합니다.

호출 횟수가 0이라는 이유만으로 바로 삭제하지 마세요. 드물게 필요한 기능일 수도 있고, 다른 컴퓨터에서만 사용하거나 프로젝트 파일이 직접 읽는 기능일 수도 있습니다.

## 호환성 메모

- 플러그인 machine name은 `hardoc`입니다.
- marketplace 이름은 `hardoc-marketplace`입니다.
- 플러그인에는 스킬이 두 개 들어 있습니다. `skill-governor`(진단)와 `trim`(승인 후 적용)입니다.
- 기존 설치와의 호환성을 위해 호출 slug는 `skill-governor`입니다.
- `trim`은 실제로 실행 중인 런타임의 설정 스키마를 읽습니다. `PATH` 앞쪽에 오래된 CLI가 있으면 지금 빌드가 지원하는 키를 모를 수 있습니다.
- Claude Code와 Codex는 각각 따로 점검합니다. 한쪽 런타임의 결과를 다른 쪽 결과로 복사하지 않습니다.
- CLI 버전이 doctor나 출력 옵션을 지원하지 않으면 추측하지 않고 그 사실을 기록합니다.

## 라이선스

현재 라이선스와 배포 조건은 저장소 메타데이터를 확인하세요.
