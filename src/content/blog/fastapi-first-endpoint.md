---
title: 'FastAPI: Creating and Testing My First API Endpoint'
description: 'Building a GET endpoint in an isolated Python environment and verifying it with pytest and Swagger UI.'
pubDate: '2026-10-10'
tags: ['Python', 'FastAPI', 'Testing']
draft: false
---

## What I wanted to learn

This exercise explores how to create a small FastAPI endpoint, test its
response automatically, and call it through interactive API documentation.

## My environment

| Tool | Version |
| --- | --- |
| Python | 3.13.14 |
| FastAPI | 0.143.0 |
| Uvicorn | 0.54.0 |
| pytest | 9.1.1 |
| HTTPX | 0.28.1 |

I used Windows and VS Code.

My terminal initially resolved Python to another project's virtual
environment. Changing folders did not change that interpreter.

I created a separate lab environment and used its Python executable
explicitly for installation, testing, and running the server.

## Implementation

I created `main.py`:

```python
from fastapi import FastAPI

app = FastAPI(title="My First FastAPI Learning Lab")


@app.get("/hello")
def hello():
    return {"message": "Hello from my learning lab!"}
```

The decorator associates GET requests to `/hello` with the function.
The function returns a dictionary, which FastAPI sends as JSON.

This example has no database, authentication, or external services.

## Automated testing

I created `test_main.py`:

```python
from fastapi.testclient import TestClient

from main import app


def test_hello_returns_expected_response():
    with TestClient(app) as client:
        response = client.get("/hello")

    assert response.status_code == 200
    assert response.headers["content-type"].startswith("application/json")
    assert response.json() == {
        "message": "Hello from my learning lab!"
    }


def test_unknown_route_returns_not_found():
    with TestClient(app) as client:
        response = client.get("/does-not-exist")

    assert response.status_code == 404
```

From the lab directory, I ran pytest using its virtual environment:

```powershell
& '.\.venv\Scripts\python.exe' -m pytest -v
```

The result was:

```text
2 passed, 1 warning in 1.15s
```

The tests checked the successful response, JSON content type, exact
response body, and a 404 response for an unknown route.

TestClient exercised the application without a separate running server.

## Browser verification

From the lab directory, I started Uvicorn:

```powershell
& '.\.venv\Scripts\python.exe' -m uvicorn main:app --host 127.0.0.1 --port 8011
```

I opened `http://127.0.0.1:8011/docs`, expanded GET `/hello`,
clicked **Try it out**, and then **Execute**.

The server returned HTTP 200 with:

```json
{
  "message": "Hello from my learning lab!"
}
```

The response content type was `application/json`.

## Warning and documentation limitation

The test run reported a Starlette deprecation warning: using HTTPX
with TestClient is deprecated in the installed version, with HTTPX2
suggested as its replacement. Both tests still passed.

I have recorded the warning rather than claiming a warning-free run.

Swagger UI displayed a generic string example in its response schema.
The actual response was a JSON object. This endpoint does not yet
declare a response model; adding one is a useful follow-up exercise.

## What I learned

- The current folder and active Python environment are separate concerns.
- Explicit interpreter paths help keep learning experiments isolated.
- Tests should check response behavior, including unsuccessful requests.
- A passing test run can still contain dependency warnings.
- Browser execution confirms that the running server responds as expected.

## References

- [FastAPI: First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)
- [FastAPI: Testing](https://fastapi.tiangolo.com/tutorial/testing/)
