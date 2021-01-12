Void accoda(MyList<T> &L1, MyList<T> &L2) { 	
 	Int pos1 = L1.begin();
 	Int pos2 = L2.begin();
 	Bool presente = false;
 	While(!L1.ultimo(pos1)) {
       	While(!L2.ultimo(pos2)) {
            	If(L1.leggi(pos1) == L2.leggi(pos2)) {
                 	presente = true;
            	}
       	Pos2 = L2.successivo(pos2);
}
       	If(!presente) {
            	T elemNodo = L1.leggi(pos1);
            	L2.inserisci(elemNodo, pos2)  	
       	}
 	Pos1 = L1.successivo(pos1); 	
 	}
