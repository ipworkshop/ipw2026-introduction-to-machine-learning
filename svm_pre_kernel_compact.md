
## Contextul folosit pe tot parcursul

Datasetul `students.csv` conține informații precum:

- `hours_studied`;
- `exercises_solved`;
- `attendance`;
- `previous_score`;
- `test_score`.

Pentru explicația de la tablă folosim doar două features:

$$
x_1=\text{hours\_studied}
$$

$$
x_2=\text{exercises\_solved}
$$

Fiecare student devine un punct:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

Definim didactic două clase:

$$
y=
\begin{cases}
+1, & \text{dacă test\_score}\geq70\\
-1, & \text{dacă test\_score}<70
\end{cases}
$$

> Pragul de 70 este doar o convenție pentru exemplul de curs.

![[students_feature_space.png]]

---

# 1. De la tabel la clasificare

## Întrebarea de pornire

> „Dacă vine un student nou și știm câte ore a studiat și câte exerciții a rezolvat, putem estima dacă va promova?”

Pe grafic:

- fiecare student este un punct;
- culoarea arată clasa;
- modelul trebuie să împartă planul în două regiuni.

Limita dintre cele două regiuni se numește **frontieră de decizie**.

### Ce trebuie să rămână

> Clasificarea poate fi privită ca împărțirea spațiului features-urilor în regiuni asociate unor clase.

### Tranziție

> „Noi putem desena intuitiv o linie între clase. Calculatorul are însă nevoie de o regulă numerică precisă.”

---

# 2. Regula liniară de decizie

Pentru două features, modelul calculează un scor:

$$
f(x)=w_1x_1+w_2x_2+b
$$

Compact:

$$
f(x)=w^Tx+b
$$

## Traducerea simbolurilor

- \(x_1\): orele studiate;
- \(x_2\): exercițiile rezolvate;
- \(w_1\): cât contribuie primul feature;
- \(w_2\): cât contribuie al doilea feature;
- \(b\): ajustarea pragului;
- \(f(x)\): scorul final al studentului.

Termenul:

$$
w^Tx
$$

este doar suma ponderată:

$$
w^Tx=w_1x_1+w_2x_2
$$

## Exemplu

Presupunem:

$$
f(x)=2x_1+x_2-10
$$

Pentru studentul:

$$
x=
\begin{bmatrix}
4\\
5
\end{bmatrix}
$$

obținem:

$$
f(x)=2\cdot4+5-10=3
$$

Scorul este pozitiv.

Pentru:

$$
x=
\begin{bmatrix}
2\\
3
\end{bmatrix}
$$

obținem:

$$
f(x)=2\cdot2+3-10=-3
$$

Scorul este negativ.

## Regula de clasificare

$$
\hat y=
\begin{cases}
+1,&f(x)>0\\
-1,&f(x)<0
\end{cases}
$$

> Scorul nu este probabilitate. Semnul lui ne spune doar partea în care se află punctul.

În notebook, aceeași idee apare prin:

```python
model.decision_function(...)
```

### Tranziție

> „Dacă un scor pozitiv înseamnă o parte și unul negativ cealaltă, ce reprezintă punctele pentru care scorul este exact zero?”

---

# 3. Frontiera de deciziem

Frontiera este formată din toate punctele pentru care:

$$
f(x)=0
$$

adică:

$$
w^Tx+b=0
$$

În exemplul nostru:

$$
2x_1+x_2-10=0
$$

Aceasta este o dreaptă.

![[Pasted image 20260806210041.png]]

## Cum o desenăm simplu

Dacă:

$$
x_1=0
$$

atunci:

$$
x_2=10
$$

Dacă:

$$
x_2=0
$$

atunci:

$$
x_1=5
$$

Dreapta trece prin:

$$
(0,10)
\quad\text{și}\quad
(5,0)
$$

## Rolul lui \(w\)

$$
w=
\begin{bmatrix}
w_1\\
w_2
\end{bmatrix}
$$

Vectorul \(w\):

- conține ponderile features-urilor;
- controlează orientarea frontierei;
- indică direcția în care scorul crește;
- este perpendicular pe frontieră.

Intuiția practică:

> De-a lungul frontierei, scorul rămâne zero.  
> Când traversăm frontiera în direcția lui \(w\), scorul trece de la negativ la pozitiv.


## Rolul lui \(b\)

\(b\) controlează poziția liniei.

Pentru:

$$
2x_1+x_2-10=0
$$

avem:

$$
x_2=-2x_1+10
$$

Dacă schimbăm numai \(b\):

$$
2x_1+x_2-14=0
$$

obținem:

$$
x_2=-2x_1+14
$$

Panta rămâne aceeași, deci linia se mută paralel fără să se rotească.

### Imaginea intuitivă

> \(w\) controlează orientarea frontierei, iar \(b\) controlează poziția ei.

### Tranziție

> „Am găsit o linie care separă clasele. Problema este că pot exista mai multe linii care clasifică perfect aceleași puncte. Pe care o alegem?”

---

# 4. De ce nu alegem orice frontieră?

Desenăm mai multe linii care separă corect aceleași două clase.

Unele trec foarte aproape de puncte.

Altele lasă mai mult spațiu între ele și clase.

Toate pot avea accuracy perfect pe train, dar nu sunt la fel de optimizate.

Un student nou poate avea:

- o oră în plus sau în minus;
- câteva exerciții în plus sau în minus;
- zgomot în date;
- un comportament diferit de exemplele existente.

Dacă frontiera este lipită de puncte, o variație mică poate schimba imediat predicția.

### Ce face SVM

> Nu vrem doar o linie care trece printre clase.  
> Vrem linia care lasă cel mai mare spațiu de siguranță.

Acest spațiu se numește **margine**.

### Tranziție

> „Ca să comparăm două frontiere, trebuie mai întâi să putem măsura cât de aproape este un punct de fiecare dintre ele.”

---

# 5. Distanța față de frontieră

Scorul brut este:

$$
w^Tx+b
$$

Un scor apropiat de zero sugerează un punct apropiat de frontieră.

Dar scorul nu este încă o distanță geometrică.

## De ce?

Aceeași frontieră poate fi scrisă:

$$
2x_1+x_2-10=0
$$

sau:

$$
20x_1+10x_2-100=0
$$

Este aceeași linie, dar scorurile produse de a doua ecuație sunt de zece ori mai mari.

Prin urmare, trebuie să eliminăm efectul scalei ecuației.

## Formula distanței

$$
\text{distanță}
=
\frac{|w^Tx+b|}{\lVert w\rVert}
$$

unde:

$$
\lVert w\rVert
=
\sqrt{w_1^2+w_2^2}
$$

## Cum explic formula

- \(w^Tx+b\) spune cât de departe este scorul de zero;
- valoarea absolută elimină partea pozitivă sau negativă;
- împărțirea la \(\lVert w\rVert\) corectează scala ecuației.

Am stabilit că \(w\) este perpendicular pe frontieră.

Cea mai scurtă distanță până la o linie se măsoară tot perpendicular, deci exact în direcția lui \(w\).

> **Atenție:** aici normalizăm ecuația frontierei, nu coloanele datasetului.

### Tranziție

> „Acum putem măsura distanța fiecărui student până la frontieră. Cum folosim aceste distanțe pentru a alege cea mai sigură frontieră?”

---

# 6. Marginea SVM

Pentru o frontieră dată, calculăm distanța fiecărui punct până la ea.

Exemplu:

- Studentul A: distanța \(4\);
- Studentul B: distanța \(2\);
- Studentul C: distanța \(0.5\).

Spațiul de siguranță este limitat de studentul cel mai apropiat:

$$
\min(4,2,0.5)=0.5
$$

SVM compară mai multe frontiere și o preferă pe aceea pentru care punctul cel mai apropiat este cât mai departe.

Formulat schematic:

$$
\max_{\text{frontiere care separă clasele}}
\min_i
\frac{|w^Tx_i+b|}{\lVert w\rVert}
$$

Formula se citește astfel:

1. calculăm distanțele;
2. alegem punctul cel mai apropiat;
3. alegem frontiera pentru care acea distanță este cea mai mare.

### Analogia coridorului

Frontiera este centrul unui coridor între cele două clase.

Extindem coridorul până când laturile sale ating primele puncte.

Punctele atinse limitează lățimea coridorului.

---

## Cele trei linii

Pentru reprezentarea standard SVM folosim:

$$
w^Tx+b=1
$$

$$
w^Tx+b=0
$$

$$
w^Tx+b=-1
$$

Interpretare:

- \(0\): frontiera de decizie;
- \(+1\): limita pozitivă a marginii;
- \(-1\): limita negativă a marginii.

![[Pasted image 20260806215454.png]]

Toate sunt paralele deoarece au același vector \(w\).

Se schimbă doar scorul constant.

Valorile \(+1\) și \(-1\) sunt o convenție de scalare care simplifică formulele.

---

## Lățimea marginii

Distanța de la linia \(0\) la linia \(+1\) este:

$$
\frac{|1-0|}{\lVert w\rVert}
=
\frac{1}{\lVert w\rVert}
$$

Distanța de la linia \(0\) la linia \(-1\) este tot:

$$
\frac{1}{\lVert w\rVert}
$$

Prin urmare, marginea completă este:

$$
\boxed{
\text{margine}
=
\frac{2}{\lVert w\rVert}
}
$$

## Ce vrea să optimizeze SVM

Vrem o margine cât mai mare:

$$
\max
\frac{2}{\lVert w\rVert}
$$

Cum \(2\) este constant, maximizarea fracției este echivalentă cu minimizarea numitorului:

$$
\min
\lVert w\rVert
$$

În practică se folosește forma:

$$
\boxed{
\min
\frac{1}{2}\lVert w\rVert^2
}
$$

Pătratul elimină radicalul, iar factorul \(\frac12\) simplifică optimizarea.

Nu este necesară derivarea în varianta principală.

### Ideea care trebuie să rămână

> Normă mică pentru \(w\) înseamnă margine mare.

### Tranziție

> „Până acum presupunem că putem construi un coridor complet liber între clase. Dar datele reale au excepții.”

---

# 7. Hard-margin SVM

În cazul ideal, toate punctele sunt perfect separabile.

Vrem ca:

- punctele pozitive să fie pe sau dincolo de linia \(+1\);
- punctele negative să fie pe sau dincolo de linia \(-1\).

Putem scrie ambele condiții compact:

$$
y_i(w^Tx_i+b)\geq1
$$

## Cum explic formula

Pentru:

$$
y_i=+1
$$

obținem:

$$
w^Tx_i+b\geq1
$$

Pentru:

$$
y_i=-1
$$

obținem:

$$
w^Tx_i+b\leq-1
$$

Formula spune:

> Fiecare punct trebuie să fie clasificat corect și să rămână în afara marginii.

## Problema

Dataseturile reale pot conține:

- outlieri;
- zgomot;
- etichete greșite;
- clase care se suprapun;
- factori pe care nu i-am măsurat.

Un singur student atipic poate face o margine perfectă imposibilă sau absurd de îngustă.

### Tranziție

> „Nu vrem ca un singur punct ciudat să forțeze modelul să strice frontiera pentru toate celelalte puncte.”

---

# 8. Soft-margin SVM

Soft margin permite unor puncte:

- să intre în margine;
- uneori chiar să ajungă de partea greșită.

Introducem pentru fiecare punct o toleranță:

$$
\xi_i\geq0
$$

Condiția devine:

$$
y_i(w^Tx_i+b)\geq1-\xi_i
$$

## Interpretare intuitivă

### Cazul 1 - punctul respectă marginea

$$
\xi_i = 0
$$

Punctul este clasificat corect și se află pe margine sau în afara ei.

---

### Cazul 2 -punctul intră în margine

$$
0 < \xi_i < 1
$$

Punctul este încă clasificat corect, dar se află în interiorul marginii.

---

### Cazul 3 - punctul este clasificat greșit

$$
\xi_i > 1
$$

Punctul a trecut de frontiera de decizie și se află în partea greșită.

SVM trebuie acum să echilibreze două obiective:

1. margine cât mai mare;
2. cât mai puține încălcări.

Funcția obiectiv devine:

$$
\min
\left(
\frac12\lVert w\rVert^2
+
C\sum_i\xi_i
\right)
$$

Traducere:

- primul termen cere o margine largă;
- al doilea penalizează încălcările.

### Tranziție

> „Mai rămâne să stabilim cât de grav considerăm fiecare încălcare. Asta controlează parametrul \(C\).”

---

# 9. Parametrul \(C\)

\(C\) controlează compromisul dintre:

- margine largă;
- puține erori pe train.

## \(C\) mare

Mesajul pentru model:

> „Greșelile sunt foarte scumpe.”

Modelul:

- încearcă să corecteze aproape toate punctele;
- poate produce o margine mai îngustă;
- poate deveni sensibil la outlieri;
- poate avea risc mai mare de overfitting.

## \(C\) mic

Mesajul pentru model:

> „Accept unele excepții dacă obțin o frontieră mai simplă.”

Modelul:

- tolerează mai multe puncte în margine;
- poate produce o margine mai largă;
- poate fi mai robust;
- dacă este prea permisiv, poate face underfitting.

### Formulare importantă

> \(C\) mare nu înseamnă automat model mai bun.

### Întrebare pentru sală

> „Dacă un student a studiat mult și a rezolvat multe exerciții, dar totuși a picat, vrem să rotim complet frontiera pentru acel singur punct?”

### Tranziție

> „Am vorbit mereu despre punctele care ating sau încalcă marginea. Acestea sunt punctele care determină efectiv soluția.”

---

# 10. Support vectors

Support vectors sunt punctele care influențează direct poziția frontierei.

În hard-margin SVM, sunt punctele care ating:

$$
w^Tx+b=1
$$

sau:

$$
w^Tx+b=-1
$$

În soft-margin SVM, pot fi și puncte:

- aflate în interiorul marginii;
- clasificate greșit.

## Experiment intuitiv

Întreabă:

> „Dacă mutăm puțin un punct foarte îndepărtat de frontieră, se schimbă linia?”

Probabil foarte puțin sau deloc.

> „Dacă mutăm un punct care atinge marginea?”

Frontiera se poate schimba.

### Ideea centrală

> Nu toate observațiile influențează în mod egal SVM-ul.

Punctele aflate departe confirmă separarea.

Support vectors o determină.

## Legătura cu notebookul

```python
model.support_vectors_
```

arată coordonatele support vectors.

```python
model.n_support_
```

arată câte avem din fiecare clasă.

```python
model.decision_function(...)
```

arată scorul față de frontieră.

---



