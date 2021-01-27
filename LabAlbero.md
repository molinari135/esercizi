Scrivere la funzione *trasforma* che prenda in input un albero n-ario e un intero *k* e, tramite una funzione:
* Stampi il valore corrente del nodo visitato
* Se il nodo ha al più *k* figli, ne incrementi il valore

```cpp
int trasforma(MyTree<int> &T, int k)
{
  int somma = 0;
  previsita(T, T.radice(), k, somma);
  return somma;
}

void previsita(MyBin<int> &T, MyBin<int>::Nodo n, int k, int somma)
{
  cout << "Elemento corrente: " << T.leggi(n);
  
  int num_figli = 0;
  if (!T.foglia(n)) {                                   // se il nodo non è una foglia
    MyTree<int>::Nodo app = T.primofiglio(n);           // crea un elemento di appoggio di tipo Nodo 
    while (!T.ultimofratello(app) && num_figli <= k) {  // mentre il Nodo di appoggio non è l'ultimo fratello e il numero dei figli è minore o uguale di k
      num_figli++;                                      // incrementa il numero dei figli trovati
      app = T.succfratello(app);                        // spostati sul prossimo fratello
    }
  }
  
  if (num_figli <= k) {                                 // se il numero dei figli è minore o uguale a k
    T.scrivi(n, T.leggi(n)+1);                          // incrementa il valore del nodo letto
    somma += T.leggi(n);                                // aggiungi alla somma il valore incrementato
  }
  
  if (!T.foglia(n)) {                                   // spostati sul prossimo fratello
    MyTree<int>::Nodo app = T.primofiglio(n);
    while (!T.ultimofratello(app)) {
      previsita(T, app, k, somma);                      // e ripeti
      app = T.succfratello(app);
    }
  }
}
```
