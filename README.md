# devops docs

Практическая работа 9 по дисциплине «Инструменты DevOps», РТУ МИРЭА.

## О репозитории

Учебный сайт документации на MkDocs. Страницы пишутся в Markdown, проверяются в GitHub Actions и публикуются на GitHub Pages.

В документации три раздела: главная с описанием процесса поставки, инструкция по эксплуатации и журнал типовых инцидентов. Рядом лежит небольшой Python-модуль `src/status.py`, который проверяется Pylint.

Сайт доступен по адресу https://vleypi.github.io/devops-docs/.

## Как работает CI

- **Проверка** (`quality.yml`). На каждый push и Pull Request в `main` запускается Pylint для `src/status.py`, а затем строгая сборка документации. Любая битая ссылка или предупреждение MkDocs роняет проверку.
- **Публикация** (`pages.yml`). После изменений в `docs/` или `mkdocs.yml` в ветке `main` сайт собирается и выкладывается на GitHub Pages.

## Как запустить

Потребуются Git и Python 3.10 или новее.

```bash
git clone https://github.com/vleypi/devops-docs.git
cd devops-docs
python -m venv .venv
source .venv/bin/activate
pip install -r requirements-dev.txt
mkdocs serve
```

После запуска документация доступна по адресу http://localhost:8000. Проверки CI локально:

```bash
python -m pylint src/status.py
mkdocs build --strict
```

## Структура

```
devops-docs/
├── docs/
│   ├── index.md          главная
│   ├── runbook.md        эксплуатация
│   └── incidents.md      журнал инцидентов
├── src/
│   └── status.py         модуль для проверки Pylint
├── .github/workflows/
│   ├── quality.yml       Pylint и сборка документации
│   └── pages.yml         публикация на GitHub Pages
├── mkdocs.yml            настройки MkDocs
└── requirements-dev.txt  зависимости
```

Каталог `site/` появляется после сборки и в Git не хранится.
