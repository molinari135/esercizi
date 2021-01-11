# Appello 1

## Laboratorio

Si assuma di avere una classe C++ per l'implementazione di alberi binari e una per l'implementazione di una lista, che presentino le seguenti funzioni:

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
    void inserisci(Nodo, const T &) const;
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

Scrivere la funzione `processa_pari` che prenda in input un albero binario e:
- crei una lista
- visiti l'albero (con una strategia di visita a scelta) e aggiunga alla lista i valori pari contenuti nell'albero
- restituisca la lista

Scrivere dunque il `main` che:
- crei il seguente albero di interi:

```
            [1]
           /   \
         [3]   [4]
        /   \     \
      [8]   [2]   [6]
```

- chiami la funzione `processa_pari`, passando l'albero in input
- stampi il contenuto della lista ottenuta come risultato

```cpp
MyList<T> processa_pari(const MyBinTree<T> &bin)
{
  MyList<T> list;
  previsita(bin, bin.radice(), list);
  return list;
}

void previsita(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo, MyList<T> &list)
{
  T elem = bin.leggi(nodo);
  
  if (cerca_pari(bin)) {
    list.inserisci(elem, begin());
  }
  
  if (!bin.sx_vuoto(nodo)) {
    previsita(bin, bin.sx(nodo), list);
  }
  
  if (!bin.dx_vuoto(nodo)) {
    previsita(bin, bin.dx(nodo), list);
  }
}

bool cerca_pari(MyBinTree<T> &bin)
{
  return previsita_pari(bin, bin.radice());
}

bool previsita_pari(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo)
{
  T elem = bin.leggi(nodo);
  
  if (elem % 2 == 0) {
    return true;
  }
  
  if (!bin.sx_vuoto(nodo)) {
    bool check_sx = previsita_pari(bin, bin.sx(nodo);
    if (check_sx) {
      return true;
    }
  }
  
  if (!bin.dx_vuoto(nodo)) {
    bool check_dx = previsita_pari(bin, bin.dx(nodo));
    if (check_dx) {
      return true;
    }
  }
  
  return false;
}

int main() 
{
  MyBinTree<int> bin;
  MyBinTree<int> radice, nodo;
  
  bin.inserisci_radice(radice);
  bin.scrivi(1, radice);
  bin.inserisci_figlio_sx(radice);
  bin.scrivi(3, bin.sx(radice));
  bin.inserisci_figlio_dx(radice);
  bin.scrivi(4, bin.dx(radice));
  
  nodo = bin.sx(radice);
  bin.inserisci_figlio_sx(nodo);
  bin.scrivi(8, bin.sx(nodo));
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(2, bin.dx(nodo));
  
  nodo = bin.dx(radice);
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(6, bin.dx(nodo));
  
  MyList<int> list;
  list = bin.processa_pari(bin, bin.radice());
  
  MyList<int>::position pos;
  while(list.ultimo(pos)) {
    cout << list.leggi(pos) << endl;
    pos = list.successivo(pos);
  }
  
  return 0;
}
```
