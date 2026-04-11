---
applyTo: "**"
---

# Copilot Instructions — Soc Ops

**Project:** Social Bingo game for in-person mixers (FastAPI + Jinja2 + HTMX)
**Language:** Python 3.13+ | **Manager:** UV | **Deploy:** Uvicorn 0.0.0.0:8000

---

## ✅ Mandatory Dev Checklist

Before committing or testing:
```bash
uv run ruff check .           # Lint (E, F, I, N, W rules)
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000  # Build/Run
uv run pytest                 # Test (all must pass)
```
**⚠️ Constraint:** Never use Simple Browser; manually confirm at `http://localhost:8000`

---

## 📋 Quick Reference

| Command | Purpose |
|---------|---------|
| `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000` | Start dev server |
| `uv run pytest` | Run all tests |
| `uv run ruff check .` | Lint check |

---

## 📂 Essential Files

- **`app/main.py`** — FastAPI routes, session middleware, template rendering
- **`app/game_logic.py`** — Board generation, toggle, bingo detection (`@functools.cache`)
- **`app/game_service.py`** — `GameSession` dataclass, state machine (START → PLAYING → BINGO)
- **`app/models.py`** — Pydantic immutable models (`GameState`, `BingoSquareData`, `BingoLine`)
- **`tests/`** — Pytest suite (API routing, game logic, sessions)
- **`.github/instructions/`** — Domain-specific guides (CSS, frontend design, general rules)
- **`.github/agents/`** — Pixel Jam, Quiz Master, TDD workflow agents

---

## 🎮 Architecture

| Pattern | Implementation |
|---------|-----------------|
| **Sessions** | Cookie UUID → in-memory dict (`request.session["session_id"]`) |
| **State** | `GameState` enum: START → PLAYING → BINGO |
| **Data** | Immutable (frozen Pydantic models, new board lists) |
| **Caching** | `@functools.cache` on winning lines |
| **Updates** | HTMX partial HTML responses (`hx-post`, `hx-swap="innerHTML"`) |
| **Layers** | Logic → Service → Handler → Template |

**Endpoints:** `GET /`, `POST /start`, `POST /toggle/{id}`, `POST /reset`, `POST /dismiss-modal`

---

## 🎨 Frontend & CSS

- **Templates:** Jinja2 with inheritance (`base.html`), HTMX for updates, no page reloads
- **Styling:** Custom utility classes in `app/static/css/app.css` (no external framework)
- **Design:** Avoid "AI slop" — use distinctive fonts, cohesive colors, thoughtful motion
- **Refs:** [CSS Utilities](.github/instructions/css-utilities.instructions.md), [Frontend Design](.github/instructions/frontend-design.instructions.md)

---

## 🧪 Testing

**Pytest** with FastAPI TestClient; tests in `tests/` folder (configured in `pyproject.toml`)

**Coverage:** Game logic, API routing, sessions, HTMX behavior

**Rules:** All tests must pass; Ruff rules E, F, I, N, W enforced

---

## 🚀 Workflow

**Adding a Feature:**
1. Write failing tests in `tests/` (Red phase)
2. Implement logic in `app/`, handlers in `app/main.py`, templates in `app/templates/`
3. Run `pytest` and `ruff check .`; verify at dev server

**Modifying Game Logic:**
- Edit `app/game_logic.py` (pure functions, immutable)
- Update tests in `tests/test_game_logic.py`
- Verify no breaks in `test_api.py`

**Updating Templates:**
- Extend `base.html`; use Jinja2 includes for components
- Leverage CSS utilities (add new ones to `app.css` if needed)
- Test HTMX swaps in dev server

---

## 📚 Agents & Skills

- **Pixel Jam** — UI design iterative workflow with design-spec.md
- **Quiz Master** — Curate themed bingo questions
- **TDD Workflow** — Red → Green → Refactor phases

See [.github/instructions/](github/instructions/) and [.github/agents/](.github/agents/) for full details.

---

## 🌍 i18n

Project supports EN, ES, PT_BR with separate doc trees:
- Workshop: `workshop/`, `workshop/es/`, `workshop/pt_BR/`
- README: `README.md`, `README.es.md`, `README.pt_BR.md`

---

## 📝 Code Conventions

- **Python:** PEP 8, type hints encouraged
- **Naming:** snake_case (functions/vars), PascalCase (classes)
- **Imports:** stdlib → third-party → local (Ruff enforces)
- **CSS:** Custom utilities only; no inline styles
- **HTML:** Semantic tags; leverage Jinja2 (DRY)
