# Appello 6

## Laboratorio

Si assuma di avere una classe C++ per l'implementazione di alberi binari e una per l'implementazione delle liste, che presentino le seguenti funzioni:

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

Scrivere la funzione `travasa` che prenda in input **solo** un albero binario e, tramite una **invisita** copi tutti i valori pari dell'albero in una lista e la **restituisca**.

Scrivere dunque il `main` che:
- crei il seguente albero di interi

```
            [6]
           /   \
         [3]   [2]
        /   \
      [1]   [4]
               \
               [7]
```

- chiami la funzione `travasa`, passando l'albero in input, ottenendo la lista
- stampi a video la somma degli elementi della lista

```cpp
MyList<T> travasa(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo)
{
  MyList<T> list;
  visita(bin, bin.radice(), list);
  return list;
}

void visita(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo, MyList<T> pari)
{
  T elem = bin.leggi(nodo);
  
  if (elem % 2 == 0) {
    pari.inserisci(bin.leggi(nodo), pari.begin());
  }
  
  if (!bin.sx_vuoto(nodo)) {
    visita(bin, bin.sx(nodo), pari);
  }
  
  if (!bin.dx_vuoto(nodo)) {
    visita(bin, bin.dx(nodo), pari);
  }
}

int main()
{
  MyBinTree<int> bin;
  MyBinTree<int>::Nodo radice, nodo;
  
  bin.inserisci_radice(radice);
  bin.scrivi(radice, 6);
  bin.inserisci_figlio_sx(radice);
  bin.scrivi(bin.sx(radice), 3);
  bin.inserisci_figlio_dx(radice);
  bin.scrivi(bin.dx(radice), 2);
  
  nodo = bin.sx(radice);
  bin.inserisci_figlio_sx(nodo);
  bin.scrivi(bin.sx(nodo), 1);
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(bin.dx(nodo), 4);
  
  nodo = bin.dx(nodo);
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(bin.dx(nodo), 7);
  
  MyList<int> list;
  MyList<int>::position indice;
  
  list = bin.travasa(bin, bin.radice());
  
  indice = list.begin();
  
  while(!list.ultimo(indice)) {
    cout << list.leggi(indice) << endl;
    indice = list.successivo(indice);
  }
}
