# Learning Log (Django)

Keep track of what you’re learning. This Django web app lets users create topics and add timestamped entries under each topic. It includes authentication, Bootstrap styling, and a clean CRUD workflow.

## Features
- **User Accounts**: Sign up, log in, and log out.
- **Topics**: Create and list personal topics you’re learning.
- **Entries**: Add, edit, and view entries for each topic (reverse chronological).
- **Ownership**: Topics and entries are tied to the authenticated user.
- **Responsive UI**: Uses `django-bootstrap5` for styling.

## Tech Stack
- **Backend**: Django 5.1
- **Frontend**: Django templates + `django-bootstrap5`
- **Database**: SQLite (dev)

Key apps and modules:
- `learning_logs/`: Domain app with `Topic` and `Entry` models and CRUD views.
- `accounts/`: Authentication views and URLs (login, logout, register if implemented).
- `ll_project/`: Project settings and URL routing.

## Getting Started (Local)

Prereqs: Python 3.11+ recommended (project created with Django 5.1). You can use any virtual environment tool.

1) Create and activate a virtual environment
```bash
python -m venv .venv
source .venv/bin/activate  # macOS/Linux
# .\.venv\Scripts\activate  # Windows PowerShell
```

2) Install dependencies
```bash
pip install "Django>=5.1,<6" django-bootstrap5
```

3) Run migrations
```bash
python learning_log/manage.py migrate
```

4) Create a superuser (optional, for admin access)
```bash
python learning_log/manage.py createsuperuser
```

5) Start the development server
```bash
python learning_log/manage.py runserver
```

Open http://127.0.0.1:8000/ to use the app.

## Core URLs
- `"/"` → Home/index (`learning_logs:index`)
- `"/topics/"` → List topics
- `"/topics/<topic_id>/"` → Topic detail with entries
- `"/new_topic/"` → Create topic
- `"/new_entry/<topic_id>/"` → Add entry
- `"/edit_entry/<entry_id>"` → Edit entry
- `"/accounts/"...` → Auth routes (login/logout, etc.)

## Data Model
- `Topic(text, date_added, owner)`
- `Entry(topic, text, date_added)`

Defined in `learning_log/learning_logs/models.py`.

## Project Structure
```text
learning_log/
├─ accounts/
├─ learning_logs/
│  ├─ models.py        # Topic, Entry
│  ├─ views.py         # index, topics, topic, new_topic, new_entry, edit_entry
│  ├─ urls.py
│  └─ templates/
├─ ll_project/
│  ├─ settings.py      # INSTALLED_APPS includes learning_logs, accounts, django_bootstrap5
│  └─ urls.py          # routes accounts/ and learning_logs/
└─ manage.py
```

## Notes
- Dev DB is SQLite (`learning_log/db.sqlite3`). For production, switch to a managed DB and set `DEBUG=False`, `ALLOWED_HOSTS`, and a secure `SECRET_KEY` via environment variables.
- Styling is via `django-bootstrap5`. Customize templates under `learning_log/learning_logs/templates/`.

