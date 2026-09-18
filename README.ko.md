# HarDoc

HarDoc은 Claude Code·Codex 하네스의 중복·충돌·불필요 노출을 읽기 전용으로 진단합니다. 스킬·MCP·플러그인·hooks·규칙·에이전트를 설치 상태, 활성 상태, 노출, 실제 호출, 사용량, 의존성으로 나누어 보고하며 `claude doctor` 또는 `codex doctor`와 실제 업무 회귀평가를 함께 확인합니다.

## Claude Code marketplace 설치

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

새 Claude Code 세션에서 다음을 실행하세요.

```text
/skill-governor audit .
```

기존 호출 호환성을 위해 스킬 slug `skill-governor`는 유지하고, 플러그인 표시명은 **HarDoc**으로 사용합니다.

## 범위

HarDoc은 근거와 최소 수정안만 보고합니다. 자동 삭제·비활성화·설치·하네스 설정 수정·doctor 자동 수정·외부 발송은 수행하지 않습니다.
