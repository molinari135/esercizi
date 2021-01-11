# Esercizi
Esercizi teorici e di laboratorio di Algoritmi e Strutture Dati

## Esonero
Si assuma di avere una classe C++ per l'implementazione della lista:

```cpp
template <class T>
class MyList {
  public:
    typedef Nodo* position;
            
    // costruttori e distruttori
    MyList();
    ...
    // operatori
    bool vuota() const;
    T leggi(position) const;
    void write(const T &, position);
    position begin() const;
    position successivo(position) const;
    position precedente(position) const;
    void inserisci(const T &, position);
    void rimuovi(position);
    bool ultimo(position);
  private:
    ...
}
```
        
Scrivere la funzione `processa_liste` che prenda in input tre liste di interi L1, L2, ed L3, scorra tutti gli elementi della lista L1 e:
- aggiunga tutti gli elementi maggiori di 100 a L2
- aggiunga tutti gli elementi minori di 50 ad L3
- lasci solamente gli elementi compresi tra 50 e 100 (inclusi) in L1

Scrivere dunque il `main` che:
- inizializzi la lista L1 con i valori <30, 40, 50, 60, 80, 120>
- crei L2 ed L3 vuote
- invochi la funzione `processa_liste` passando L1, L2 ed L3
```cpp
template <class T> 
void processa_liste(MyList<T> &L1, MyList<T> &L2, MyList<T> &L3
{
  MyList<T>::position indice1;
  MyList<T>::position indice2;
  MyList<T>::position indice3;
          
  while(!L2.ultimo(indice2)) {
    while(!L1.ultimo(indice1) && !L2.ultimo(indice2)) {
      T elem = L1.leggi(indice1);
      if (elem > 100) {
        L2.inserisci(elem, indice2);
      }
    
      L1.successivo(indice1);
      
      if (L2.ultimo(indice2) {
        indice2 = L2.begin();
      }
      
      L2.successivo(indice2);
    }
  }
          
  while(!L3.ultimo(indice3)) {
    while(!L1.ultimo(indice1) && !L3.ultimo(indice3)) {
      T elem = L1.leggi(indice1);
      if (elem < 50) {
        L3.inserisci(elem, indice3);
      }
    
      L1.successivo(indice1);
      
      if (L3.ultimo(indice3) {
        indice3 = L3.begin();
      }
      
      L3.successivo(indice3);
    }
  }
          
int main()
{
  MyList<int> L1;
  MyList<int> L2;
  MyList<int> L3;
            
  MyList<int>::position indice1;
            
  indice1 = L1.begin();
            
  L1.inserisci(30, indice1 = L1.successivo(indice1));
  L1.inserisci(40, indice1 = L1.successivo(indice1));
  L1.inserisci(50, indice1 = L1.successivo(indice1));
  L1.inserisci(60, indice1 = L1.successivo(indice1));
  L1.inserisci(80, indice1 = L1.successivo(indice1));
  L1.inserisci(120, indice1 = L1.successivo(indice1));
            
  L1.processa_liste(L1, L2, L3);
}
```

## Esonero 2

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

Scrivere la funzione `processa_pari` che prenda in input un albero binario e:
- crei una lista
- visiti l'albero e aggiunga alla lista i valori pari contenuti nell'albero
- restituisca la lista

Scrivere dunque il `main` che:
- crei il seguente albero di interi:

```      [1]
        /   \
      [3]   [4]
     /   \    \
   [8]   [2]  [6]
```
- chiami la funzione `processa_pari`, passando l'albero in input
- stampi il contenuto della lista ottenuta come risultato

```cpp
MyList<T> processa_pari(const MyBinTree<T> &BT, MyBinTree<T>::Nodo n) 
{
  MyList<T> List;
  visita(T, n, List);
  return List;
}

void visita(MyBinTree<T> &BT, MyBinTree<T>::Nodo n, MyList<T> L) 
{
  T elem = BT.leggi(n);
  
  if (pari(BT, n)) {
    L.inserisci(elem, L.begin());
  }
  
  if (!BT.sx_vuoto(n)) {
    visita(BT, BT.sx(n), L);
  }
  
  if (!BT.dx_vuoto(n)) {
    visita(BT, BT.dx(n), L);
  }
}

bool pari(MyBinTree<T> &BT, MyBinTree<T>::Nodo n) 
{
  return visita_pari(BT, n);
}

bool visita_pari(MyBinTree<T> &BT, MyBinTree<T>::Nodo n) 
{
  T elem = BT.leggi(n);
  
  if (elem % 2 == 0) {
    return true;
  }
  
  if (!BT.sx_vuoto(n)) {
    bool check_sx = visita_pari(BT, BT.sx(n));
    if (check_sx) {
      return true;
    }
  }
  
  if (!BT.dx_vuoto(n)) {
    bool check_dx = visita_pari(BT, BT.dx(n));
    if (check_dx) {
      return true;
    }
  }
  
  return false;
}

int main()
{
  MyBinTree<int> T;
  MyBinTree<int>::Nodo radice, n;
  MyList<int> List;
  
  T.inserisci_radice(radice);
  T.scrivi(radice, 1);
  T.inserisci_figlio_sx(radice);
  T.scrivi(T.sx(radice), 3);
  T.inserisci_figlio_dx(radice);
  T.scrivi(T.dx(radice), 4);
  
  n = T.sx(radice);
  T.inserisci_figlio_sinistro(n);
  T.scrivi(T.sx(n), 8);
  T.inserisci_figlio_destro(n);
  T.scrivi(T.dx(n), 2);
  
  n = T.dx(radice);
  T.inserisci_figlio_dx(n);
  T.scrivi(T.dx(n), 6);
  
  List = T.processa_pari(T, T.radice());
}
```
