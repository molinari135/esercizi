# Appello 5

## Laboratorio

Si assuma di avere una classe C++ per l'implementazione di una lista, che presenti le seguenti funzioni:

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
  
Scrivere la funzione `trasforma` che prenda in input una lista ed un valore intero *x* e incrementi di *x* tutti i valori pari della lista.
  
Scrivere dunque il `main` che:
- crei la seguente lista [1, 7, 2, 4, 5, 6]
- chiami la funzione `trasforma` passando la lista in input e il valore *x* pari a 3
- stampi a video la lista modificata (che sarà dunque [1, 7, *5*, *7*, 5, *9*]
  
```cpp
void trasforma(MyList<T> list, int x)
{
  MyList<T>::position indice;
  indice = list.begin();
    
  while(!list.ultimo(indice)) {
    T elem = list.leggi(indice);
    if (elem % 2 == 0) {
      list.scrivi(elem + x, indice);
    }
  }
}
  
int main()
{
  MyList<int> list;
  MyList<int>::position indice;
  indice = list.begin();
  
  list.inserisci(1, indice = list.successivo(indice));
  list.inserisci(7, indice = list.successivo(indice));
  list.inserisci(2, indice = list.successivo(indice));
  list.inserisci(4, indice = list.successivo(indice));
  list.inserisci(5, indice = list.successivo(indice));
  list.inserisci(6, indice = list.successivo(indice));
  
  list.trasforma(list, 3);
  
  indice = list.begin();
  
  while(!list.ultimo(indice)) {
    cout << list.leggi(indice) << endl;
    indice = list.successivo(indice);
  }
}
