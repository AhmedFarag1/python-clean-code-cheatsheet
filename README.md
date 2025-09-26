# 🧹 Clean Code Summary (Python)

## 📑 Table of Contents
- [Importance of Clean Code](#-importance-of-clean-code)
- [Naming Conventions](#naming-conventions)
- [Project Structure](#-project-structure)
- [Variables](#-variables)
- [Classes](#-classes)
  - [Single Responsibility Principle (SRP)](#1--single-responsibility-principle-srp)
  - [Open/Closed Principle (OCP)](#2--openclosed-principle-ocp)
  - [Liskov Substitution Principle (LSP)](#3--liskov-substitution-principle-lsp)
  - [Interface Segregation Principle (ISP)](#4--interface-segregation-principle-isp)
  - [Dependency Inversion Principle (DIP)](#5--dependency-inversion-principle-dip)

---

## 🔑 Importance of Clean Code
- Code should be **clear and readable** even after months.  
- Easy to **extend and modify** without breaking other parts.  
- Easier to **test** with unit tests.  
- Promotes **reusability** through proper abstractions.  
- Makes **team collaboration** smoother since everyone can understand it quickly.  

---

## ✍️ Naming Conventions

| Element          | Convention                   | Example                |
|------------------|------------------------------|------------------------|
| variable / func  | `lower_case_with_underscores` | `user_name`, `get_data()` |
| constant         | `UPPER_CASE_WITH_UNDERSCORES` | `PI = 3.14` |
| class            | `PascalCase`                 | `class UserProfile:` |
| module / file    | `lower_case_with_underscores` | `email_sender.py` |
| package          | `lowercase`                  | `models`, `utils` |
| private          | `_prefix`                    | `_validate()` |
| special method   | `__dunder__`                 | `__init__`, `__str__` |

---

## 🏗 Project Structure 

Example of a clean and scalable structure for AI API projects:  

```

project_name/
│
├── app/
│   ├── main.py            # entrypoint (FastAPI instance + routes include)
│   ├── api/
│   │   ├── endpoints/     # API endpoints (image, audio, text...)
│   │   │   ├── image.py
│   │   │   ├── audio.py
│   │   │   └── text.py
│   │   └── **init**.py
│   ├── core/              # core settings (config, logging, security)
│   │   ├── config.py
│   │   └── logger.py
│   ├── models/            # Pydantic models (request/response schemas)
│   ├── services/          # business logic (AI calls, ML models, utils)
│   └── utils/             # small helpers
│
├── tests/                 # unit/integration tests
│
├── requirements.txt       # Python dependencies
├── .env                   # environment variables (API keys, DB urls...)
├── README.md
└── Dockerfile / docker-compose.yml (optional)

```

### 🔄 Request Flow (FastAPI AI Endpoint)

```

Client Request
│
▼
[API Endpoint]  →  [Pydantic Model Validation]
│
▼
[Service Layer] → (AI / ML Logic e.g. Gemini, OpenAI, HuggingFace)
│
▼
[Response Model] → Returned to Client

````

---

## 🟢 Variables
- Use clear and descriptive names:  
```python
# ❌
n = 86400  

# ✅
SECONDS_IN_DAY = 60 * 60 * 24
````

* Use the same vocabulary for the same entity:

```python
# ❌
get_user_info(), get_client_data()  

# ✅
get_user_info(), get_user_data()
```

* Don’t repeat context in property names:

```python
# ❌
class Car:  
    car_color: str  

# ✅
class Car:  
    color: str
```

---

## 🟣 Classes

### 1- Single Responsibility Principle (SRP)

A Class should have only **one reason to change**.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
    
    def calculate_salary(self):
        return self.salary * 12

class ReportPrinter:
    def print_report(self, employee: Employee):
        print(f"{employee.name}: {employee.salary}")
```

---

### 2- Open/Closed Principle (OCP)

Classes should be **open for extension, closed for modification**.

```python
class Animal:
    def speak(self):
        raise NotImplementedError

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"
```

---

### 3- Liskov Substitution Principle (LSP)

Subclasses should be **replaceable** by their base class without breaking the code.

```python
class Bird: pass

class FlyingBird(Bird):
    def fly(self):
        return "Flying..."

class Penguin(Bird):
    def swim(self):
        return "Swimming..."
```

---

### 4- Interface Segregation Principle (ISP)

Don’t force classes to implement methods they don’t need.

```python
class Flyable:
    def fly(self): ...

class Swimmable:
    def swim(self): ...

class Duck(Flyable, Swimmable):
    def fly(self): return "Flying..."
    def swim(self): return "Swimming..."
```

---

### 5- Dependency Inversion Principle (DIP)

Depend on **abstractions**, not concrete implementations.

```python
class Storage:
    def save(self, data): 
        raise NotImplementedError

class FileStorage(Storage):
    def save(self, data):
        with open("file.txt", "w") as f:
            f.write(data)

def store_data(storage: Storage, data: str):
    storage.save(data)
```

---
