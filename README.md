# Machine Learning Course

Acest repository conține notebook-urile, dataset-urile și exercițiile folosite în cadrul cursului de Machine Learning.

Platforma principală de lucru este **Google Colab**.

Lucrul local în Visual Studio Code sau PyCharm este opțional.

## Google Colab

### 1. Deschide notebook-ul din GitHub

1. Intră pe Google Colab.
2. Selectează `File -> Open notebook`.
3. Deschide tab-ul `GitHub`.
4. Introdu URL-ul repository-ului.
5. Selectează notebook-ul dorit.

De exemplu:

```text
notebooks/01_python_numpy.ipynb
```

sau:

```text
notebooks/02_pandas_train_test.ipynb
```

După deschiderea notebook-ului, creează o copie personală folosind:

```text
File -> Save a copy in Drive
```

Lucrează în copia salvată în Google Drive, astfel încât modificările și rezolvările să fie păstrate.

### 2. Folosește fișierele necesare notebook-ului

Unele notebook-uri folosesc fișiere externe, cum ar fi dataset-uri CSV.

De exemplu:

```text
data/students.csv
```

Ai două variante.

#### Varianta A: încarcă manual fișierele

În partea stângă a interfeței Colab:

1. deschide secțiunea `Files`;
2. apasă `Upload`;
3. selectează fișierul necesar de pe calculator.

De exemplu, pentru sesiunea 2 poți încărca:

```text
students.csv
```

După încărcare, fișierul poate fi citit cu:

```python
import pandas as pd

df = pd.read_csv("students.csv")
```

Fișierele încărcate manual sunt disponibile doar în sesiunea Colab curentă. Dacă sesiunea este resetată, poate fi necesar să le încarci din nou.

#### Varianta B: clonează repository-ul

Poți descărca întregul repository direct în Colab.

Rulează într-o celulă:

```python
!git clone <REPOSITORY_URL>
```

Intră apoi în folderul repository-ului:

```python
%cd <REPOSITORY_FOLDER>
```

După clonare, vei avea acces la întreaga structură a proiectului:

```text
notebooks/
data/
requirements.txt
README.md
```

De exemplu, dataset-ul poate fi încărcat cu:

```python
import pandas as pd

df = pd.read_csv("data/students.csv")
```

### 3. Instalează dependențele, dacă este necesar

După clonarea repository-ului și intrarea în folderul proiectului, poți instala dependențele cu:

```python
!pip install -r requirements.txt
```

### 4. Rulează notebook-ul

Rulează celulele în ordine, de sus în jos.

Pentru a rula o celulă:

- apasă butonul din stânga celulei;
- sau folosește combinația `Shift + Enter`.

Notebook-urile conțin:

- explicații;
- exemple;
- exerciții marcate cu `TODO`;
- celule de verificare bazate pe `assert`.

Înlocuiește valorile `...` din exerciții și rulează celulele de verificare pentru a confirma că rezolvarea este corectă.

## Lucrul local - opțional

Poți lucra și local folosind Visual Studio Code sau PyCharm.

## 1. Ce trebuie instalat

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

## 2. Descarcă proiectul

Deschide un terminal în folderul în care dorești să salvezi proiectul și rulează:

```bash
git clone <REPOSITORY_URL>
```

Intră apoi în folderul proiectului:

```bash
cd <REPOSITORY_FOLDER>
```

Toate comenzile următoare trebuie rulate din acest folder.

## 3. Creează mediul virtual

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

## 4. Instalează dependențele

Cu mediul virtual activat, rulează:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Dependențele proiectului sunt definite în:

```text
requirements.txt
```

## 5. Visual Studio Code

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

## 6. PyCharm

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
