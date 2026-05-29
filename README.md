# Toggl Skill

Toggl Track 시간 추적 데이터를 Claude Code agent가 read/write하는 CLI skill.

## Setup

1. **Get Toggl API Token**: track.toggl.com → 프로필 → Profile Settings → 페이지 하단 **API Token** → reveal+copy
2. **Link**:
   ```bash
   python3 toggl link <api_token>
   ```
3. Workspace ID는 `/me` endpoint로 자동 detect

## Usage

```bash
python3 toggl whoami              # 본인 정보
python3 toggl list                # project 목록
python3 toggl today               # 오늘 time entries (project별 합산)
python3 toggl summary --days 7    # 최근 N일 요약
python3 toggl current             # 진행 중 timer
python3 toggl start "manifesto" --project Heisenberg
python3 toggl stop                # 현재 timer stop
```

## Architecture

- **API**: Toggl Track REST API v9 (`api.track.toggl.com/api/v9`)
- **Auth**: Basic Auth — `<api_token>:api_token`
- **Storage**: `.user` (mode 0o600) — `api_token`, `workspace_id`
- **No dependencies**: stdlib only (urllib + base64)

## Integration with The System

Toggl은 The System의 5번째 context source:

| Source | Layer |
|--------|-------|
| Obsidian my-note | 1차 자유 메모 + Research/Meeting Note #tag |
| Google Tasks | Daily + Later (todo) |
| Google Calendar | Guide Plan + 0_MLML (schedule) |
| HabitLoop habits | streak long-term |
| **Toggl** (new) | **actual time spent (retrospective)** |

agent 사용 패턴:
- **read** (sweep cron): "오늘 manifesto 1.5h / heisenberg 2h" 한 줄 보고
- **write** (Tasks 체크 시): my-note Work `[x] DONE` → 자동 Toggl entry seed
- **분석** (sleep cron): 주말 retrospective "이 주 manifesto 8h vs 목표 10h gap"

## License

MIT.
