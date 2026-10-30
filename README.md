# arena

Минимальный Python-проект с «Hello, World!» и проверкой синтаксиса в GitHub Actions.

## Запуск

```bash
python main.py
# Hello, World!
```

Требуется Python 3.10+.

## CI (GitHub Actions)

Workflow: [`.github/workflows/ci.yml`](.github/workflows/ci.yml)

Запускается на **каждый push** (в любую ветку), на pull request и вручную
(`workflow_dispatch`).

| Job | Что делает |
| --- | --- |
| **Syntax check** | Python 3.10 / 3.11 / 3.12 / 3.13. Каждый `.py` файл компилируется через `compile()`, при `SyntaxError` job падает с указанием файла и строки. Затем `python main.py` как smoke-тест. |
| **Lint** | `ruff check` + `ruff format --check` (конфиг в `pyproject.toml`). |

Локально проверить то же самое:

```bash
python -m compileall -q .            # синтаксис
pip install ruff
ruff check . && ruff format --check .  # линт
```

## Структура

```
main.py                     # точка входа, печатает Hello, World!
pyproject.toml              # метаданные проекта + конфиг ruff
.github/workflows/ci.yml    # CI: синтаксис + линт
```
