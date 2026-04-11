🌐 [Português (BR)](README.pt_BR.md) | [Español](README.es.md)

# 🎱 Soc Ops

> **Social Bingo for in-person mixers.** Find people who match the questions, mark your card, get 5 in a row — first to win yells *BINGO!*

Built with **FastAPI + HTMX** — no page reloads, pure fun.

---

## 🚀 Quick start

```bash
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
# → open http://localhost:8000
```

---

## 📚 Lab Guide

| Part | Title |
|------|-------|
| [**00**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=00-overview) | Overview & Checklist |
| [**01**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=01-setup) | Setup & Context Engineering |
| [**02**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=02-design) | Design-First Frontend |
| [**03**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=03-quiz-master) | Custom Quiz Master |
| [**04**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=04-multi-agent) | Multi-Agent Development |

> 📝 Guides also available in [`workshop/`](workshop/) for offline reading.

---

## 🗂 Project layout

```
app/
├── main.py          # FastAPI routes
├── game_service.py  # Session management
├── game_logic.py    # Board & win detection
├── models.py        # Pydantic models
├── data.py          # Question bank
└── templates/       # Jinja2 + HTMX views
tests/               # 25 pytest tests
```

---

## 🛠 Dev commands

| Command | What it does |
|---------|-------------|
| `uv run uvicorn app.main:app --reload` | Start dev server |
| `uv run pytest` | Run all 25 tests |
| `uv run ruff check .` | Lint code |

