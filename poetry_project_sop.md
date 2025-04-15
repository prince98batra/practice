# SOP: Managing a Poetry Project for Python

**Owner**: Prince Batra  
**Team**: Development Team  
**Date Created**: 15-Apr-2025  
**Last Updated**: 15-Apr-2025  

---

## 📦 Stack Details  
**Component**: Poetry (Python Dependency Manager)  
**OS/Platform**: Ubuntu 22.04 LTS  

---

## 🎯 Purpose  
This SOP provides detailed instructions on setting up a Poetry project for managing Python dependencies and virtual environments. It ensures a smooth workflow for Python project development.

---

## 🛠 Prerequisites  
- Python 3.x and pip installed on the system  

---

## 1. Introduction  
Poetry is a tool that helps manage Python packages and virtual environments easily. It keeps dependencies organized and ensures consistent environments across teams.

---

## 2. Step-by-Step Instructions  

### 📍 Step 1: Install Python & pip (If not already installed)

\`\`\`bash
sudo apt update
sudo apt install python3 python3-pip -y
python3 --version
pip3 --version
\`\`\`

These commands ensure your system has the latest Python version and pip (Python package installer) installed.

---

### 📍 Step 2: Install Poetry

\`\`\`bash
curl -sSL https://install.python-poetry.org | python3 -
\`\`\`

This command downloads and runs the official Poetry installation script.

Update your shell configuration:

\`\`\`bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
poetry --version
\`\`\`

This ensures that Poetry is added to your terminal path and accessible globally from the terminal.

---

### 📍 Step 3: Create a New Poetry Project

\`\`\`bash
poetry new my_project
cd my_project
\`\`\`

Creates a standard Python project folder with all the required files and structure. The `cd` command takes you inside the project directory.

---

### 📍 Step 4: Create & Activate Virtual Environment

\`\`\`bash
poetry env use python3
poetry env info
\`\`\`

This sets up a dedicated environment just for this project. It keeps your global Python setup clean.

To manually activate:

\`\`\`bash
source $(poetry env info --path)/bin/activate
\`\`\`

This is helpful if you want to work inside the environment like a normal Python virtualenv.

---

### 📍 Step 5: Add Dependencies

\`\`\`bash
poetry add requests pandas flask
\`\`\`

Installs these libraries locally for the project and adds them to the `pyproject.toml` file automatically.

Check `pyproject.toml`:

\`\`\`toml
[tool.poetry.dependencies]
requests = "^2.31.0"
pandas = "^2.2.1"
flask = "^2.3.0"
\`\`\`

This is where Poetry tracks what libraries your project depends on.

---

### 📍 Step 6: Create a Simple Real-life Python Script 

\`\`\`bash
nano cart.py
\`\`\`

Use `nano` (or any editor) to create a Python file.

Paste the following code:

\`\`\`python
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
\`\`\`

This is a small script that calculates a total bill using predefined values — great for basic understanding and testing the setup.

---

### 📍 Step 7: Run the Script Using Poetry (Running in Context)

\`\`\`bash
poetry run python cart.py
\`\`\`

This runs your script **inside the virtual environment** managed by Poetry. This way, all dependencies used come from your isolated environment, not the system-wide Python.

Expected output:

\`\`\`
Total grocery bill is: ₹170
\`\`\`

---

## 🔚 End of SOP

| Date       | Author        | Change Description         |
|------------|---------------|----------------------------|
| 15-Apr-25  | Prince Batra  | Initial draft |