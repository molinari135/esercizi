# Estensione di una struttura dati esistente con nuovi operatori

## Appello 1
**Specifica sintattica**
* cambia_valore_speciale(alberobin, nodo, valore) &rightarrow; alberobin
* incrementa_figli(alberobin, nodo) &rightarrow; alberobin

**Specifica semantica**
* `cambia_valore_speciale(T, x, v) = T'`
  * **Precondizione:** T = (N, A), x &in; N
  * **Postcondizione:** se `sinistrovuoto(x, T)` = false
    * T' = `scrivinodo(v, figliosinistro(x, T), T)`
    * altrimenti, T' = `scrivinodo(v, x, T)`
* `incrementa_figli(T, x) = T'`
  * **Precondizione:** T = (N, A), x &in; N
  * **Postcondizione:** T' = T
    * se `sinistrovuoto(x, T) = false`
      * dato y = `figliosinistro(x, T)`, T' = `scrivinodo(legginodo(y, T')+1, y, T')`
    * se destrovuoto(x, T) = false
      * dato z = `figliodestro(x, T)`, T' = `scrivinodo(legginodo(z, T')+1, z, T')`

## Appello 2
**Specifica sintattica**
* conta_fratelli(albero, nodo) &rightarrow; intero
* incrementa_padre(albero, nodo) &rightarrow; albero

**Specifica semantica**
* conta_fratelli(T, a) = n
  * **Precondizione:** T = (N, A), a &in; N
  * **Postcondizione:** se `livello(a)` = 0
    * allora n = 0
    * altrimenti, dato p = `padre(a)`, n = |{u &in; N t.c. `padre(u)` = p}| - 1
* incrementa_padre(T, a) = T'
  * **Precondizione:** T = (N, A), a &in; N, `livello(a)` > 0
    * al posto di `livello(a)` > 0 si può scrivere `radice(T)` != a
  * **Postcondizione:** dato p = `padre(a)`
    * T' = `scrivinodo(T, p, legginodo(p)+1)`
    
## Appello 3
**Specifica sintattica**
* conta_figli(albero, nodo) &rightarrow; intero
* più_figli(albero) &rightarrow; nodo

**Specifica semantica**
* conta_figli(T, a) = n
  * **Precondizione:** T = (N, A) AND a &in; N
  * **Postcondizione:** n = |{v &in; N t.c. (a, v) &in; A}|
    * oppure, n = |{v &in; N t.c. padre(v, T) = a}|
* più_figli(T) = a
  * **Precondizione:** T = (N, A) AND T &ne; alberovuoto
  * **Postcondizione:** a &in; N t.c. &notexists; nodo x &in; N con
    * x &ne; a t.c. conta_figli(T, x) &ge; conta_figli(T, a)
    
## Appello 4
**Specifica sintattica**
* due_figli(alberobin, nodo) &rightarrow; boolean
* nonno(alberobin, nodo) &rightarrow; nodo

**Specifica semantica**
* due_figli(T, a) = b
  * **Precondizione:** T = (N, A), a &in; N
  * **Postcondizione:** se ((`sinistrovuoto(a, T)` &ne; true) AND ((`destrovuoto(a, T)` &ne; true)
    * b = true
    * altrimenti, b = false
* nonno(T, a) = u
  * **Precondizione:** T = (N, A), a &in; N, `padre(pare(a, T), T)` &in; N
    * conviene verificare che il livello sia almeno 2
  * **Postcondizione:** u = `padre(padre(a, T), T)`
  
## Appello 5
**Specifica sintattica**
* inverti_pari_dispari(lista) &rightarrow; lista
* incrementa_estremi(lista, intero) &rightarrow; lista

**Specifica semantica**
* inverti_pari_dispari(l) = l'
  * **Precondizione:** l = < a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n-2</sub>, a<sub>n-1</sub>, a<sub>n</sub> > con &ge; 2
  * **Postcondizione:** se n % 2 = 0
    * allora l' = < a<sub>2</sub>, a<sub>1</sub>, a<sub>n</sub>, a<sub>n-1</sub> >
    * altrimenti l' = < a<sub>2</sub>, a<sub>1</sub>, ..., a<sub>n-1</sub>, a<sub>n-2</sub>, a<sub>n</sub> >
* incrementa_estremi(l, x) = l'
  * **Precondizione:** l = < a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> > con n &ge; 2
  * **Postcondizione:** l' = < a<sub>1+x</sub>, a<sub>2</sub>, ..., a<sub>n+x</sub> >
 
## Appello 6
**Specifica sintattica**
* conta_figli_pari(albero, nodo) &rightarrow; intero
* meno_figli_pari(albero) &rightarrow; nodo

**Specifica semantica**
* conta_figli_pari(T, a) = n
  * **Precondizione:** T = (N, A), a &in; N
  * **Postcondizione:** num = |{v &in; N con v &ne; a t.c. 
    * `padre(v, T)` = a AND `legginodo(v, albero)` % 2 == 0}
* meno_figli_pari(T) = a
  * **Precondizione:** T = (N, A)
  * **Postcondizione:** a &in; N &notexists; x &in; N con &ne; a t.c.
    * `conta_figli_pari(T, x)` < `conta_figli_pari(T, a)`
    
## Appello 7
**Specifica sintattica*
* conta_tanti_figli(albero, intero) &rightarrow; intero
* aggiorna_figlio_unico(albero, intero) &rightarrow; albero

**Specifica semantica**
* conta_tanti_figli(T, k) = n
  * **Precondizione:** T = (N, A), `albervuoto(T)` = false
  * **Postcondizione:** n = |{a &in; N |{v &in; N t.c. `padre(v, T)` = a}| &ge; k}|
* aggiorna_figlio_unico(T, n) = T'
  * **Precondizione:** T = (N, A), `alberovuoto(T)` = false
  * **Postcondizione:** T' = T
    * a &in; N t.c. `livello(a, T)` > 0
    * se |{v &in; N t.c. `padre(v, T)` = a}| = 1
    * allora T' = `scrivinodo(T, a, n)`
