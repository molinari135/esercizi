# Progettare una nuova struttura dati

## Appello 1
**Specifica semantica**
* **città**: insieme di tutti i possibili grafi non orientati G = (N, A) con N insieme finito di elementi di tipo abitante e A sottoinsieme di N x N
* **abitante**: insieme finito qualsiasi
* **lista**: insieme di tutte le possibili liste < a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> > di elementi di tipo abitante

* `creaCittà() = G`
  * **Precondizione:** *nessuna*
  * **Postcondizione:** G = (N, A), N = { }, A = { }
* `aggiungiAbitante(G, a) = G'`
  * **Precondizione:** G = (N, A), a &notin; N
  * **Postcondizione:** G = (N', A) con N' = N &cup; {a}
* `indicaVicino(G, a1, a2) = G'`
  * **Precondizione:** G = (N, A), a1 &in; N, a2 &in; N
  * **Postcondizione:** G = (N, A') con A' = A &cup; {(a1, a2), (a2, a1)}
* `ottieniVicini(G, a) = l`
  * **Precondizione:** G = (N, A), a &in; N
  * **Postcondizione:** l = lista che contiene una e una sola volta gli elementi dell'insieme
    * {v &in; N t.c. (a, v) &in; A OR (v, a) &in; A}
* `abitanteConPiùVicini(G) = a`
  * **Precondizione:** G = (N, A), `vuoto(G)` = false
  * **Postcondizione:** a &in; N t.c. &notexists; v &in; N con v &ne; a t.c.
    * |ottieniVicini(G, v)| &ge; |ottieniVicini(G, a)|
    
## Appello 2
**Specifica semantica**
* **socialnet**: insieme di tutti i possibili gradi orientati G = (N, A), con N sottoinsieme finito di elementi di tipo utente e A sottoinsieme di N x N
* **utente**: insieme finito qualsiasi
* **lista**: insieme di tutte le possibili liste < a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> > di elementi di tipo utente

* `creaSocialNetwork() = G`
  * **Precondizione:** *nessuna*
  * **Postcondizione:** G = (N, A), N = { }, A = { }
* `aggiungiUtente(G, u) = G'`
  * **Precondizione:** G = (N, A), a &notin; N
  * **Postcondizione:** G = (N', A) con N' = N &cup; {a}
* `aggiungiFollower(G, u1, u2) = G'`
  * **Precondizione:** G = (N, A), u1 &in; N, u2 &in; N
  * **Postcondizione:** G = (N, A') con A' = A &cup; {(u1, u2)}
* `ottieniFollower(G, u) = l`
  * **Precondizione:** G = (N, A), u &in; N
  * **Postcondizione:** l = lista che contiene una e una sola volta gli elementi dell'insieme
    * {v &in; N t.c. (v, u) &in; A}
* `utentiPiùSeguiti(G, n) = l`
  * **Precondizione:** G = (N, A), n > 0
  * **Postcondizione:** l = < u1, u2, ..., un > con
    * |ottieniFollower(G, ui)| > |ottieniFollower(G, u(i+1))|
    * &forall; i che va da 1 a n-1
    * AND &notexists; v &in; N &ne; u1, u2, ..., un t.c.
    * |ottieniFollower(G, v)| > |ottieniFollower(G, un)|
    
## Appello 3
**Specifica semantica**
* **scacchiera**: insieme di possibili matrici n x m di caselle, ciascuna delle quali può essere occupata da elementi di tipo giocatore (pedina) oppure vuota
* **giocatore**: pedina, elemento che popola la scacchiera
* **posizione**: coppia di coordinate (i per l'indice delle righe, j per l'indice delle colonne)

* `creaScacchiera(n, m) = S`
  * **Precondizione:** P = (r, c) con r &le; n, c &le; m
  * **Postcondizione:** S'(r, c) = G
    * &forall; i = 1, 2, ..., n
    * &forall; j = 1, 2, ..., m
    * con (i, j) &ne; (r, c) allora S'(i, j) = S(i, j)
* `spostaPedina(S, P1, P2) = S'`
  * **Precondizione:** P1 = (r1, c1=, con r1 &le; n e c1 &le; m non mi va di fare questo esercizio, scusate
  
## Appello 4
**Specifica semantica**
* **catena**: insieme di tutte le possibili sequenze di analli accessibili soltanto in testa o in coda
* **anello**: {RO, GI, VE}
* **posizione**: {T, C}

* `creaCatena(a) = C`
  * **Precondizione:** *nessuna*
  * **Postconizione:** C = < a >
* `aggiungiAnello(C, a, pos) = C'
  * **Precondizione:** C = < a1, a2, ..., an >
    * pos = T AND
      * (a = GI OR a = RO AND (a1 = RO OR a1 = GI) OR a = VE AND (a1 = VE OR a1 = GI))
    * pos = C AND
      * (a = GI OR a = RO AND (an = RO OR an = GI) OR a = VE AND (an = VE OR an = GI))
  * **Postcondizione:** se pos = T
    * allora c' = < a, a1, a2, ..., an >
    * altrimenti c' = < a1, a2, ..., an, a >
* `rimuoviAnello(C, pos) = C'`
  * **Precondizione:** c = < a1, a2, ..., an > con n > 0
  * **Postcondizione:** se pos = T
    * allora c' = < a2, a3, ..., an >
    * altrimenti c' = < a1, a2, ..., a(n-1) >
* `scambiaEstremi(C) = C'`
  * **Precondizione:** c = < a1, a2, ..., an > con n &ge; 2
    * (a2 = an OR a2 = GI OR an = G1)
    * AND (a1 = a(n-1) OR a1 = GI OR a(n-1) = GI)
  * **Postcondizione:** c' = < an, a2, a3, ..., a(n-1), a1 >
  
## Appello 5
**Specifica semantica**
* **catena**: insieme di tutte le possibili sequenze di anelli accessibili soltanto in testa o in coda
* **anello**: {TO, Q, TR}
* posizione: {T, C}

* `creaCatena(a) = C`
  * **Precondizione:** *nessuna*
  * **Postcondizione:** C = < a >
* `aggiungiAnello(C, a, pos) = C'
  * **Precondizione:** C = < a1, a2, ..., an >
    * pos = T AND
      * (a = TO OR a = Q AND (a1 = Q OR a1 = TO) OR a = TR AND (a1 = TR OR a1 = TO))
    * pos = C AND
      * (a = TO OR a = Q AND (an = Q OR an = TO) OR a = TR AND (an = TR OR an = TO))
  * **Postcondizione:** se pos = T
    * allora c' = < a, a1, a2, ..., an >
    * altrimenti c' = < a1, a2, ..., an, a >
* `rimuoviAnello(C, pos) = C'`
  * **Precondizione:** C = < a1, a2, ..., an > con n > 0
  * **Postcondizione:* se pos = T
    * allora C' = < a2, a3, ..., an >
    * altrimenti C' = < a1, a2, ..., a(n-1) >
* `scambiaEstremi(C) = C'`
  * **Precondizione:** C = < a1, a2, ..., an > con n &ge; 2
    * (a2 = an OR a2 = TO OR an = TO)
    * AND (a1 = a(n-1) OR a1 = TO OR a(n-1) = TO)
    
## Appello 6
**Specifica semantica**
* **rete**: insieme di tutti i possibili grafi non orientati G = (N, A) con N insieme finito di elementi di tipo nodo e A sottoinsieme di N x N
* **nodo**: insieme finito qualsiasi
* **lista**: insieme di tutte le possibili liste < a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> > di elementi di tipo nodo

* `creaRete() = G`
  * **Precondizione:** *nessuna*
  * **Postcondizione:** G = (N, A), N = { }, A = { }
* `aggiungiNodo(G, a) = G'`
  * **Precondizione:** G = (N, A), a &notin N
  * **Postcondizione:** G' = (N', A) con N' = N &cup; {a}
* `aggiungiLinea(G, a1, a2) = G'`
  * **Precondizione:** G = (N, A), a1 &in; N, a2 &in; N
  * **Postcondizione:** G' = (N, A') con A' = A &cup; {(a1, a2), (a2, a1)}
* `ottieniCollegati(G, a) = l`
  * **Precondizione:** G = (N, A), a &in; N
  * **Postcondizione:** l = lista che contiene una e una sola volta gli elementi dell'insieme
    * {v &in; N t.c. (a, v) &in; A OR (v, a) &in; N}
* `almenoKConnessioni(G, num) = l`
  * **Precondizione:** G = (N, A), num > 0
  * **Postcondizione:** l = lista che contiene una e una sola volta gli elementi dell'insieme
    * {v &in; N t.c. |ottieniCollegati(G, v)| &ge; num
    
## Appello 7
**Specifica semantica**
* **catena**: insieme di tutte le possibili sequenze di anelli accessibili soltanto in testa
* **anello**: {TO, Q, TR}
* **posizione**: {T}

* `creaCatena(a) = C`
  * **Precondizione:** a &ne; TO
  * **Postcondizione:** C = < a >
* `aggiungiAnello(C, a) = C'`
  * **Precondizione:** C = < a1, a2, ..., an > con n &ge; 0
    * (n = 0 AND a &ne; TO) 
    * AND (n > 0 AND ((a = TO AND n &ge; 3) OR (a = TR AND (a1 = TR OR a1 = TO) OR (a1 = Q OR a1 = TO)))
  * **Postcondizione:** C' = < a, a1, a2, ..., an >
* `rimuoviAnello(C) = C'`
  * **Precondizione:** C = < a1, a2, ..., an > con n > 0
  * **Postcondizione:** C' = < a2, a3, ..., an >
* `contaTondi(C) = num`
  * **Precondizione:** C = < a1, a2, ..., an > con n > 0
  * **Postcondizione:** num = |a1, 1 &le; i &le; n t.c. ai = TO}|
