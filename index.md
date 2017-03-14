---
layout: default
title: "Ghidul concurentului la OJI"
description: "O colecție de sfaturi pentru concurenții la olimpiada de
informatica"
---

[Pull requests](https://github.com/{{ site.github_username }}/{{ site.github_username}}.github.io/edit/master/resources.md).

# Cuprins

  * [Introducere](#introducere)
  * [Ghid general pentru olimpiada de informatică](#ghid-general-pentru-olimpiada-de-informatic%C4%83)
    * [freopen](#freopen)
    * [Debug](#debug)
    * [Șmen pentru utilizatorii de Code::Blocks pe Linux](#șmen-pentru-utilizatorii-de-codeblocks-pe-linux)
    * [Calcularea timpului](#calcularea-timpului)
    * [Setări pentru compilator\-ul de C/C\+\+](#setări-pentru-compilator-ul-de-cc)
    * [Calcularea memoriei](#calcularea-memoriei)
    * [Bibliotecile non\-standard](#bibliotecile-non-standard)
    * [Zecimale](#zecimale)
    * [Strategie pe timp de concurs](#strategie-pe-timp-de-concurs)
    * [Strategie de pregătire pentru concurs:](#strategie-de-preg%C4%83tire-pentru-concurs)
    * [Psihologia de concurs](#psihologia-de-concurs)

# Introducere

La olimpiada de informatică sunt multe moduri in care poți greși, de la
emoții, din neatenție sau pur și simplu pentru ca nu te-ai pregătit. De aceea,
	noi am făcut acest site cu sfaturi și informații.

În continuare găsiți un ghid general pentru olimpiadă, scris de însuși Matei
Tinca, olimpic la informatică. Apoi, vom continua cu diferite sfaturi și
informații împărțite pe categorii.

# Ghid general pentru olimpiada de informatică

Șmecherii de implementare/obiceiuri bune și rele

## `freopen`

În general utilizarea funcției `freopen` nu este recomandată, deoarece într-o adevărată companie dacă dai redirect la mai multe fișiere se pot întâmplă lucruri dubioase. Pentru olimpiadă să zicem că e ok, deoarece scapă programul de cod în plus. Problema cu `freopen()` este că nu se poate scrie pe consolă. Există totuși o soluție:

```c
 fprintf(stderr, "...", ...);
 ```

## Debug

Debug-ul este un lucru foarte important atunci când faci o problemă. Consider că debugger-ul integrat din mediul de programare (funcția de "watches") nu este bună deoarece e mai greu de folosit și arată mai puține lucruri. Eu cred că dacă îți scrii tu datele de care ai nevoie în consolă cu `printf` primești mai multe informații decât iți oferă debugger-ul integrat.

De exemplu, dacă nu merge o bucată din cod, pui `printf("1");` și vezi unde crapă. Sau dacă ai de exemplu o matrice pe care vrei să o verifici, e mai util să o scrii în consolă decât să te uiți prin watches.

## Șmen pentru utilizatorii de Code::Blocks pe Linux

<small> Disclaimer: nu este un fapt confirmat dacă acest lucru chiar se
întâmplă pe toate sistemele Linux cu Code::Blocks, doar cele cu Ubuntu sau
doar sistemul lui Matei. </small>

Când ești pe Linux și rulezi un program, după ce închizi consolă trebuie să dai alt+tab că să îți apăra că s-a modificat fișierul. Asta se poate remedia cu următoarea setare: Settings -> Environment -> Terminal to launch program... și setați să apăra ceva cu `gnome-terminal`. Am înțeles că nu merge debug-ul din Code::Blocks pe asta.

## Calcularea timpului

O mare problemă este măsurarea timpului. Ideea generală este că un procesor are de obicei 1 GHz care are 1.000.000.000 (un miliard) de tacți pe secundă. Fiecare operație consumă un anumit număr de tacți. În general operațiile de modulo și de împărțire sunt mai încete, sau lucrul cu tipuri de date mai mari gen long long.

 // TODO: bagă pt operații nr de tacti

 Folosind regula de trei simplă

 ```
 1.000.000.000 tacti ........ 1 secundă
 ```

Deducem că pentru limita clasică de 0.1 secunde avem nevoie de 100.000.000 tacți, dar din cauza operațiilor de adunare/scădere/înmulțire/împărțire o să iasă cam 10 milioane de operații la 0.1 secunde.

## Setări pentru compilator-ul de C/C++

Când compilați programul folosiți `-Wall` și `-O2`.
`-Wall` arată toate warning-urile programului și e util atunci când ai uitat să inițializezi o variabilă sau ceva de genul.

`-O2` optimizează programul pentru viteză.

## Calcularea memoriei

Sunt niște reguli relativ simple: tipurile de date consumă un anumit număr de octeți. Fie K = nr total de octeți => memoria totală în kb = K / 1024, iar în mb e K / 1024 / 1024.

| Tip variabilă | Nr. octeți |
|---------------|------------|
| `int`         | 4          |
| `short`       | 2          |
| `char`/`bool` | 1          |
| `long long`   | 8          |
| `float`       | 4          |
| `double`      | 8          |

De exemplu, dacă folosești un vector de 1.000.000 (un milion) de elemente int, atunci memoria totală o să fie: `1.000.000 * 4 = 4.000.000` octeți => memoria totală în mb este ~4 mb

Pro tip: programul mai folosește de la sine 200 de kb, deci dacă folosești un vector care e la limită, există șanse să dea `MLE` (Memory Limit Exceeded)`.

Atenție: dacă evaluarea se face pe Windows, acesta va aloca toată memoria de la început. Linux alocă doar parțial, de exemplu dacă ai un vector de 1.000.000 de elemente și le folosești doar pe primele 100, îți va aloca doar primele 100 de elemente. Pe Windows îți va aloca tot vectorul și poți lua MLE.

## Bibliotecile non-standard

`bits/stdc++.h` nu e librărie standard, deci nu va merge compilarea la olimpiadă.

## Zecimale

În primul rând ce merge și ce nu merge:

```c
printf("%f", x);  // merge
printf("%lf", x); // nu merge
scanf("%f", &x);  // merge
scanf("%lf", &x); // merge
```

Pentru a afișa un număr real cu un anumit număr de zecimale:

```c
printf("%.3f", x); // va afisa numarul cu 3 zecimale
cout << fixed << set_precision(3); // va avea acelasi rezultat ca cel de mai sus. Atentie, trebuie pus la inceput #include <iomanip>
```

## Strategie pe timp de concurs

Există foarte multe strategii de concurs. Nu pot să zic care ar fi cea mai bună, dar pot să dau niște sfaturi, dar nu promit nimic:

1. Citește mai intâi toate problemele, dacă nu te prinzi de vreuna, încearcă să vezi care dintre ele ar fi mai usoară și încearcă să o rezolvi. Ia-le crescator.

2. Scrie programele cu cât mai multă atenție. Sa fii conștient de faptul că un singur caracter în plus sau în minus te poate duce de la 100 puncte la 0 puncte.

3. Testeaza-ți programul. Caută contra-exemple sau cazuri particulare.

4. Dacă ai terminat și mai ai timp destul, încearcă sa scrii o soluție proastă și să verifici rezultatele sursei bune cu cea proastă.

	* Eventual fă un generator de teste și un evaluator, dacă mai ai destul timp

5. Să te uiți mereu la timp și la memorie.

6. Dacă se întâmplă ceva: iți crapă calculatorul și trebuie să se repare: negociază cu supraveghetorii să iți acorde timpul pierdut.

7. Verifică memoria si timpul.

8. Dacă folosești vectori preinițializați să ai grijă să nu depășești marimea sursei în caz că ai sute peste sute de valori.

9. Să nu uiți `printf`-urile de debug in program deoarece încetinesc rău programul, iar dacă folosești `freopen` si `printf` o să rămână în fișier și probabil că o sa iei 0

10. Gândește-te bine la soluție înainte să te apuci să o scrii.

11. Să ai grijă în caz că faci modificări în ultimele 5 minute, deoarece există sanse sa faci vreo prostie si sa pierzi puncte. In caz ca faci asta sa iti salvezi sursa intr-un notepad ca sa nu o pierzi pe cea veche.

12. De fiecare data cand scrii ceva sa dai save (ctrl+s).

## Strategie de pregătire pentru concurs:

1. Munca e cel mai important lucru. Pentru a avea rezultate trebuie sa lucrezi mai mult la informatica. Surse bune de pregatire: [varena](http://varena.ro/), [campion](http://campion.edu.ro/arhiva/), [infoarena](http://infoarena.ro/), [pbinfo](https://pbinfo.ro/).

2. E bine sa iti repeti lucrurile de baza. Recomand www.algopedia.ro

3. Sa nu furi sursele altcuiva. Pe Infoarena, la anumite probleme poti sa te uiti pe sursele altora fara ca tu sa fi rezolvat problema cu scopul de a invata ceva unii de la altii. Daca furi o sursa e ca si cum ti-ai fura singur caciula. Nu inveti nimic.

4. Sa nu stai mult pe o problema. Daca dupa ore peste ore de munca nu iti iese o problema, intreaba pe cineva, un prieten, un profesor sau sa te uiti pe solutie. Totusi, sa nu faci asta fara sa stai sa te gandesti la o problema. Consider ca daca dupa o ora si jumatate nu te-ai prins de solutie sa te duci sa intrebi pe cineva sau sa treci la alta problema.

5. Mai bine faci adhocuri / probleme pe care le poti primi tu la concurs decat sa inveti lucruri super-avansate.

6. Nu sari peste etape. Toate lucrurile trebuie invatate intr-un mod structurat si logic. Recomand www.algopedia.ro.

7. Fara procrastinare. Poti sa lucrezi cu muzica, exista sanse sa iti scada atentia, dar e acceptabil. Youtube-ul in schimb te poate scoate total din treaba si sa pierzi timp.

8. Dupa olimpiada merge o pauza, dar nu prea mare. Recomand cititul de carti si plimbarile.

9. Sa nu lucrezi intens la info cu o zi inainte de proba. Sau pe scurt nu ingrasa porcul de Ajun. In plus, daca nu iti iese o problema te vei demoraliza degeaba.

10. Daca nu ai inteles vreun algoritm trivial dintr-o anumita sursa intreaba pe cineva experimentat, cum ar fi un profesor, un parinte sau un prieten.

11. Informatica nu e neaparat matematica, dar totusi necesita un minim de cunostinte. In plus, informatica se bazeaza mai mult pe lucruri cu mult diferite de ce se face la clasa precum combinatorica, probabilitatile etc. (cel putin la gimnaziu).

## Psihologia de concurs

1. Sa nu uiti de faptul ca olimpiada nu este cel mai important lucru legat de informatica. Daca esuezi la vreo etapa sa nu te demoralizezi total, ci sa fii determinat sa lucrezi mai mult ca sa nu ti se mai intample.

	* Sa ne gandim la cursurile de info ca si la niste cursuri de karate. Acolo la cursuri trebuie sa faci bine, civilizat si elegant, dar la olimpiada e ca si cum vine cineva pe strada si incearca sa te fure. Atunci nu te va controla nimeni cum faci, cat de elegant faci, tot ce conteaza este sa treci. Daca gasesti o bata, poti sa o folosesti.

2. Daca la o problema nu ai nici o idee incearca sa gasesti un caz particular cu care ai putea sa iei un test sau doua. Orice punct conteaza ca sa treci.

3. Daca totusi la o etapa nu te califici, poti sa faci ce iti doresti. Ori poti sa inveti pentru Evaluarea Nationala/Bac, lucru pe care il recomand, sau poti sa inveti alte lucruri care nu sunt legate neaparat de info, cum ar fi cum sa faci un joc, grafica etc. , sau poti sa inveti materie in avans. Credeti-ma, materia avansata e foarte frumoasa. Poti eventual sa iei o pauza ca sa iti recapeti fortele pentru anul urmator. Poti sa te apuci de alte materii interesante cum ar fi fizica, astronomia, chimia etc.
