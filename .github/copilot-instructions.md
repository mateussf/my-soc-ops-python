# Copilot Workspace Instructions

**Soc Ops** is a Social Bingo game built with **FastAPI**, **Jinja2**, and **HTMX** for in-person mixers. Players find people matching bingo card questions to get 5-in-a-row.

## Quick Start

```bash
# Run dev server (http://localhost:8000)
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Run test suite
uv run pytest

# Lint code
uv run ruff check .
```

## Architecture

| Component | Purpose | Key Files |
|-----------|---------|-----------|
| **Backend** | FastAPI routes, server-side state management | `app/main.py`, `app/game_service.py` |
| **Game Logic** | Board generation, bingo detection, rules | `app/game_logic.py`, `app/models.py` |
| **Frontend** | Jinja2 templates, HTMX for dynamic updates | `app/templates/`, `app/static/` |
| **Data** | Question bank and game content | `app/data.py` |
| **Tests** | Unit & integration tests (25 total) | `tests/test_api.py`, `tests/test_game_logic.py` |

### State Management
- **GameSession**: UUID-based server-side session management
- **Persistence**: Signed cookies via `itsdangerous`
- **State Model**: `GameState` enum (IDLE, GAME_STARTED, PLAYER_WON)

### Frontend Pattern
- HTMX handles partial page updates without full page reloads
- Template responses return HTML fragments
- Custom CSS utilities (Tailwind-like) defined in `app/static/css/app.css`

## Pre-Commit Checklist

Before committing:
- [ ] `uv run ruff check .` passes with no errors
- [ ] `uv run pytest` passes (all 25 tests)
- [ ] Type hints on all function parameters and returns
- [ ] No unused imports or variables
- [ ] Code follows snake_case (functions/variables) and PascalCase (classes)

## Development Guidelines

### Code Style
- **Python version**: 3.13+
- **Line length**: 88 characters (Ruff default)
- **Type hints**: Required for function signatures
- **Import order**: Alphabetical, grouped (stdlib → third-party → local)

### Styling
Refer to [CSS Utilities Instructions](.github/instructions/css-utilities.instructions.md) for:
- Available utility classes (layout, spacing, colors, typography)
- Component styling patterns
- Composing utilities

### Frontend Design
Refer to [Frontend Design Instructions](.github/instructions/frontend-design.instructions.md) for:
- Creating distinctive, polished UI (avoiding "AI slop")
- Typography and color strategy
- Animation best practices

### General Guidelines
Refer to [General Instructions](.github/instructions/general.instructions.md) for:
- Tool usage restrictions
- Browser preview guidelines

## Common Tasks

### Add a New Route
1. Define endpoint in `app/main.py` with `@app.get()` or `@app.post()`
2. Return `TemplateResponse` for HTML responses
3. Create or update template in `app/templates/`
4. Add tests in `tests/test_api.py`

### Add New Questions
Edit `app/data.py` with diverse, inclusive questions for social mixers

### Update Styling
- Add utilities to `app/static/css/app.css` if needed
- Use existing utilities as reference
- Follow Tailwind-like naming conventions

### Write Tests
Use pytest with TestClient:
```python
from fastapi.testclient import TestClient
from app.main import app

client = TestClient(app)
response = client.get("/")
assert response.status_code == 200
```

## Dependencies

**Runtime**: fastapi, jinja2, uvicorn, itsdangerous
**Dev**: pytest, httpx, ruff

Install new dependencies with `uv add <package>`

## Resources

- **Workshop Guide**: [Lab Steps](workshop/) (also available at [Copilot Dev Days](https://copilot-dev-days.github.io/agent-lab-python/))
- **Contributing**: [CONTRIBUTING.md](CONTRIBUTING.md)
- **Code of Conduct**: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)

##Key Files Reference

- `app/main.py` - FastAPI application, routes, HTMX endpoints
- `app/game_service.py` - GameSession class for state management
- `app/game_logic.py` - Board generation, win detection logic
- `app/models.py` - Pydantic models (GameState, BingoSquare)
- `app/data.py` - Question bank and game data
- `app/templates/base.html` - Base layout template
- `app/templates/components/` - Reusable component templates
- `tests/test_api.py` - API endpoint tests (8 tests)
- `tests/test_game_logic.py` - Game logic unit tests (17 tests)
