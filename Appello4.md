# Appello 4

## Laboratorio

Si assuma di avere una classe C++ per l'implementazione di alberi binari, che presenti le seguenti funzioni:

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

Scrivere la funzoine `trasforma` che prenda in input un albero binario e, tramite una **visita simmetrica**:
- stampi il valore corrente del nodo visitato
- se il nodo ha al più un figlio, ne incrementi il valore
La funzione `trasforma` deve **restituire la somma dei valori degli elementi aggiornati dall'albero**.

Scrivere dunque il `main` che:
- crei il seguente albero di interi:

```
          [3]
         /   \
       [5]   [5]
      /   \
    [2]   [1]
            \
            [4]
```

- chiami la funzione `trasforma` passando l'albero in input
- stampi a video il valore restituito dalla funzione `trasforma`

```cpp
int trasforma(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo)
{
  int value = 0;
  visita(bin, bin.radice(), value);
  return value
}

void visita(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo, int value)
{ 
  if (!bin.sx_vuoto(nodo)) {
    visita(bin, bin.sx(nodo), value);
  }
  
  T elem = bin.leggi(nodo);
  cout << "Corrente: " << elem << endl;
  
  if (bin.sx_vuoto(nodo) || bin.dx_vuoto(nodo)) {
    T new_elem = elem + 1;
    bin.scrivi(nodo, new_elem);
    value = value + new_elem;
  }
  
  if (!bin.dx(nodo)) {
    visita(bin, bin.dx(nodo));
  }
}
```
