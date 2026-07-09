THEORY: WHY FASTAPI IS USED

1. What FastAPI is
   FastAPI is a Python web framework specifically built for creating
   APIs (backend endpoints that return data, usually JSON) rather than
   full server-rendered websites. It sits on top of two lower-level
   libraries:
   - Starlette — handles the actual async web server mechanics
     (routing, middleware, WebSockets)
   - Pydantic — handles data validation and serialization using
     Python type hints

2. Why "Fast" — performance angle
   - It's built on ASGI (Asynchronous Server Gateway Interface) instead
     of the older WSGI standard that Flask/Django traditionally used.
     ASGI allows asynchronous request handling — the server can start
     handling a second request while waiting on I/O (database calls,
     external API calls) for the first, instead of blocking.
   - Because Starlette's async core is thin and close to the metal,
     FastAPI benchmarks close to Node.js and Go frameworks — unusually
     fast for a Python framework, where async isn't the default.

3. Why "Fast" — developer speed angle
   - FastAPI uses standard Python type hints (e.g. `name: str`,
     `age: int`) to do double duty: they define your function
     signature AND automatically generate request validation,
     serialization, and documentation. You don't write validation
     logic separately — the types ARE the validation.
   - This is why it's called "fast to code" — a working, validated,
     documented API endpoint often takes just a few lines.

4. Automatic interactive documentation
   - Because endpoints are defined with typed Pydantic models, FastAPI
     can introspect them and auto-generate an OpenAPI (Swagger) schema
     at runtime.
   - This produces a live, interactive docs page (usually at /docs)
     where you can test endpoints directly in the browser — with zero
     extra code from the developer. This is a major reason teams pick
     it over Flask, which requires manual doc generation (e.g. via
     separate libraries like flask-swagger).

5. Why it fits data science / ML teams particularly well
   - Since most ML/data teams are already writing Python (numpy,
     pandas, PyTorch, scikit-learn), FastAPI lets them expose a model
     or pipeline as a web API without switching languages or learning
     a separate backend stack.
   - Type-hint-based validation catches malformed input data early —
     useful when the "backend logic" is really a model inference call
     that expects clean, typed input.

6. Why it displaced Flask for many new projects
   - Flask is WSGI-based (synchronous by default), older, and requires
     more manual wiring for validation, docs, and async support.
   - FastAPI essentially took what people liked about Flask's
     simplicity, added modern Python type hints, native async, and
     auto-docs — covering three separate concerns Flask needed extra
     libraries for.

7. Trade-off it accepts
   - It relies heavily on Python's type-hinting system, so teams that
     don't already write typed Python (or resist adopting it) get less
     benefit and more friction.
   - Its async model gives the biggest wins for I/O-bound work
     (database/network calls). For CPU-bound work (heavy computation
     inside a request), async alone doesn't help — you still need
     background workers or multiprocessing, same as any Python
     framework.