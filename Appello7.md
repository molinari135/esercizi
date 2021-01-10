# Appello 7

## Laboratorio

Si assuma di avere una classe C++ per l'implementazoine di alberi binari e una per l'implementazione delle liste, che presentino le seguenti funzioni:

```cpp
template <class T>
class MyBinTree {
  public:
    typedef int Nodo;
    
    MyBinTree();
    bool vuoto() const;
    Nodo radice() const;
    Nodo padre(Nodo) const;
    Nodo sx(Nodo) const;
    Nodo dx(Nodo) const;
    bool sx_vuoto(Nodo) const;
    bool dx_vuoto(Nodo) const;
    void inserisci_radice(Nodo);
    void inserisci_figlio_sx(Nodo);
    void inserisci_figlio_dx(Nodo);
    T leggi(Nodo) const;
    void scrivi(Nodo, const T &) const;
}
```

```cpp
template <class T>
class MyList {
  public:
    typedef Cella* position;
    
    MyList();
    bool vuota() const;
    T leggi(position) const;
    void scrivi(const T &, position);
    position begin() const;
    position successivo(position) const;
    position precedente(position) const;
    void inserisci(const T &, position);
    void rimuovi(position);
    bool ultimo(position);
}
```

Scrivere la funzione `trova_comuni` che prenda in input **due** alberi binari, copi in una lista gli elementi presenti in entrambi gli alberi e **restituisca tale lista**. Utilizzare una tecnica di visita a scelta (indicare quale visita si sta utilizzando) per individuare gli elementi presenti in entrambi gli alberi.

Scrivere dunque il `main` che:
- crei i seguenti alberi di interi:

```         
            [6]                       [7]
           /   \                     /   \
        [3]     [5]                [5]   [9]
       /   \                            /
     [1]   [4]                        [3]
     
```
- chiami la funzione `trova_comuni`, passando gli alberi in input, ottenendo la lista
- stampi a video la lista (che dovrebbe contenere i valori 3 e 5)

```cpp
MyList<T> trova_comuni(const MyBinTree<T> &T1, const MyBinTree<T> &T2)
{
  MyList<T> list;                                 // crea una lista
  previsita(bin1, bin2, bin1.radice(), list);     // effettua la visita dell'albero
  return list;                                    // restituisce la lista avvalorata
}

void previsita(const MyBinTree<T> &bin, const MyBinTree<T> &bin2, MyBinTree<T>::Nodo nodo, MyList<T> &comuni)
{
  T elemNodo = bin.leggi(nodo);                 // elemento letto dall'albero
  
  if (cerca(bin2, elemNodo)) {                  // effettua la ricerca del valore nell'albero
    comuni.inserisci(elemNodo, comuni.begin()); // se lo trova, scrive il valore nella lista
  }
    
  if (!bin.sx_vuoto(nodo)) {                    // controlla il ramo sinistro
    previsita(bin, bin2, bin.sx(nodo), comuni); // effettua la visita del ramo sinistro
  }
  
  if (!bin.dx_vuoto(nodo)) {                    // controlla il ramo destro
    previsita(bin, bin2, bin.dx(nodo), comuni); // effettua la visita del ramo destro
  }
}

bool cerca(const MyBinTree<T> &bin, T elem)
{
  return previsita_cerca(bin, bin.radice(), elem); // restituisce 1 se trova l'elemento, 0 altrimenti
}

bool previsita_cerca(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo, T elem)
{
  T elemNodo = bin.leggi(nodo);                 // elemento letto dall'albero
  
  if (elemNodo == elem) {                       // se trova l'elemento
    return true;                                // restituisce 1
  }
  
  if (!bin.sx_vuoto(nodo)) {                    // controlla il ramo sinistro
    bool check_sx = previsita_cerca(bin, bin.sx(nodo), elem);
    if (check_sx) {                             // se trova l'elemento
      return true;                              // restituisce 1
    }
  }
  
  if (!bin.dx_vuoto(nodo)) {                    // controlla il ramo destro
  bool check_dx = previsita_cerca(bin, bin.dx(nodo), elem);
  if (check_dx) {                               // se trova l'elemento
    return true;                                // restituisce 1
  }
  
  return false;                                 // se non trova l'elemento, restituisce 0
}

int main()
{
  MyBinTree<int> bin1;            // crea il primo albero binario
  MyBinTree<int>::Nodo rad, n1;   // crea il nodo "radice" e un nodo generico
  
  bin1.inserisci_radice(rad);     // crea la radice
  bin1.scrivi(rad, 6);            
  bin1.inserisci_figlio_sx(rad);  // crea il figlio sx della radice
  bin1.scrivi(bin1.sx(rad), 3);   
  bin1.inserisci_figlio_dx(rad);  // crea il figlio dx della radice
  bin1.scrivi(bin1.dx(rad), 5);   
  
  n1 = bin.sx(rad);               // si posiziona sul ramo sx della radice
  bin1.inserisci_figlio_sx(n1);   // crea il figlio sx del nodo
  bin1.scrivi(bin1.sx(n1), 1);
  bin1.inserisci_figlio_dx(n1);   // crea il figlio dx del nodo
  bin1.scrivi(bin1.dx(n1), 4);
  
  MyBinTree<int> bin2;            // crea il secondo albero binario
  
  bin2.inserisci_radice(rad);     // crea la radice
  bin2.scrivi(rad, 7);
  bin2.inserisci_figlio_sx(rad);  // crea il figlio sx della radice
  bin2.scrivi(bin2.sx(rad), 5);
  bin2.inserisci_figlio_dx(rad);  // crea il figlio dx della radice
  bin2.scrivi(bin2.dx(rad), 9);
  
  n1 = bin2.dx(rad);              // si posizione sul ramo dx della radice
  bin2.inserisci_figlio_sx(n1);   // crea il figlio sx del nodo
  bin2.scrivi(bin2.sx(n1), 3);
  
  MyList<int> comuni = trova_comuni(bin1, bin2);  // crea la lista
  
  MyList<int>::position pos = comuni.begin();
  
  while(!comuni.ultimo(pos)) {                    // stampa la lista
    cout << comuni.leggi(pos);
    pos = comuni.successivo(pos);                 // sposta il cursore sul prossimo nodo
  }
}
```
