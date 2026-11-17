# bias-skills

AI가 답할 때 사용자 의견, 먼저 나온 숫자, 권위 같은 것에 끌려가지 않게 막는 스킬 두 개입니다. [Agent Skills](https://agentskills.io) 형식(SKILL.md)이라서 이 형식을 지원하는 AI에 설치해서 쓸 수 있습니다.

| 스킬 | 하는 일 |
|---|---|
| [bias-tripwire](skills/bias-tripwire/SKILL.md) | 답을 쓰기 전에 질문, 첨부, 이전 대화에서 편향 위험 신호를 찾아 대응을 정합니다. |
| [bias-guard](skills/bias-guard/SKILL.md) | 위의 사전 점검에 더해, 답을 쓴 뒤 인지 편향과 아첨을 A~L 항목으로 점검합니다. |

두 스킬 모두 **재작성 모드**가 있습니다. 이미 쓴 글(이전 답, 내가 쓴 글, 다른 AI의 답)을 주고 "편향 점검해서 다시 써 줘"라고 하면 점검 결과, 고친 점, 다시 쓴 글, 보완 제안 순서로 돌려줍니다.

## 설치

### 코딩 에이전트 (Claude Code, Codex, Cursor, Gemini CLI, GitHub Copilot 등)

```bash
npx skills add hamjw-97/bias-skills
```

`-a claude-code`처럼 설치할 에이전트를 고르거나, `--skill bias-guard`처럼 스킬 하나만 고를 수 있습니다. 직접 넣으려면 `skills/` 아래 폴더를 각 도구의 스킬 폴더(Claude Code는 `~/.claude/skills/`)에 복사합니다.

### 채팅 앱 (ChatGPT, Claude.ai)

이 저장소의 Releases 페이지에서 zip을 받아 각 앱의 Skills 메뉴에서 하나씩 올립니다. ChatGPT는 Skills → Create → Upload from your computer 순서입니다. 요금제에 따라 Skills 메뉴가 없을 수 있습니다.

## 쓰는 법

- 판단, 평가, 추정, 조언이 필요한 질문이면 AI가 알아서 이 스킬을 고릅니다.
- 직접 부를 때는 ChatGPT에서 `@bias-guard`, Claude Code에서 `/bias-guard`라고 씁니다.
- 재작성 예시: 글을 붙여 넣고 "@bias-guard 이 글 편향 점검해서 다시 써 줘".

## zip 다시 만들기

스킬을 고친 뒤 채팅 앱용 zip을 다시 만드는 방법입니다. 저장소 최상위 폴더에서 실행하고, `dist` 폴더가 없으면 먼저 만듭니다. `dist/`는 git에 올라가지 않습니다.

```bash
tar -a -c -f dist/bias-guard.zip -C skills bias-guard
tar -a -c -f dist/bias-tripwire.zip -C skills bias-tripwire
```

Windows(PowerShell이나 명령 프롬프트)와 macOS의 기본 tar로 됩니다. Git Bash의 tar는 zip 대신 tar 파일을 만드니 쓰지 마세요. Linux에서는 `cd skills && zip -r ../dist/bias-guard.zip bias-guard`처럼 만듭니다.
