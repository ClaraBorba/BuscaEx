# BuscaEx
Terceira Atividade de Grafos

import java.util.LinkedList;
import java.util.Queue;

public class BuscaEmExtensao {
    private ListaAdjacente lista;
    private int cor[];
    private int d[];
    private int ante[];

    public BuscaEmExtensao(ListaAdjacente lista) {
        this.lista = lista;
        cor = new int[lista.numeroV()];
        d = new int[lista.numeroV()];
        ante = new int[lista.numeroV()];
    }

    public void preencherVetores() {
        for(int i = 0; i < cor.length ; i++) {
            cor[i] = 0;    //branco
            d[i] = -1;    //infinito
            ante[i] = -1;
        }
    }

    public void busca(Vertice vertice) {
        Vertice atual;
        Vertice v;
        preencherVetores();
        int i,x;  // getNext
        Queue fila = new LinkedList();
        cor[vertice.getNumero()] = 1; //cinza
        d[vertice.getNumero()] = 0; //inicial
        fila.add(vertice);

        while(!fila.isEmpty()) {
            atual = (Vertice) fila.remove();
            v = (Vertice) lista.getLista().get(atual.getNumero()).get(0);
            i = 0;

            while(v != null) {
                if(cor[v.getNumero()] == 0) {
                    fila.add(v);
                    cor[v.getNumero()] = 1;
                    d[v.getNumero()] = d[atual.getNumero()] + 1;
                    ante[v.getNumero()] = atual.getNumero();
                    i++;
                    if(i < lista.getLista().get(atual.getNumero()).size()) {
                        v = (Vertice) lista.getLista().get(atual.getNumero()).get(i);
                    } else {
                        v = null;
                    }
                } else {
                    i++;
                    if(i < lista.getLista().get(atual.getNumero()).size()) {
                        v = (Vertice) lista.getLista().get(atual.getNumero()).get(i);
                    } else {
                        v = null;
                    }
                }
            }

            cor[atual.getNumero()] = 2;     // preto
        }
    }
}
