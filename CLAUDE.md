# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Flask web application that displays course information. Uses a simple MVC-like pattern with in-memory data storage (no database).

## Development Commands

### Setup
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
uv pip install -r requirements.txt
```

### Run Application
```bash
python src/app.py
```
The app runs on `http://127.0.0.1:5000` by default with debug mode enabled.

### Run Tests
```bash
python -m unittest discover -s tests
```

To run a single test file:
```bash
python -m unittest tests.test_app
```

To run a specific test case:
```bash
python -m unittest tests.test_app.AppTestCase.test_index
```

## Architecture

### Request Flow
1. Routes are registered in [src/app.py](src/app.py) using `app.add_url_rule()`
2. View functions in [src/views.py](src/views.py) handle requests
3. Templates in `src/templates/` render responses using Jinja2
4. All templates extend [src/templates/layout.html](src/templates/layout.html) base template

### Data Layer
Course data is hardcoded in [src/models.py](src/models.py) as a list of `Course` objects. There is no database or persistence layer.

### Testing Conventions
Tests must add `src/` to `sys.path` to import application modules (see [tests/test_app.py:6](tests/test_app.py#L6)). This is required because the tests directory is outside the src package structure.

## Key Patterns

- **URL Routing**: Routes are registered programmatically in app.py rather than using decorators
- **View Functions**: Pure functions that return rendered templates, no class-based views
- **Static Course Data**: To modify course information, edit the `courses` list in models.py
## Add unit test
-whenever you add any changes add unit test and run make sure the unit test should pass