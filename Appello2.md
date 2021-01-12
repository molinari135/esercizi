# Appello 2

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

Scrivere la funzione `trasforma_in_pari` che prenda in input un albero binarioe, tramite una **visita simmetrica**:
- stampi il valore corrente del nodo visitato
- lo aggiorni, incrementandone il valore se il valore corrente è dispari
- se il nodo è stato aggiornato, stampi il nuovo valore
La funzione `trasforma_in_pari` deve restituire il numero di aggiornamenti effettuati.

Scrivere dunque il `main` che:
- crei il seguente albero di interi:

```
          [1]
         /   \
       [3]   [2]
      /   \
    [5]   [6]
```

- chiami la funzione `trasforma_in_pari`, passando l'albero in input
- stampi a video il numero di aggiornamenti effettuati

```cpp
int trasforma_in_pari(MyBinTree<T> bin, MyBinTree<T>::Nodo nodo)
{
  int upd = 0;
  visita_simmetrica(bin, bin.radice(), upd);
  return upd;
}

void visita_simmetrica(MyBinTree<T> bin, MyBinTree<T>::Nodo nodo, int upd)
{
  if (!bin.sx_vuoto(nodo)) {
    visita_simmetrica(bin, bin.sx(nodo), upd);
  }
  
  T elem = bin.leggi(nodo);
  if (elem % 2 != 0) {
    T new_elem = elem + 1;
    bin.scrivi(new_elem, nodo);
    upd = upd + 1;
  }
  
  if (!bin.dx_vuoto(nodo)) {
    visita_simmetrica(bin, bin.dx(nodo), upd);
  }
}

int main() 
{
  MyBinTree<int> bin;
  MyBinTree<int>::Nodo radice, nodo;
  
  bin.inserisci_radice(radice);
  bin.scrivi(1, radice);
  bin.inserisci_figlio_sx(radice);
  bin.scrivi(3, bin.sx(radice));
  bin.inserisci_figlio_dx(radice);
  bin.scrivi(2, bin.dx(radice));
  
  nodo = bin.sx(radice);
  bin.inserisci_figlio_sx(nodo);
  bin.scrivi(5, bin.sx(nodo));
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(6, bin.dx(nodo));
  
  int aggiornamenti = bin.trasforma_in_pari(bin, bin.radice());
  cout << "Aggiornamenti: " << aggiornamenti << endl;
  
  return 0;
}
```
