import pypandoc, os
content = r"""# PROJECT ORION — Pre-Development Learning Roadmap

**Purpose:** Prepare for building ORION by understanding the technologies and concepts before writing the application.

**Study target:** Approximately **10.5 hours**.

> ORION's first goal is to build an AI-powered application that sends prompts to Google's Gemini model through its API and receives generated responses. We are using an existing AI model; we are **not training our own model**.

---

## 1. What we're building

At the beginning, ORION will be a small Python application that communicates with Gemini. We will then expose the functionality through FastAPI. 

```text
User
  |
  v
ORION application (Python)
  |
  v
Gemini API
  |
  v
Gemini model
  |
  v
Generated response
  |
  v
ORION receives and displays the response
```

The initial scope is deliberately small:

1. Set up the project and Python environment.
2. Connect Python to Gemini.
3. Send a prompt.
4. Receive and display the response.
5. Expose the functionality through a FastAPI endpoint.

The visual interface and ASCII-art visualizer are separate future work. They are not prerequisites for the first AI integration.

---

## 2. Learning roadmap

### Module 1 — Python fundamentals revision (2 hours)

Revise these concepts:

| Concept | What to understand |
|---|---|
| Variables and data types | Strings, integers, floats and booleans |
| Lists | Ordered collections of values |
| Dictionaries | Key-value data structures |
| Functions | Reusable blocks of code |
| Parameters and arguments | Passing data into functions |
| `return` | Returning a result from a function |
| Loops | Repeating operations |
| Conditionals | Making decisions with `if`, `elif` and `else` |
| Exceptions | Handling errors with `try` and `except` |
| Modules | Organising code into separate files |
| Imports | Reusing code from modules and packages |
| File handling | Reading and writing files |

**Prioritise:** functions, dictionaries, exceptions, modules and imports.

Why it matters: API responses are structured data, and ORION will need to process them and handle failures.

**Practice:** Write a function that accepts a dictionary, extracts a value safely, and handles a missing key.

### Module 2 — Object-oriented programming (1 hour)

Understand the basics:

- Classes and objects
- Constructors (`__init__`)
- Attributes
- Methods
- Encapsulation
- Basic inheritance

You do not need to become an OOP expert yet. Learn how objects group data and behaviour, and recognise objects returned by Python SDKs.

**Practice:** Create a small `User` class with a constructor, a couple of attributes and a method.

### Module 3 — HTTP, APIs and JSON (2 hours)

This is one of the most important modules.

#### A. APIs

Understand what an Application Programming Interface is and how it allows software systems to communicate.

Know the difference between:
- An API provider
- An API consumer/client
- An endpoint
- A request
- A response

#### B. HTTP methods

| Method | Common purpose |
|---|---|
| GET | Retrieve information |
| POST | Send information or request an operation |
| PUT | Replace a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |

#### C. HTTP status codes

Learn what these mean:

| Code | Meaning |
|---|---|
| 200 | OK / successful request |
| 201 | Created |
| 400 | Bad request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not found |
| 429 | Too many requests / rate limited |
| 500 | Internal server error |

#### D. JSON

Learn:
- Objects and key-value pairs
- Arrays
- Nested objects
- Strings, numbers, booleans and `null`
- Serialization and deserialization

Example:

```json
{
  "user": "Nani",
  "message": "Explain Python APIs",
  "role": "student"
}
```

#### E. Request and response details

Understand:
- Client and server
- Request URL and endpoint
- Headers
- Request body
- Response body
- Authentication
- API keys

**Practice:** Write a small JSON object, parse it in Python, change a value and serialise it again.

### Module 4 — Python networking and API communication (1 hour)

Learn the basic flow of making an HTTP request from Python.

Topics:
- HTTP requests and responses
- The `requests` library
- GET and POST requests
- Sending JSON
- Reading JSON responses
- Request headers
- Connection errors and timeouts
- API authentication

You do not need to master computer networking. You should understand what happens when Python sends a request to another server and receives a response.

**Practice:** If you have access to a safe public test API, send one GET request and inspect its status code and JSON response. Do not put private keys in the exercise.

### Module 5 — FastAPI (1.5 hours)

FastAPI will expose ORION functionality through HTTP endpoints.

Learn:

| Concept | Purpose |
|---|---|
| FastAPI | Python web framework for building APIs |
| Route / endpoint | A URL and method handled by the application |
| GET | Retrieve information |
| POST | Accept data or trigger an operation |
| Path parameter | A value included in the URL path |
| Query parameter | An optional value in the URL query string |
| Request body | Data sent by the client |
| Pydantic | Data validation and parsing |
| Uvicorn | ASGI server used to run the application |
| Swagger UI | Interactive API documentation |

Understand the difference between FastAPI (the framework) and Uvicorn (the server that runs the ASGI application).

Basic request flow:

```text
Client
  |
  | HTTP request
  v
FastAPI route
  |
  v
Python application logic
  |
  v
HTTP response
  |
  v
Client
```

**Practice:** Make a tiny FastAPI app with a GET route that returns a JSON message. Then make a POST route that accepts a simple Pydantic model.

### Module 6 — Gemini API and AI fundamentals (2 hours)

You do not need machine-learning expertise to use a hosted LLM API. You do need to understand the basic vocabulary and request flow.

#### A. LLM fundamentals

Learn what these terms mean:

1. Large Language Model (LLM)
2. Transformer — high-level purpose, not the maths
3. Token
4. Context window
5. System instruction
6. User prompt
7. Model response
8. Temperature
9. Hallucination

You do not need to derive transformer equations or train a neural network.

#### B. Gemini API

Understand:
- What the Gemini API provides
- What an API key is used for
- How to select a model
- How a prompt is sent
- How generated content is returned
- How to handle API errors
- Rate limits and quotas
- Token usage and possible billing

#### C. Conversation history

A model does not automatically know every previous message in a separate API call. An application commonly sends relevant conversation history along with the latest user message.

Example:

```text
USER: What is Python?
ORION: Python is a programming language.
USER: Who created it?
```

For the follow-up to make sense, ORION needs to provide the relevant earlier context to the model.

Learn:
- Message roles
- Multi-turn conversations
- Conversation history
- Context management

We can implement conversation history later. For the first integration, a single prompt and response is enough.

### Module 7 — Environment variables and security (30 minutes)

Learn:
- What environment variables are
- What a `.env` file is
- What an API key does
- Why secrets must not be committed to Git
- What `.gitignore` does

Do not hardcode a real API key in source code or put it in frontend JavaScript. Keep it outside the repository and load it through environment configuration.

Example `.gitignore` entries:

```gitignore
.env
.venv/
__pycache__/
```

Never share the actual API key in screenshots, public repositories or chat messages. If a key is accidentally exposed, revoke it and create a replacement.

---

## 3. Study schedule

| Subject | Time | Priority |
|---|---:|---|
| Python fundamentals revision | 2 hours | High |
| OOP basics | 1 hour | Medium |
| HTTP, APIs and JSON | 2 hours | Very high |
| Python networking | 1 hour | High |
| FastAPI | 1.5 hours | Very high |
| Gemini and LLM fundamentals | 2 hours | Very high |
| Environment variables and security | 30 minutes | High |
| Revision | 30 minutes | High |
| **Total** | **10.5 hours** | |

This is a focused introduction, not a claim that every topic can be mastered in one sitting. Spend extra time on anything you cannot explain or practise.

---

## 4. What NOT to study yet

These technologies are useful in other projects, but they are not prerequisites for ORION's first Gemini API integration.

| Technology / topic | For now |
|---|---|
| PyTorch | Not required |
| TensorFlow | Not required |
| Neural-network training | Not required |
| NumPy | Not required |
| Pandas | Not required |
| Scikit-learn | Not required |
| Advanced mathematics | Not required |
| CUDA | Not required |
| Docker | Later, if needed |
| PostgreSQL | Later, if we add persistent storage |
| Redis | Later, if a real use case appears |
| React | Not required for the initial Python integration |
| Machine-learning algorithms | Not required |

Important distinction: ORION will initially **use** a hosted AI model through an API. It will not train or fine-tune a model.

---

## 5. Readiness checklist

Before implementation, try to explain these in your own words without copying definitions:

- [ ] What is an API?
- [ ] What happens when an HTTP POST request is sent?
- [ ] What is JSON?
- [ ] What is the difference between a client and a server?
- [ ] What does an API key do?
- [ ] What is an endpoint?
- [ ] What is FastAPI?
- [ ] What does Uvicorn do?
- [ ] What is Pydantic?
- [ ] What is an LLM?
- [ ] What are tokens?
- [ ] What is a context window?
- [ ] At a high level, how does Gemini return a response?
- [ ] What is conversation history?
- [ ] What do common HTTP status codes mean?
- [ ] Why must API keys remain private?

You do not need perfect textbook definitions. You need to understand the concepts well enough to follow the code and debug basic problems.

---

## 6. Learning resources

Prefer official documentation and short experiments over passively watching long tutorial playlists.

1. [Python Official Tutorial](https://docs.python.org/3/tutorial/)
2. [Python Classes](https://docs.python.org/3/tutorial/classes.html)
3. [MDN: HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
4. [MDN: Working with JSON](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON)
5. [FastAPI Tutorial](https://fastapi.tiangolo.com/tutorial/)
6. [Gemini API Documentation](https://ai.google.dev/gemini-api/docs)
7. [Google Gen AI Python SDK](https://googleapis.github.io/python-genai/)

Documentation can change, so use the current official Gemini SDK examples when we begin implementation.

---

## 7. How to study each topic

For every concept:

1. Understand what it is.
2. Understand why it exists.
3. Write a small example yourself.
4. Change the example and predict what will happen.
5. Run it and observe the result.
6. Explain the result in your own words.

Do not aim to memorise every method or parameter. Learn how to read documentation and identify what a piece of code is doing.

### The standard for ORION

When we eventually use an SDK call such as:

```python
response = client.models.generate_content(
    model="MODEL_NAME",
    contents="Explain APIs"
)
```

The goal is to understand:
- What `client` represents
- What the SDK method does
- What the `model` argument selects
- What `contents` sends
- What `response` contains
- What errors might occur

We should not add a library or architectural layer unless we understand why ORION needs it.

---

## 8. First implementation milestone

After the preparation, build this in small steps:

**Milestone 1:** Python can communicate with Gemini and print a generated response.

**Milestone 2:** Put the AI request behind a FastAPI endpoint.

**Milestone 3:** Test the endpoint by sending a prompt and inspecting the JSON response.

Conversation history, storage, a desktop interface, ASCII visuals and other features can come later.

**Core principle: Build ORION one understandable layer at a time.**
"""
out = "/mnt/data/ORION_Pre_Development_Roadmap.md"
pypandoc.convert_text(content, "md", format="md", outputfile=out, extra_args=["--standalone"])
print(out, os.path.getsize(out))
#   P R O J E C T - O R I O N  
 