

# 1. De ce avem nevoie de altceva decât o frontieră liniară

Până acum, funcția de decizie a fost:

$$
f(x)=w^Tx+b
$$

iar frontiera:

$$
w^Tx+b=0
$$

În două dimensiuni, aceasta este o dreaptă.

Pentru unele dataseturi, o dreaptă este suficientă. Pentru altele, nu există nicio dreaptă care să separe corect clasele.

## Exemplul cercurilor

Presupunem că avem două clase:

- clasa \(-1\) formează un cerc interior;
- clasa \(+1\) formează un inel în jurul lui.

Fiecare punct este descris prin două coordonate:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

Asta înseamnă că fiecare observație este doar un punct în plan.

Problema este forma claselor:

- punctele unei clase sunt în centru;
- punctele celeilalte clase le înconjoară.

Orice dreaptă trasăm va tăia inevitabil una dintre clase.

Nu putem avea o singură linie care să lase:

- tot cercul interior într-o parte;
- tot cercul exterior în cealaltă parte.

Cu alte cuvinte, problema nu este **liniar separabilă** în spațiul original.

> Nu este o problemă că modelul nu s-a antrenat suficient.

> Nu este nici o problemă de alegere greșită a parametrului \(C\).

> În reprezentarea actuală a datelor, frontiera liniară potrivită pur și simplu nu există.

Parametrul \(C\) poate controla cât de mult tolerăm punctele clasificate greșit sau aflate în interiorul marginii.

Dar \(C\) nu schimbă forma de bază a frontierei.

Dacă folosim un kernel liniar, frontiera rămâne o dreaptă.

Prin urmare:

> \(C\) poate muta sau ajusta dreapta, dar nu o poate transforma într-un cerc.

Asta ne conduce la următoarea idee:

> Dacă forma datelor nu poate fi separată printr-o dreaptă, trebuie să schimbăm modul în care reprezentăm punctele.

![[Pasted image 20260806232909.png]]


---

# 2. Maparea într-un spațiu nou

În spațiul original, fiecare punct este descris prin două coordonate:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

Putem interpreta:

- \(x_1\) ca poziția pe axa orizontală;
- \(x_2\) ca poziția pe axa verticală.

Problema este că, folosind doar aceste două coordonate, cele două clase formează cercuri concentrice și nu pot fi separate printr-o dreaptă.

Ideea este să construim un feature nou care descrie mai bine forma datelor.

Pentru problema cercurilor alegem:

$$
z=x_1^2+x_2^2
$$

Această valoare măsoară cât de departe se află punctul față de centrul graficului.

Mai exact, distanța față de origine este:

$$
\sqrt{x_1^2+x_2^2}
$$

Dar pentru separarea claselor nu avem nevoie neapărat de radical.

Putem folosi direct:

$$
z=x_1^2+x_2^2
$$

pentru că ordinea punctelor rămâne aceeași:

- un punct apropiat de centru are un \(z\) mic;
- un punct îndepărtat de centru are un \(z\) mare.

---

## Exemplu intuitiv

Luăm un punct apropiat de centru:

$$
x=
\begin{bmatrix}
0.2\\
0.3
\end{bmatrix}
$$

Atunci:

$$
z=0.2^2+0.3^2
$$

$$
z=0.04+0.09
$$

$$
z=0.13
$$

Acest punct are o valoare mică pentru \(z\), deci este probabil în cercul interior.

Luăm acum un punct mai îndepărtat:

$$
x=
\begin{bmatrix}
0.9\\
0.8
\end{bmatrix}
$$

Atunci:

$$
z=0.9^2+0.8^2
$$

$$
z=0.81+0.64
$$

$$
z=1.45
$$

Acest punct are o valoare mai mare pentru \(z\), deci este probabil în cercul exterior.

---

## Ce am câștigat

În planul original, clasele aveau o formă circulară și nu puteau fi separate printr-o dreaptă.

După ce construim feature-ul:

$$
z=x_1^2+x_2^2
$$

putem privi punctele după distanța lor față de centru.

Astfel:

- cercul interior produce valori mici pentru \(z\);
- cercul exterior produce valori mari pentru \(z\).

Putem separa cele două clase printr-un prag:

$$
z<c
$$

pentru cercul interior și:

$$
z>c
$$

pentru cercul exterior.

Cu alte cuvinte:

> O problemă care nu putea fi separată liniar în coordonatele originale devine mult mai simplă după ce alegem un feature mai potrivit.

### Tranziție

> „Acum nu mai folosim doar poziția stânga-dreapta și sus-jos a punctului. Adăugăm și informația despre cât de departe este el față de centru.”


# 3. Funcția de transformare 

Notăm transformarea prin:

$$
\phi(x)
$$

Litera grecească \(\phi\), citită „fi”, reprezintă o funcție care primește punctul original și produce o reprezentare nouă a lui.

Important:

> Nu schimbăm observația în sine.

Studentul sau punctul rămâne același.

Schimbăm doar modul în care îl descriem.

---

## Exemplu

În spațiul original avem:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

Punctul este descris doar prin:

- poziția pe axa \(x_1\);
- poziția pe axa \(x_2\).

Pentru problema cercurilor, adăugăm informația despre distanța față de centru:

$$
z=x_1^2+x_2^2
$$

Noua reprezentare devine:

$$
\phi(x)=
\begin{bmatrix}
x_1\\
x_2\\
x_1^2+x_2^2
\end{bmatrix}
$$

sau, folosind notația \(z\):

$$
\phi(x)=
\begin{bmatrix}
x_1\\
x_2\\
z
\end{bmatrix}
$$

---

## Ce s-a schimbat concret

Spațiul original avea două coordonate:

$$
(x_1,x_2)
$$

Spațiul transformat are trei coordonate:

$$
(x_1,x_2,z)
$$

Am adăugat o axă nouă.

Această axă nu conține o informație complet nouă din dataset.

Ea este calculată din coordonatele existente:

$$
z=x_1^2+x_2^2
$$

Dar poate face forma claselor mai ușor de separat.

---

## Exemplu numeric

Pentru punctul:

$$
x=
\begin{bmatrix}
0.2\\
0.3
\end{bmatrix}
$$

avem:

$$
z=0.13
$$

Prin urmare:

$$
\phi(x)=
\begin{bmatrix}
0.2\\
0.3\\
0.13
\end{bmatrix}
$$

Punctul nu a devenit o altă observație.

Este același punct, descris acum prin trei valori în loc de două.

---

## De ce facem transformarea

În planul original, clasele circulare nu puteau fi separate cu o dreaptă.

După adăugarea coordonatei \(z\):

- punctele apropiate de centru au valori mici pe noua axă;
- punctele îndepărtate au valori mari;
- clasele pot deveni separabile printr-un plan în spațiul tridimensional.

Așadar:

> Transformarea \(\phi\) caută o reprezentare în care problema de clasificare să fie mai simplă.

Această operație poate fi numită:

- mapare într-un spațiu de features;
- embedding;
- ridicare într-un spațiu cu mai multe dimensiuni.

În materialul de curs folosim formularea:

> **mapare într-un spațiu de features nou**

### Tranziție

> „Am reușit să facem problema mai simplă adăugând manual un feature. Dar pentru dataseturi mari nu putem ghici și construi de fiecare dată toate transformările utile.”

---

# 4. De ce transformarea ajută

În planul original, punctele formează două cercuri.

După adăugarea coordonatei:

$$
z=x_1^2+x_2^2
$$

punctele cercului interior se află la valori mici ale lui $z$, iar punctele cercului exterior la valori mari.

În spațiul tridimensional putem folosi un plan pentru a le separa.

Funcția de decizie devine:

$$
f(x)=w^T\phi(x)+b
$$

Modelul este în continuare liniar în spațiul transformat.

Când privim frontiera înapoi în spațiul original, ea apare curbată.

> Frontiera poate fi neliniară în spațiul original, dar liniară în spațiul transformat.

---

# 5. De ce nu construim manual toate transformările

Pentru două features putem încerca manual:

$$
x_1^2,\quad x_2^2,\quad x_1x_2,\quad x_1^2+x_2^2
$$

Dar pentru un dataset cu multe features pot apărea:

- pătratele tuturor coloanelor;
- produsele dintre toate perechile;
- termeni de grad mai mare;
- foarte multe interacțiuni.

Numărul coordonatelor poate crește rapid.

Construirea explicită a spațiului transformat poate necesita:

- mai multă memorie;
- mai mult timp de calcul;
- foarte multe coloane noi.

În unele cazuri, spațiul asociat unui kernel poate avea extrem de multe sau chiar infinit de multe dimensiuni.

### Tranziție

> „Ar fi util să obținem efectul transformării fără să construim efectiv toate coordonatele noi.”

---

# 6. De ce apar produsele scalare în SVM

Până acum am scris funcția de decizie astfel:

$$
f(x)=w^Tx+b
$$

Pentru un punct nou \(x\), modelul calculează un scor.

- dacă scorul este pozitiv, punctul ajunge într-o clasă;
- dacă scorul este negativ, ajunge în cealaltă clasă.

Vectorul \(w\) descrie orientarea frontierei.

Întrebarea importantă pentru Kernel Trick este:

> De unde vine vectorul \(w\) și cum poate fi exprimată decizia folosind punctele din dataset?

---

## Legătura dintre \(w\) și punctele de antrenare

În SVM, vectorul \(w\) poate fi scris sub forma:

$$
w=\sum_i\alpha_i y_i x_i
$$

O interpretăm pe componente:

- \(x_i\) este un punct din setul de antrenare;
- \(y_i\in\{-1,+1\}\) este clasa acelui punct;
- \(\alpha_i\) arată cât de mult contribuie punctul la construirea frontierei;
- simbolul \(\sum_i\) înseamnă că adunăm contribuțiile tuturor punctelor.

Cu alte cuvinte:

> Vectorul \(w\) este construit ca o combinație ponderată a punctelor de antrenare.

---

## Ce rol are \(y_i\)

Eticheta:

$$
y_i\in\{-1,+1\}
$$

stabilește sensul contribuției punctului.

- un punct din clasa \(+1\) contribuie în direcția sa;
- un punct din clasa \(-1\) contribuie cu semn opus.

Astfel, modelul combină informația venită din ambele clase pentru a construi direcția frontierei.

---

## Ce rol are \(\alpha_i\)

Coeficientul:

$$
\alpha_i
$$

arată importanța punctului \(x_i\).

- dacă \(\alpha_i=0\), punctul nu contribuie direct la soluția finală;
- dacă \(\alpha_i>0\), punctul influențează frontiera.

Pentru majoritatea punctelor aflate departe de frontieră:

$$
\alpha_i=0
$$

Punctele cu coeficienți nenuli sunt, în principal, **support vectors**.

Prin urmare, deși formula conține suma tuturor punctelor, decizia finală depinde în special de observațiile apropiate de margine.

---

## Introducem expresia lui \(w\) în funcția de decizie

Pornim de la:

$$
f(x)=w^Tx+b
$$

și știm că:

$$
w=\sum_i\alpha_i y_i x_i
$$

Înlocuim \(w\):

$$
f(x)=
\left(
\sum_i\alpha_i y_i x_i
\right)^Tx+b
$$

Produsul cu \(x\) se distribuie peste sumă:

$$
f(x)=
\sum_i\alpha_i y_i(x_i^Tx)+b
$$

Nu s-a schimbat rolul funcției.

Ea produce în continuare un scor pentru punctul nou.

S-a schimbat doar modul în care exprimăm acel scor.

---

## De unde apare produsul scalar

În formula obținută apare:

$$
x_i^Tx
$$

Acesta este produsul scalar dintre:

- punctul de antrenare \(x_i\);
- punctul nou \(x\).

Pentru două features:

$$
x_i=
\begin{bmatrix}
x_{i1}\\
x_{i2}
\end{bmatrix}
$$

și:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

produsul scalar este:

$$
x_i^Tx
=
x_{i1}x_1+x_{i2}x_2
$$

Așadar, modelul nu mai are nevoie să privească separat toate componentele lui \(w\).

Poate calcula decizia folosind direct comparațiile dintre punctul nou și observațiile importante din train.

---

## Cum interpretăm produsul scalar

Produsul scalar măsoară cât de bine se aliniază doi vectori.

În mod intuitiv:

- o valoare mare și pozitivă indică o orientare asemănătoare;
- o valoare apropiată de zero indică puțină aliniere;
- o valoare negativă indică direcții opuse.

Totuși, produsul scalar brut depinde și de lungimea vectorilor.

De aceea nu îl tratăm automat ca pe o măsură perfectă de „asemănare” în orice situație.

Pentru Kernel Trick, ideea importantă este doar:

> SVM folosește punctele prin produse scalare între ele.

---

## Cum produce modelul scorul

Putem citi formula:

$$
f(x)=
\sum_i\alpha_i y_i(x_i^Tx)+b
$$

în patru pași.

### Pasul 1 - comparăm punctul nou cu un punct de antrenare

$$
x_i^Tx
$$

### Pasul 2 - ținem cont de clasa punctului

$$
y_i(x_i^Tx)
$$

### Pasul 3 - ponderăm contribuția lui

$$
\alpha_i y_i(x_i^Tx)
$$

### Pasul 4 - adunăm toate contribuțiile

$$
f(x)=
\sum_i\alpha_i y_i(x_i^Tx)+b
$$

Rezultatul este scorul final.

---

## Legătura cu support vectors

Deoarece majoritatea coeficienților sunt zero, putem interpreta formula astfel:

$$
f(x)=
\sum_{\text{support vectors}}
\alpha_i y_i(x_i^Tx)+b
$$

În practică:

1. luăm punctul nou;
2. îl comparăm cu fiecare support vector;
3. ponderăm comparațiile;
4. adunăm contribuțiile;
5. obținem scorul final.

Semnul scorului stabilește clasa:

$$
f(x)>0
\Rightarrow
\hat y=+1
$$

$$
f(x)<0
\Rightarrow
\hat y=-1
$$

---

# 7. Ce se schimbă după mapare

Dacă mapăm datele prin:

$$
\phi(x)
$$

produsul scalar obișnuit:

$$
x_i^Tx
$$

devine:

$$
\phi(x_i)^T\phi(x)
$$

Funcția de decizie poate fi scrisă:

$$
f(x)=
\sum_i
\alpha_i y_i
\left(
\phi(x_i)^T\phi(x)
\right)
+b
$$

Pentru a calcula direct această expresie, ar trebui să:

1. transformăm fiecare punct;
2. construim toate coordonatele lui $\phi(x)$;
3. calculăm produsul scalar în spațiul nou.

Dacă spațiul este foarte mare, abordarea poate deveni costisitoare.

---

# 8. Kernel Trick

Până aici am ajuns la următoarea idee:

SVM-ul are nevoie de produse scalare între puncte.

În spațiul original folosim:

$$
x_i^Tx
$$

După transformarea punctelor prin:

$$
\phi(x)
$$

am avea nevoie de:

$$
\phi(x_i)^T\phi(x)
$$

Problema este că vectorii transformați pot avea foarte multe coordonate.

De aceea vrem să calculăm rezultatul produsului scalar fără să construim explicit acei vectori.

---

## Definiția kernelului

Definim o funcție:

$$
K(x_i,x_j)
=
\phi(x_i)^T\phi(x_j)
$$

Kernelul primește două puncte din spațiul original:

$$
x_i
\quad\text{și}\quad
x_j
$$

și întoarce direct valoarea produsului scalar pe care am fi obținut-o după transformare.

Cu alte cuvinte, în loc să facem:

1. transformarea primului punct;
2. transformarea celui de-al doilea punct;
3. produsul scalar dintre reprezentările noi;

kernelul calculează direct rezultatul final.

---

## Pas cu pas

Fără kernel, am face:

$$
x_i
\longrightarrow
\phi(x_i)
$$

$$
x_j
\longrightarrow
\phi(x_j)
$$

apoi:

$$
\phi(x_i)^T\phi(x_j)
$$

Cu un kernel, calculăm direct:

$$
K(x_i,x_j)
$$

iar valoarea este aceeași:

$$
K(x_i,x_j)
=
\phi(x_i)^T\phi(x_j)
$$

Așadar:

> Kernel Trick înseamnă că obținem rezultatul comparației din spațiul transformat fără să construim explicit coordonatele din acel spațiu.

---

## De ce se numește „trick”

Nu este un truc prin care evităm transformarea matematică.

Transformarea există conceptual.

Doar că nu o calculăm explicit.

Kernelul ne permite să lucrăm:

> ca și cum punctele ar fi fost transformate într-un spațiu nou.

De exemplu, spațiul transformat ar putea avea:

- zeci de features;
- mii de features;
- foarte multe dimensiuni.

Noi continuăm să oferim kernelului doar punctele originale:

$$
x_i
\quad\text{și}\quad
x_j
$$

---

## Funcția de decizie cu kernel

În forma liniară aveam:

$$
f(x)
=
\sum_i
\alpha_i y_i
(x_i^Tx)
+b
$$

După transformare, produsul scalar ar deveni:

$$
\phi(x_i)^T\phi(x)
$$

Prin definiția kernelului:

$$
K(x_i,x)
=
\phi(x_i)^T\phi(x)
$$

Prin urmare, funcția de decizie devine:

$$
f(x)
=
\sum_i
\alpha_i y_i K(x_i,x)
+b
$$

---

## Cum citim formula

Pentru un punct nou \(x\):

### Pasul 1

Îl comparăm cu un punct important din train:

$$
K(x_i,x)
$$

### Pasul 2

Ținem cont de clasa acelui punct:

$$
y_iK(x_i,x)
$$

### Pasul 3

Ponderăm contribuția lui:

$$
\alpha_i y_iK(x_i,x)
$$

### Pasul 4

Adunăm toate contribuțiile și adăugăm \(b\):

$$
f(x)
=
\sum_i
\alpha_i y_iK(x_i,x)
+b
$$

În practică, punctele relevante sunt în principal support vectors.

---

## Imaginea intuitivă

Fără Kernel Trick:

$$
x_i
\longrightarrow
\phi(x_i)
$$

$$
x
\longrightarrow
\phi(x)
$$

$$
\phi(x_i)^T\phi(x)
$$

Cu Kernel Trick:

$$
(x_i,x)
\longrightarrow
K(x_i,x)
$$

Kernelul sare direct la valoarea produsului scalar din spațiul transformat.

---

# 10. Exemplu concret: kernelul polinomial

Până acum am spus că un kernel poate calcula direct produsul scalar dintr-un spațiu transformat.

Acum vedem un exemplu concret în care putem identifica exact ce features apar în acel spațiu nou.

Considerăm kernelul:

$$
K(x,z)=(x^Tz)^2
$$

Aici:

- \(x\) este primul punct;
- \(z\) este al doilea punct;
- \(x^Tz\) este produsul scalar dintre ele;
- apoi ridicăm rezultatul la pătrat.

---

## Pasul 1 - scriem produsul scalar

Presupunem că ambele puncte au două features:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

și:

$$
z=
\begin{bmatrix}
z_1\\
z_2
\end{bmatrix}
$$

Produsul scalar dintre ele este:

$$
x^Tz=x_1z_1+x_2z_2
$$

Prin urmare, kernelul devine:

$$
K(x,z)=\left(x_1z_1+x_2z_2\right)^2
$$

---

## Pasul 2 - dezvoltăm pătratul

Folosim formula:

$$
(a+b)^2=a^2+2ab+b^2
$$

unde:

$$
a=x_1z_1
$$

și:

$$
b=x_2z_2
$$

Obținem:

$$
\left(x_1z_1+x_2z_2\right)^2
=
x_1^2z_1^2
+
2x_1x_2z_1z_2
+
x_2^2z_2^2
$$

Așadar:

$$
K(x,z)
=
x_1^2z_1^2
+
2x_1x_2z_1z_2
+
x_2^2z_2^2
$$

Observăm că au apărut termeni care nu existau separat în spațiul original:

$$
x_1^2
$$

$$
x_1x_2
$$

$$
x_2^2
$$

Aceștia pot fi interpretați ca features noi.

---

## Pasul 3 - construim transformarea \(\phi\)

Definim:

$$
\phi(x)=
\begin{bmatrix}
x_1^2\\
\sqrt{2}x_1x_2\\
x_2^2
\end{bmatrix}
$$

și:

$$
\phi(z)=
\begin{bmatrix}
z_1^2\\
\sqrt{2}z_1z_2\\
z_2^2
\end{bmatrix}
$$

Am ales exact aceste trei componente deoarece ele apar atunci când dezvoltăm:

$$
(x^Tz)^2
$$

Factorul:

$$
\sqrt{2}
$$

este pus în termenul din mijloc astfel încât, în produsul scalar, să obținem coeficientul corect:

$$
\sqrt{2}\cdot\sqrt{2}=2
$$

În spațiul original, fiecare punct avea două coordonate:

$$
(x_1,x_2)
$$

După transformare, fiecare punct are trei coordonate:

$$
\left(
x_1^2,
\sqrt{2}x_1x_2,
x_2^2
\right)
$$

Cu alte cuvinte, noua reprezentare conține:

- pătratul primului feature;
- combinația dintre cele două features;
- pătratul celui de-al doilea feature.

---

## Pasul 4 - calculăm produsul scalar în spațiul nou

Produsul scalar dintre cele două reprezentări este:

$$
\phi(x)^T\phi(z)
$$

Adică:

$$
\phi(x)^T\phi(z)
=
x_1^2z_1^2
+
\left(\sqrt{2}x_1x_2\right)
\left(\sqrt{2}z_1z_2\right)
+
x_2^2z_2^2
$$

Termenul din mijloc devine:

$$
\left(\sqrt{2}x_1x_2\right)
\left(\sqrt{2}z_1z_2\right)
=
2x_1x_2z_1z_2
$$

Prin urmare:

$$
\phi(x)^T\phi(z)
=
x_1^2z_1^2
+
2x_1x_2z_1z_2
+
x_2^2z_2^2
$$

Dar aceasta este exact expresia obținută din kernel:

$$
K(x,z)
=
x_1^2z_1^2
+
2x_1x_2z_1z_2
+
x_2^2z_2^2
$$

Deci:

$$
\boxed{
K(x,z)=\phi(x)^T\phi(z)
}
$$

---

## Ce demonstrează exemplul

Kernelul:

$$
K(x,z)=(x^Tz)^2
$$

calculează direct același rezultat pe care l-am obține dacă:

1. am transforma fiecare punct;
2. am construi features-urile:

$$
x_1^2,\quad
\sqrt{2}x_1x_2,\quad
x_2^2
$$

3. am calcula produsul scalar în spațiul nou.

Dar kernelul nu trebuie să construiască explicit aceste coordonate.

El primește direct punctele originale:

$$
x
\quad\text{și}\quad
z
$$

și calculează:

$$
(x^Tz)^2
$$

obținând același rezultat.

### Ideea care trebuie să rămână

> Kernelul polinomial produce efectul unor features neliniare fără să fie obligatoriu să construim manual acele features.

> Aici vedem concret de ce Kernel Trick funcționează: rezultatul kernelului este exact produsul scalar dintr-un spațiu transformat.

## Ce demonstrează exemplul

Kernelul:

$$
K(x,z)=(x^Tz)^2
$$

produce efectul features-urilor:

$$
x_1^2,\quad \sqrt{2}x_1x_2,\quad x_2^2
$$

fără să fie obligatoriu să construim manual aceste coloane.

Acesta este exemplul concret care arată că Kernel Trick nu este doar o metaforă.

---

# 11. Kernel liniar, polinomial și RBF

## Kernel liniar

$$
K(x_i,x_j)=x_i^Tx_j
$$

Frontiera rămâne liniară în spațiul original.

```python
SVC(kernel="linear")
```

## Kernel polinomial

O formă uzuală este:

$$
K(x_i,x_j)=\left(\gamma x_i^Tx_j+r\right)^d
$$

Poate reprezenta:

- pătrate;
- produse între features;
- interacțiuni de grad mai mare.

```python
SVC(
    kernel="poly",
    degree=2,
)
```

## Kernel RBF

$$
K(x_i,x_j)=
\exp\left(-\gamma\lVert x_i-x_j\rVert^2\right)
$$

Compară punctele pe baza distanței dintre ele:

- puncte apropiate → kernel aproape de $1$;
- puncte îndepărtate → kernel aproape de $0$.

```python
SVC(
    kernel="rbf",
    gamma="scale",
)
```

---

# 12. Cum produce kernelul o predicție

Pentru un punct nou $x$, SVM calculează schematic:

$$
f(x)=
\sum_i\alpha_i y_i K(x_i,x)+b
$$

În practică, ne putem gândi în principal la support vectors:

$$
f(x)=
\sum_{\text{support vectors}}
\alpha_i y_i K(x_i,x)+b
$$

Pentru fiecare support vector:

1. kernelul compară support vectorul cu punctul nou;
2. comparația este ponderată prin $\alpha_i y_i$;
3. contribuțiile sunt adunate;
4. se adaugă $b$;
5. semnul scorului stabilește clasa.

$$
f(x)>0\Rightarrow\hat y=+1
$$

$$
f(x)<0\Rightarrow\hat y=-1
$$

Kernelul schimbă modul în care punctele sunt comparate. Regula finală bazată pe semnul scorului rămâne aceeași.

---
