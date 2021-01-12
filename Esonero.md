# Esonero 1

## Laboratorio

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
          
  while(!L1.ultimo(indice1)) {
    T elem = L1.leggi(indice1);
    
    if (elem > 100) {
        L2.inserisci(elem, indice2);
        L1.rimuovi(indice1);
    } else {
      if (elem < 50) {
        L3.inserisci(elem, indice3);
        L1.rimuovi(indice1);
      }
    }
    
    L1.successivo(indice1);
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
