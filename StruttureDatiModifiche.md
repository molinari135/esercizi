# Estensione di una struttura dati esistente con nuovi operatori

## Appello 1
* cambia_valore_speciale(alberobin, nodo, valore) &rightarrow; alberobin
* incrementa_figli(alberobin, nodo) &rightarrow; alberobin

* cambia_valore_speciale(T, x, v) = T'
  * **Precondizione:** T = (N, A), x &in; N
  * **Postcondizione:** se sinistrovuoto(x, T) = false
    * T' = scrivinodo(v, figliosinistro(x, T), T)
    * altrimenti, T' scrivinodo(v, x, T)
* incrementa_figli(T, x) = T'
  * **Precondizione:** T = (N, A), x &in; N
  * **Postcondizione:** T' = T
    * se sinistrovuoto(x, T) = false
      * dato y = figliosinistro(x, T), T' = scrivinodo(legginodo(y, T')+1, y, T')
    * se destrovuoto(x, T) = false
      * dato z = figliodestro(x, T), T' = scrivinodo(legginodo(z, T')+1, z, T')

## Appello 2
* conta_fratelli(albero, nodo) &rightarrow; intero
* incrementa_padre(albero, nodo) &rightarrow; albero

* conta_fratelli(T, a) = n
  * **Precondizione:** T = (N, A), a &in; N
  * **Postcondizione:** se livello(a) = 0
    * allora n = 0
    * altrimenti, dato p = padre(a), n = |{u &in; N t.c. padre(u) = p}| - 1
* incrementa_padre(T, a) = T'
  * **Precondizione:** T = (N, A) AND a &in; N AND livello(a) > 0
    * al posto di livello(a) > 0 si può scrivere radice(T) != a
  * **Postcondizione:** dato p = padre(a)
    * T' = scrivinodo(T, p, legginodo(p)+1)
    
## Appello 3
* conta_figli(albero, nodo) &rightarrow; intero
* più_figli(albero) &rightarrow; nodo

* conta_figli(T, a) = n
  * **Precondizione:** T = (N, A) AND a &in; N
  * **Postcondizione:** n = |{v &in; N t.c. (a, v) &in; A}|
    * oppure, n = |{v &in; N t.c. padre(v, T) = a}|
* più_figli(T) = a
  * **Precondizione:** T = (N, A) AND T &ne; alberovuoto
  * **Postcondizione:** a &in; N t.c. &notexists; nodo x &in; N con
    * x &ne; a t.c. conta_figli(T, x) &ge; conta_figli(T, a)
    
## Appello 4
* due_figli(alberobin, nodo) &rightarrow; boolean
* nonno(alberobin, nodo) &rightarrow; nodo

* due_figli(T, a) = b
  * **Precondizione:** T = (N, A) AND a &in; N
  * **Postcondizione:** se ((sinistrovuoto(a, T) &ne; true) AND ((destrovuoto(a, T) &ne; true)
    * b = true
    * altrimenti, b = false
* nonno(T, a) = u
  * **Precondizione:** T = (N, A) AND a &in; N AND padre(pare(a, T), T) &in; N
    * conviene verificare che il livello sia almeno 2
  * **Postcondizione:** u = padre(padre(a, T), T)
  
## Appello 5
* inverti_pari_dispari(lista) &rightarrow; lista
* incrementa_estremi(lista, intero) &rightarrow; lista

* inverti_pari_dispari(l) = l'
  * **Precondizione:** l = < a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n-2</sub>, a<sub>n-1</sub>, a<sub>n</sub> > con &ge; 2
  * **Postcondizione:** se n % 2 = 0
    * allora l' = < a<sub>2</sub>, a<sub>1</sub>, a<sub>n</sub>, a<sub>n-1</sub> >
    * altrimenti l' = < a<sub>2</sub>, a<sub>1</sub>, ..., a<sub>n-1</sub>, a<sub>n-2</sub>, a<sub>n</sub> >
* incrementa_estremi(l, x) = l'
## Appello 6

## Appello 7
