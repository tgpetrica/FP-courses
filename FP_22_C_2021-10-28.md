## MACROCOMENZI
```c
__DATE__
__TIME__
__LINE__
__FILE__
__STDC__	se expandeaza in 1 sau 0 dupa cum compilatorul respecta sau nu standardul ISO
__STDC_VERSION__	se expandeaza intr-un nr intreg de tip long si acesta reprezinta versiunea 
standard de compilare (pt ce versiune de C a fost implentat) in formatul YYYYMM
__cplusplus	se expandeaza in 1 daca si numai daca avem de-a face cu un compilator de C++
__OBJC__	"C++ de la Apple"
__ASSEMBLER__	verifica daca prepocesarea se face in limbaj assembler
_WIN64		este sau nu compilator pentru Windows x64
_WIN32		este sau nu compilator pentru Windows x32
__APPLE__	rezulta cod executabil pentru Apple
__linux		verific daca sunt sub mediul Linux
__unix		verific daca sunt sub mediul Unix
```

In etapa de precompilare:
-includeri
-macrocomenzi
-precompilarea conditionala

## PRECOMPILAREA CONDITIONALA
```c
#ifdef
#if
#ifndef
...
#elif
...
#else
...
#endif
```
ex.:
```c
#ifdef __cplusplus
	cout<<"Salut!"<<endl;
	#else
		printf("salut!\n");
#endif
```

dupa ```#ifdef``` trebuie sa urmeze obligatoriu numele unei macrocomenzi. daca aceasta este definita atunci se compileaza codul ce urmeaza. Daca avem ramura else si macrocomanda nu exista, se compileaza codul ce urmeaza dupa ```#else```.
in exemplul de mai sus, daca este vorba de un compilator C++ care genereaza macromanda ```__cplusplus``` se compileaza afisarea cu ```cout```, altfel se compileaza afisarea cu ```printf```, stil C.

ex.:
```c
#define inter4(x,y,tip){tip inte=x;\
			x=y;\
			y=inte;\
			}
...
int a=1, b=2, c;
#ifdef inter(a,b)
#elif inter2
inter2(a,b,c)
#else
inter4(a,b,int)
#endif


#ifndef __cplusplus
printf...
#else
cout...
#endif


#if define (__cplusplus)
...
#endif


#if __STDC_VERSION__>201100
...
#endif
```


## ELEMENTE ALE LIMBAJULUI C

### FUNCTIA main


Executia unui program C/C++ porneste din interiorul functiei main. Atat intr-un proiect C, cat si intr-unul C++ nu este voie sa existe mai mult de o functie ```main```, chiar daca difera ca nr de parametri. Functia ```main``` este acceptata ca standard avand niciun parametru sau doi. Tipul returnat este, de obicei, ```int``` , dar multe compilatoare accepta si ```void```. O functie care are altul tipul returnat altul decat ```void``` se incheie, de regula, cu un apel al instructiunii ```return```, urmat de o expresie care trebuie sa aibe valoarea convertibila la tipul returnat de catre functie. In consecinta, de obicei, ultima linie a functiei main este: ```return```, urmat de un numar intreg. Parasirea functiei ```main``` are ca efect incheierea executiei aplicatiei. Valoarea ```int``` returnata reprezinta un cod de terminare a executiei aplicatiei. Returnarea valorii ```0``` semnifica faptul ca executia aplicatiei s-a incheiat cu succes. Orice valoare diferita de ```0``` inseamna eroare. Codul returnat de catre aplicatia noastra este primit de catre SO. 

```c
#include <stdio.h>
int main()
{
	printf("Salut!\n");
	return 0;
}

In C exista functia exit(cod); ce primeste ca parametru un cod nr intreg, care atunci cand se executa
intrerupe executia programului.

void main()
{
	printf(...);
}

main()
{
...
}
```

Exista o conventie in unele compilatoare mai recente c/c++ ca atunci cand nu se specifica un tip de date este consider automat ```int```.

```c
const x=1; // se considera ca x este de tip int
```

Functia standard main poate avea si doi parametri. Primul parametru este de tip ```int``` si al doilea este un vector de stringuri ```NULL``` terminate.
```c
void main(int narg,char* varg[])
```

la pornirea executiei primul parametru se initializeaza cu nr de elemente din linie de comanda; al doilea parametru, la pornirea executiei, se initializeaza un vector ce contine denumirile parametrilor din linie de comanda. intotdeauna ```narg > 1``` pt ca primul parametru din linia de comanda este intotdeauna numele executabilului aplicatiei

calculator.exe
calculator 17.8 + 20.22 => 38.02

```c

#include <stdio.h>
int main(int narg, char* varg[])
{
	if(narg!=4) 
		return 1;
	if(strlen(varg[2])!=1) 
		return 1;
	char op==varg[2];
	if(op!='+' && op!='-' && op!='*' && op!='/')
		return 1;
	double x,y;
	sscanf(varg[1],"%lf",&x);
	sscanf(varg[3],"%lf",&y);
	if(op=='+')
		printf("%lf\n",x+y);
	if(op=='-')
		printf("%lf\n",x-y);
	if(op=='*')
		printf("%lf\n",x*y);
	if(op=='/')
		printf("%lf\n",x/y);
	return 0;
}
```

Daca functia ```main``` se implementeaza cu alt numar de parametri in afara de ```0``` sau ```2``` sau cu alte tipuri de date pt cei 2 parametri unele compilatoare vor da eroare, iar altele vor compila functia ```main``` asa cum este data, dar utilizarea valorilor pt parametri va fi evident defectuoasa, daca se incearca acest lucru. 