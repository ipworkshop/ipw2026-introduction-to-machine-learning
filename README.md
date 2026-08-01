# Machine Learning Course

Acest repository conține notebook-urile și exercițiile folosite în cadrul cursului de Machine Learning.

## Ce trebuie instalat înainte

Înainte de a descărca proiectul, asigură-te că ai instalat:

- **Python 3.10 sau o versiune mai nouă**
- **Git**
- unul dintre următoarele editoare:
  - **Visual Studio Code**
  - **PyCharm**

Pentru a verifica dacă Python și Git sunt instalate, deschide un terminal și rulează:

```bash
python --version
git --version
```

Pe Linux sau macOS, Python poate fi disponibil prin comanda:

```bash
python3 --version
```

Pe Windows, poate fi disponibil prin:

```powershell
py --version
```

## 1. Descarcă proiectul

Deschide un terminal în folderul în care dorești să salvezi proiectul și rulează:

```bash
git clone <REPOSITORY_URL>
```

Intră apoi în folderul proiectului:

```bash
cd <REPOSITORY_FOLDER>
```

Toate comenzile următoare trebuie rulate din acest folder.

## 2. Creează mediul virtual

Mediul virtual păstrează separat dependențele necesare cursului.

### Linux / macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### Windows PowerShell

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

După activare, terminalul ar trebui să afișeze `(.venv)` înaintea comenzii.

Exemplu:

```text
(.venv) user@computer:~/machine-learning-course$
```

## 3. Instalează dependințele

Cu mediul virtual activat, rulează:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Dependențele proiectului sunt definite în fișierul:

```text
requirements.txt
```

## 4. Deschide proiectul

### Visual Studio Code

Instalează extensiile:

- **Python**
- **Jupyter**

Deschide apoi folderul proiectului în VS Code.

Deschide notebook-ul:

```text
notebooks/01_python_numpy.ipynb
```

În partea de sus a notebook-ului:

1. apasă **Select Kernel**;
2. selectează **Python Environments**;
3. alege interpreterul din folderul `.venv`.

Pe Linux și macOS:

```text
.venv/bin/python
```

Pe Windows:

```text
.venv\Scripts\python.exe
```

### PyCharm

Deschide folderul proiectului în PyCharm.

Configurează interpreterul din:

```text
Settings -> Project -> Python Interpreter
```

Selectează un interpreter existent și alege:

Pe Linux și macOS:

```text
.venv/bin/python
```

Pe Windows:

```text
.venv\Scripts\python.exe
```

Deschide apoi notebook-ul:

```text
notebooks/01_python_numpy.ipynb
```

Rulează celulele în ordine, de sus în jos.

### Google Colab

Google Colab permite rularea notebook-urilor direct în browser, fără instalarea locală a Python sau a unui editor.

Pentru a deschide notebook-ul:

1. intră pe Google Colab;
2. selectează **File -> Open notebook**;
3. deschide tab-ul **GitHub**;
4. introdu URL-ul repository-ului;
5. selectează notebook-ul dorit, de exemplu:

```text
notebooks/01_python_numpy.ipynb
```

După deschidere, creează o copie personală folosind:

`File -> Save a copy in Drive`

Lucrează în copia salvată în Google Drive, astfel încât modificările și rezolvările să fie păstrate.