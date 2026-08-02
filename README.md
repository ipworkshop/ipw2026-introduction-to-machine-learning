# Machine Learning Course

Acest repository conține notebook-urile, dataset-urile și exercițiile folosite în cadrul cursului de Machine Learning.

Platforma principală de lucru este **Google Colab**.

# Sesiuni

## Ziua 1 

### Sesiunea 1 - Fundamentele Python și NumPy

[Deschide notebook-ul în Google Colab](https://colab.research.google.com/github/ipworkshop/ipw2026-introduction-to-machine-learning/blob/main/notebooks/01_python_numpy.ipynb)

### Sesiunea 2 - Manipularea datelor și Train/Test Split

[Deschide notebook-ul în Google Colab](https://colab.research.google.com/github/ipworkshop/ipw2026-introduction-to-machine-learning/blob/main/notebooks/02_pandas_train_test.ipynb)

## Ziua 3

### Sesiunea 6 - Probabilități, Legea lui Bayes și Naive Bayes

[Deschide notebook-ul în Google Colab](https://colab.research.google.com/github/ipworkshop/ipw2026-introduction-to-machine-learning/blob/main/notebooks/06_probabillities_bayes_naive_bayes.ipynb)

## Cum lucrezi în Google Colab

După deschiderea notebook-ului:

1. selectează `File -> Save a copy in Drive`;
2. lucrează în copia salvată în Google Drive;
3. rulează celulele în ordine, de sus în jos;
4. completează exercițiile marcate cu `TODO`;
5. înlocuiește valorile `...` din exerciții;
6. rulează celulele de verificare bazate pe `assert`.

Notebook-urile și dataset-urile necesare sunt încărcate direct din repository.

## Lucrul local - opțional

Poți lucra și local folosind Visual Studio Code sau PyCharm.

### 1. Ce trebuie instalat

Asigură-te că ai instalat:

- Python 3.10 sau o versiune mai nouă;
- Git;
- Visual Studio Code sau PyCharm.

Pentru a verifica dacă Python și Git sunt instalate, deschide un terminal și rulează:

```bash
python --version
git --version
```

Pe Linux sau macOS, Python poate fi disponibil prin:

```bash
python3 --version
```

Pe Windows, poate fi disponibil prin:

```powershell
py --version
```

### 2. Descarcă proiectul

Deschide un terminal în folderul în care dorești să salvezi proiectul și rulează:

```bash
git clone https://github.com/ipworkshop/ipw2026-introduction-to-machine-learning.git
```

Intră apoi în folderul proiectului:

```bash
cd ipw2026-introduction-to-machine-learning
```

Toate comenzile următoare trebuie rulate din acest folder.

### 3. Creează mediul virtual

Mediul virtual păstrează separat dependențele necesare cursului.

#### Linux / macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

#### Windows PowerShell

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

După activare, terminalul ar trebui să afișeze `(.venv)` înaintea comenzii.

Exemplu:

```text
(.venv) user@computer:~/ipw2026-introduction-to-machine-learning$
```

### 4. Instalează dependențele

Cu mediul virtual activat, rulează:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Dependențele proiectului sunt definite în:

```text
requirements.txt
```

### 5. Visual Studio Code

Instalează extensiile:

- Python;
- Jupyter.

Deschide folderul proiectului în Visual Studio Code.

Deschide notebook-ul dorit, de exemplu:

```text
notebooks/01_python_numpy.ipynb
```

În partea de sus a notebook-ului:

1. apasă `Select Kernel`;
2. selectează `Python Environments`;
3. alege interpreterul din folderul `.venv`.

Pe Linux și macOS:

```text
.venv/bin/python
```

Pe Windows:

```text
.venv\Scripts\python.exe
```

### 6. PyCharm

Deschide folderul proiectului în PyCharm.

Configurează interpreterul din:

```text
Settings -> Project -> Python Interpreter
```

Selectează interpreterul existent din mediul `.venv`.

Pe Linux și macOS:

```text
.venv/bin/python
```

Pe Windows:

```text
.venv\Scripts\python.exe
```

Deschide apoi notebook-ul dorit și rulează celulele în ordine, de sus în jos.

## Open Source

Acest proiect este open source și poate fi folosit, modificat și distribuit în scop educațional.

Copyright © 2026 IP Workshop.
