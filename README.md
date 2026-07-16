# 30-Day Python Crash Course
### For Suneel — 1-2 hrs/day, comfortable with scripts, going deep on OOP → advanced Python → FastAPI → Data/ML

**Instructor's note:** You already write working Python — this course doesn't touch basic syntax, loops, or lists. It starts exactly at your stated gap (OOP) and builds outward. Each week's output becomes the next week's building block, ending in one real deployed project that touches everything: a proper class-based codebase, tested and packaged, exposed as a FastAPI service, backed by a database, with a lightweight ML model serving predictions through it.

**Realistic outcome by Day 30:** Confident OOP and advanced Python (decorators, generators, async, typing, testing). A working FastAPI backend with a real database and auth. Practical fluency in NumPy/pandas/scikit-learn for data work. One complete, deployed capstone project proving all of it works together — not four disconnected tutorials.

---

## WEEK 1 — OOP & Pythonic Fundamentals

**Day 1 — Functions, Revisited: `*args`, `**kwargs`, Decorators Intro**
- Variable-length arguments, keyword-only arguments, first-class functions (functions as values), a first look at decorators
- Exercise: write a `@timer` decorator that logs a function's execution time

**Day 2 — OOP Basics**
- `class`, `__init__`, instance vs class attributes, methods, `self`
- Analogy: a class is a resource *type* (like a Terraform resource block); an instance is one deployed resource of that type
- Exercise: build a `Server` class with `name`, `cpu`, `status`, and a `report()` method

**Day 3 — Inheritance, Polymorphism, Magic Methods**
- `class WebServer(Server):`, method overriding, `super()`, `__str__`, `__repr__`, `__eq__`
- Exercise: `WebServer` and `DatabaseServer` subclasses overriding a `health_check()` method differently

**Day 4 — Decorators Deep Dive & Closures**
- Closures, decorators with arguments, `functools.wraps`, stacking decorators
- Exercise: a `@retry(times=3)` decorator for flaky operations — directly useful for your infra scripting

**Day 5 — Generators, Iterators, Context Managers**
- `yield`, generator expressions, the iterator protocol, `with` statements, writing a custom context manager
- Exercise: a generator that lazily reads a huge log file line by line; a custom context manager for timing a code block

**Day 6 — Error Handling, Properly**
- Custom exception classes, `try/except/else/finally`, exception chaining, when to catch vs let propagate
- Exercise: a custom `ServerUnhealthyError` hierarchy used across your Day 2-3 classes

**Day 7 — Review + Mini Project**
- Build a class-based CLI tool: server inventory manager using your `Server`/`WebServer`/`DatabaseServer` classes, custom exceptions, a decorator for logging actions, and a generator for reading input from a file

---

## WEEK 2 — Advanced Python & Tooling

**Day 8 — Type Hints & Dataclasses**
- `typing` module (`List`, `Optional`, `Union`), `@dataclass` as a lighter alternative to hand-written classes
- Exercise: convert Week 1's `Server` class to a `@dataclass`, add full type hints

**Day 9 — Modules, Packages, Virtual Environments**
- Package structure (`__init__.py`), relative imports, `venv`, `pip`, intro to `poetry` as a modern alternative
- Analogy: `venv`/`poetry` ≈ your Terraform workspace isolation; `pyproject.toml` ≈ your project manifest
- Exercise: restructure Day 7's project into a proper package with a `pyproject.toml`

**Day 10 — Async Python**
- `async`/`await`, `asyncio.run`, `asyncio.gather` for concurrent operations, when async actually helps (I/O-bound work) vs when it doesn't (CPU-bound)
- Exercise: fetch multiple URLs concurrently with `asyncio` + `httpx`, compare timing to sequential requests

**Day 11 — Testing with Pytest**
- Writing tests, fixtures, parametrize, mocking external calls with `unittest.mock`
- Exercise: write a test suite for Week 1's `Server` classes and Day 4's `@retry` decorator

**Day 12 — File Handling, `pathlib`, Data Formats**
- `pathlib.Path` (the modern replacement for `os.path`), reading/writing JSON and CSV properly
- Exercise: load a CSV of server metrics, transform it, write results to JSON

**Day 13 — Working with APIs**
- `httpx`/`requests`, environment variables (`os.environ`, `python-dotenv`), config management patterns
- Exercise: a script that calls a public API, using env vars for config, with proper error handling from Day 6

**Day 14 — Review + Mini Project**
- Package Day 7's tool properly: add type hints, a test suite, async API calls where relevant, and clean config via environment variables

---

## WEEK 3 — Backend/API Development with FastAPI

**Day 15 — FastAPI Basics**
- Routes, path/query parameters, automatic OpenAPI docs
- Exercise: a `/servers` GET/POST API, reusing your Week 1-2 `Server` dataclass

**Day 16 — Pydantic Models**
- Request/response validation, nested models, custom validators
- Exercise: strict request models for creating/updating servers, with validation errors returned properly

**Day 17 — Async Endpoints & Dependency Injection**
- `async def` route handlers, FastAPI's `Depends()` system
- Analogy: `Depends()` ≈ the DI you saw conceptually in Angular — declare what you need, FastAPI provides it
- Exercise: a shared `get_db()` dependency injected into multiple routes

**Day 18 — Database Integration**
- SQLAlchemy or SQLModel basics, models, sessions, a real Postgres or SQLite-backed API
- Exercise: replace your file-based storage with a real database table

**Day 19 — Authentication Basics**
- Password hashing, JWT issuing/validation, protected routes
- Exercise: a `/login` route issuing a JWT, and a protected `/servers` route requiring it

**Day 20 — Testing FastAPI & Background Tasks**
- `TestClient`, testing routes end-to-end, `BackgroundTasks` for fire-and-forget work
- Exercise: a test suite covering your CRUD routes and auth; a background task that logs every server creation

**Day 21 — Mini Project: Full REST API**
- Complete FastAPI service: CRUD, database-backed, authenticated, tested — your Week 2 skills wired into a real backend

---

## WEEK 4 — Data/ML & Capstone

**Day 22 — NumPy Basics**
- Arrays, vectorized operations, broadcasting — why NumPy is faster than plain Python loops
- Exercise: compute stats (mean, std dev, percentiles) over a dataset of server metrics

**Day 23 — Pandas**
- DataFrames, filtering, grouping, cleaning messy data
- Exercise: load a CSV of historical server metrics, clean it, compute per-server summaries

**Day 24 — Data Visualization**
- matplotlib/seaborn basics — line charts, histograms, bar charts
- Exercise: visualize CPU trends over time per server

**Day 25 — Intro ML with scikit-learn**
- Train/test split, a simple classifier (logistic regression or decision tree), fit/predict
- Exercise: train a model predicting "will this server become unhealthy" from historical metrics

**Day 26 — Model Evaluation & Feature Engineering**
- Accuracy/precision/recall, confusion matrix, basic feature engineering
- Exercise: evaluate Day 25's model, try improving it with an engineered feature

**Day 27 — Serving the Model via FastAPI**
- Load a trained model (`pickle`/`joblib`), a `/predict` endpoint
- Exercise: add a `/predict` route to your Week 3 API that returns the model's health prediction for a given server

**Day 28-29 — Capstone Project**
- One complete system: FastAPI backend, database-backed CRUD, JWT auth, tested, packaged properly, with a `/predict` endpoint serving your Day 25-26 ML model — a genuinely deployable "server health platform"

**Day 30 — Packaging, Deployment, Next Steps**
- `Dockerfile` for the FastAPI app (natural fit given your Kubernetes background), deployment options (Render/Fly.io/your own infra), a realistic 90-day plan for going deeper on whichever of the four areas matters most for your job search

---

## How to Use This
- Same discipline as the JS course: mini-projects are the actual proof of learning, not the reading
- Given the breadth here, it's fine to spend an extra day on any week that needs it — better to solidify OOP and FastAPI (the parts most job-relevant to backend/platform roles) than rush through ML just to hit Day 30 on schedule
- Given your Azure/platform engineering job search, Weeks 1-3 are the highest-leverage material; Week 4 (data/ML) is valuable breadth but treat it as the most flexible week if time gets tight
