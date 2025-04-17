
# SOP: Managing a Poetry Project for Python

## 👤 **Author Information**
| **Author** | **Created on** | **Version**  | **Comment** | **Reviewer** |
|------------|----------------|--------------|-------------|--------------|
| **Prince Batra**   | **15-04-2025**   | **Version 1** | **Internal review** | **Siddharth Pawar** |

---

# 📘 Python Poetry Project Setup SOP

## 📖 Table of Contents    
- [📌 Introduction](#1-introduction)
- [🛠 Prerequisites](#2-prerequisites)
- [🧭 Step-by-Step Instructions](#2-step-by-step-instructions)  
  - [📍 Step 1: Install Python & pip](#-step-1-install-python--pip-if-not-already-installed)  
  - [📍 Step 2: Install Poetry](#-step-2-install-poetry)  
  - [📍 Step 3: Create a New Poetry Project](#-step-3-create-a-new-poetry-project)  
  - [📍 Step 4: Create & Activate Virtual Environment](#-step-4-create--activate-virtual-environment)  
  - [📍 Step 5: Add Dependencies](#-step-5-add-dependencies)  
  - [📍 Step 6: Create a Simple Python Script (`cartpy`)](#-step-6-create-a-simple-python-script-cartpy)  
  - [📍 Step 7: Run the Script Using Poetry](#-step-7-run-the-script-using-poetry-running-in-context)  

---
## 1. Introduction  
Poetry is a Python dependency manager and packaging tool that simplifies the process of managing libraries and virtual environments. It allows developers to easily add dependencies, configure virtual environments, and run commands within isolated environments.

---

## 2.Prerequisites  
- Python 3.x and pip installed on the system   

---

## 3. Step-by-Step Instructions  

### 📍 Step 1: Install Python & pip (If not already installed)

```bash
sudo apt update
sudo apt install python3 python3-pip -y
python3 --version
pip3 --version
```
This step ensures that Python 3 and pip are installed, which are required before installing Poetry.

### 📍 Step 2: Install Poetry

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

To make Poetry available in your terminal session, update your shell configuration:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
poetry --version
```

This installs Poetry and adds it to your system's PATH.

### 📍 Step 3: Create a New Poetry Project

```bash
poetry new my_project
cd my_project
```

This command will create a new project structure with:
- `pyproject.toml`: The file that manages dependencies.
- `my_project/`: Folder for your Python package.
- `tests/`: Folder for unit tests.

### 📍 Step 4: Create & Activate Virtual Environment

```bash
poetry env use python3
poetry env info
```

To manually activate the environment, run:

```bash
source $(poetry env info --path)/bin/activate
```

This step sets up a virtual environment isolated from your global Python environment.

### 📍 Step 5: Add Dependencies

```bash
poetry add requests pandas flask
```

This command will add requests, pandas, and flask to your project. The dependencies will appear in the pyproject.toml file under the [tool.poetry.dependencies] section:

```toml
[tool.poetry.dependencies]
requests = "^2.31.0"
pandas = "^2.2.1"
flask = "^2.3.0"
```

Poetry will also create or update the poetry.lock file to ensure the same package versions are used everywhere.

### 📍 Step 6: Create a Simple Python Script (`cart.py`)

```bash
nano cart.py
```

Paste the following code into the `cart.py` file:

```python
def calculate_total():
    cart = {
        "milk": 55,
        "bread": 40,
        "eggs": 75
    }
    total = sum(cart.values())
    print(f"Total grocery bill is: ₹{total}")

if __name__ == "__main__":
    calculate_total()
```

This script calculates the total cost of grocery items and prints the bill in Indian Rupees (₹).

### 📍 Step 7: Run the Script Using Poetry (Running in Context)

```bash
poetry run python cart.py
```

Expected output:

```bash
Total grocery bill is: ₹170
```

Running the script with `poetry run` ensures it uses the isolated virtual environment rather than your system's Python.

---

## 🔚 End of SOP

## 📬 **Contact Information**
| **Name** | **Email Address**        |
|----------|--------------------------|
| **Prince Batra**  | **prince.batra.snaatak@mygurukulam.co**   |
---
