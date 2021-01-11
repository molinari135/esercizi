# Esercizi
Esercizi teorici e di laboratorio di Algoritmi e Strutture Dati

## Contenuto

### Esonero 1
**Es. 1 - Estensione di una struttura dati esistente, con nuovi operatori**
Data la struttura dati **lista**, scrivere specifica sintattica e semantica di due nuovi operatori:
- **aggiungi_ad_estremi**, che aggiunge un dato elemento ad entrambi gli estremi della lista
- **rimuovi_metà**, che rimuove la prima metà (i primi n/2 elementi) della lista

**Es. 2** Descrivere brevemente le diverse implementazioni della struttura dati **Pila**, enfatizzando vantaggi e svantaggi in termini di complessità computazionale dei singoli operatori, anche attraverso esempi.

**Es. 3** Si consideri il seguente algoritmo che lavora sull'array V (costituito da n elementi). Stimare la complessità dell'algoritmo nel caso pessimo e nel caso ottimo, motivando la risposta e illustrando in quali casi l'algoritmo si trova nelle condizione ottime e pessime.

```cpp
analizza_array(int V[], int n)
{
  for (int i = 0; i < n; i++)
    cout << "Elemento:" << V[i];
  if (n%2 == 0)
  {
    for (int i = 0; i < n; i++)
      for (int j = i+1; j < n: j++)
        cout << "Vicini:" << V[i] << "," << V[j];
  }
}
```

**Es. 4 - Progettare una nuova struttura dati**
Si vuole progettare una struttura dati per la gestione di uno **sportello** alla posta.
Completare la specifica della struttura dati **sportello**, fornendo la specifica semantica per mezzo di PRE e POST condizioni, rispetto alla seguente specifica sintattica:

**domini**: sportello, cliente, intero

**operatori**:
* creaSportello() &rightarrow; sportello
  * crea lo sportello, con nessun cliente
* aggiungiCliente(sportello, cliente) &rightarrow; sportello
  * aggiunge il cliente in fila per lo sportello
* processaCliente(sportello) &rightarrow; sportello
  * processa il prossimo cliente in fila allo sportello
* contaClienti(sportello) &rightarrow; intero
  * conta i clienti ancora in fila allo sportello
* aggiungiClienteAmico(sportello, cliente) &rightarrow; sportello
  * aggiunge il cliente in fila in prima posizione

### Appello 1 - Esonero 2
**Es. 1 - Estensione di una struttura dati esistente, con nuovi operatori**
Data la struttura dati **albero binario**, scrivere specifica sintattica e semantica di due nuovi operatori (quando possibile, fare uso degli operatori esistenti dell'albero binario):
- **cambia_valore_speciale**, che dato un nodo x ed un valore v, scrive il valore v nel figlio sinistro di x, se quest'ultimo esiste, altrimenti lo scrive in x
- **incrementa_figli**, che dato un nodo x, incrementa di 1 il valore contenuto nei suoi figli

**Es. 2** Descrivere brevemente le diverse implementazioni della struttura dati **Grafo**, enfatizzando vantaggi e svantaggi in termini di complessità computazionale dei singoli operatori, anche attraverso esempi.

**Es. 3 - Progettare una nuova struttura dati**
Si vuole progettare una struttura dati per la gestione delle informazioni relative alle persone di un città insieme ai loro vicini (a distanza di 1km). Completare la specifica della struttura dati **città**, fornnendo la specifica semantica per mezzo di PRE e POST condizioni, rispetto alla seguente specifica sintattica:

**domini**: città, abitante, lista

**operatori**:
* creaCittà() &rightarrow; città
  * crea la città, inizialmente con nessun abitante
* aggiungiAbitante(città, abitante) &rightarrow; città
  * aggiunge l'abitante alla città
* indicaVicino(città, abitante, abitante) &rightarrow; città
  * memorizza il fatto che due abitanti sono vicini di casa
* ottieniVicini(città, abitante) &rightarrow; lista
  * restituisce la lista dei vicini dell'abitante indicato
* abitanteConPiùVicini(città) &rightarrow; abitante
  * restituisce l'abitante con più vicini (se non vi sono parimerito)
  
**Es. 4 - Tecniche algoritmiche**
Spiegare il problema dello zaino e descrivere un possibile algoritmo solutivo basato su tecnica greedy.

**Es. 5** Si consideri il seguente algoritmo che lavora sull'array V (costituito da n elementi). Stimare la complessità dell'algoritmo nel caso pessimo e nel caso ottimo, motivando la risposta e illustrando in quali casi l'algoritmo si trova nella condizioni ottime e pessime.

```cpp
analizza_array(int V[], int n, int val)
{
  for (int i = 0; i < n; i++)
    cout << "Elemento:" << V[i];
  if (V[0] == val)
    cout << "Elemento val in prima posizione";
  else
    for (int i = 0; i < n; i++)
      if (V[i] == val)
        cout << "Val è presente in poszione:" << i;
}
```

### Appello 2
### Appello 3
### Appello 4
### Appello 5
### Appello 6
### Appello 7
### Appello 8
