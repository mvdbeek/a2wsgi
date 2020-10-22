# a2wsgi

Convert WSGI app to ASGI app or ASGI app to WSGI app.

Pure Python. Only depend on the standard library.

## Install

```
pip install a2wsgi
```

## How to use

Convert WSGI app to ASGI app:

```python
from a2wsgi import WSGIMiddleware

ASGI_APP = WSGIMiddleware(WSGI_APP)
```

Convert ASGI app to WSGI app:

```python
from a2wsgi import ASGIMiddleware

WSGI_APP = ASGIMiddleware(ASGI_APP)
```

## Benchmark

Run `pytest ./benchmark.py -s` to compare the performance of `a2wsgi` and `uvicorn.middleware.wsgi.WSGIMiddleware` / `asgiref.wsgi.WsgiToAsgi`.

## Why a2wsgi

### Convert WSGI app to ASGI app

The uvicorn-WSGIMiddleware dealing with large file uploads, it is easy to cause insufficient memory [uvicorn/issue#371](https://github.com/encode/uvicorn/issues/371). a2wsgi uses `asyncio.run_coroutine_threadsafe` to regulate the pace of reading data, thus solving this problem.

### Convert ASGI app to WSGI app
There is a lot of support for WSGI. Converting ASGI to WSGI, you will be able to use many existing services to deploy ASGI applications.
