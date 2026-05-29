# Toggl Skill

Toggl Track 시간 추적 데이터 read/write.

## 첫 사용 시

`.user` 파일이 없으면 사용자에게 API token 받기:
1. track.toggl.com → Profile Settings → API Token (reveal+copy)
2. `python3 toggl link <token>`

## 사용

- "오늘 시간 어떻게 썼어" → `python3 toggl today`
- "이번 주 어디에 시간 썼나" → `python3 toggl summary`
- "지금 timer 뭐 돌고 있어" → `python3 toggl current`
- "manifesto에 timer 시작" → `python3 toggl start "manifesto" --project Heisenberg`
- "timer 멈춰" → `python3 toggl stop`
