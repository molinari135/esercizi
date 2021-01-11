# Appello 3

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

Scrivere la funzione `trasforma_e_somma` che prenda in input un albero binario e, tramite una **previsita**:
- stampi il valore corrente del nodo visitato
- lo aggiorni, incrementandone il valore, se il valore corrente è pari
La funzione `trasforma_e_somma` deve **restituire la somma degli elementi dell'albero aggiornato**.

Scrivere dunque il `main` che:
- crei il seguente albero di interi:

```
            [6]
           /   \
         [3]    [2]
        /   \
      [1]   [4]
               \
               [7]
```

- chiami la funzione `trasforma_e_somma`, passando l'albero in input
- stampi a video la somma degli elementi dell'albero aggiornato

```cpp
int trasforma_e_somma(MyBinTree<T> &bin)
{
  int somma = 0;
  previsita(bin, bin.radice(), somma);
  return somma;
}

void previsita(MyBinTree<T> &bin, MyBinTree<T>::Nodo nodo, int &somma)
{
  T elem = bin.leggi(nodo);
  cout << "Corrente: " << elem << endl;
  
  if (elem % 2 == 0) {
    T new_elem = elem + 1;
    bin.scrivi(new_elem, nodo);
    somma = somma + new_elem;
  }
  
  if (!bin.sx_vuoto(nodo)) {
    previsita(bin, bin.sx(nodo), somma);
  }
  
  if (!bin.dx_vuoto(nodo)) {
    previsita(bin, bin.dx(nodo), somma);
  }
}

int main() 
{
  MyBinTree<int> bin;
  MyBinTree<int>::Nodo radice, nodo;
  
  bin.inserisci_radice(radice);
  bin.scrivi(6, radice);
  bin.inserisci_figlio_sx(radice);
  bin.scrivi(3, bin.sx(radice));
  bin.inserisci_figlio_dx(radice);
  bin.scrivi(2, bin.dx(radice));
  
  nodo = bin.sx(radice);
  bin.inserisci_figlio_sx(nodo);
  bin.scrivi(1, bin.sx(nodo));
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(4, bin.dx(nodo));
  
  nodo = bin.dx(nodo);
  bin.inserisci_figlio_dx(nodo);
  bin.scrivi(7, bin.dx(nodo));
  
  int valore = bin.trasforma_e_somma(bin, bin.radice());
  cout << "Valore: " << valore << endl;
  
  return 0;
}
```
