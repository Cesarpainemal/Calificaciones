# Calificaciones
package pruebaa;

public class Alternativa {

    private boolean opcion;
    
    public Alternativa(){
        this.opcion = false;
    }
    
    public Alternativa(boolean op){
        this.opcion = op;
    }

    public boolean isOpcion() {
        return opcion;
    }

    public void setOpcion(boolean opcion) {
        this.opcion = opcion;
    }
    
}
-------------------------------------

package pruebaa;

import java.util.Scanner;


public class Evaluacion {
 
    public void realizarEvalucion(Pruebaa p) {

        Scanner lectura = new Scanner(System.in);

        for (int pregunta = 0; pregunta < p.getCantidadDePreguntas(); pregunta++) {
            System.out.print("Ingrese su respuesta para la pregunta " + (pregunta + 1)
                    + "\n[1] opción a"
                    + "\n[2] opción b"
                    + "\n[3] opción c"
                    + "\n------> ");
            int resp = lectura.nextInt();
            while (resp < 1 || 3 < resp) {
                System.out.print("intente nuevamente.. ");
                resp = lectura.nextInt();
            }            
            if(resp == 1 && p.getPregunta(pregunta).getAlternativa(0).isOpcion()){
                p.agregarPuntajeObtenido(10);  
            }else if (resp == 2 && p.getPregunta(pregunta).getAlternativa(1).isOpcion()) {
                p.agregarPuntajeObtenido(10);
            } else if (resp == 3 && p.getPregunta(pregunta).getAlternativa(2).isOpcion()) {
                p.agregarPuntajeObtenido(10);
            }
        }
    }

    public static void main(String[] args) {

        int cantidadDePreguntas = 10;
        int cantidadDeAlternativas = 3;

        Evaluacion e = new Evaluacion();

        Pruebaa p1 = new Pruebaa(cantidadDePreguntas, cantidadDeAlternativas);

        e.realizarEvalucion(p1);

        p1.calcularPuntaje();

        System.out.println("la nota es:" + p1.getNota());

        for (int pregunta = 0; pregunta < p1.getCantidadDePreguntas(); pregunta++) {
            for (int alternativa = 0; alternativa < p1.getPregunta(pregunta).getCantidadAlternativas(); alternativa++) {
                if(p1.getPregunta(pregunta).getAlternativa(alternativa).isOpcion()){
                    System.out.println("pregunta "+(pregunta+1) + " respuesta "+ (alternativa+1));
                }
                
            }

        }
        System.out.println("respuestas correctas "+(p1.getPuntajeObtenido()/10));

    }
}
--------------------------------------------

package pruebaa;

import java.util.Random;


public class Pregunta {
    
    
    private final int puntaje = 10;
    private Alternativa[] alternativas;
    private int cantidadAlternativas;
    
    private void crearAlternativas(int cantAlternativas){
       
        int altCorrectas = 0; 
        Random rn = new Random();
        
        for(int i = 0; i < cantAlternativas; i++){   
            
            int auxiliar = rn.nextInt(2);
            
            Alternativa aux = new Alternativa();
            
            if(auxiliar == 1 && altCorrectas != 1){
                altCorrectas = 1;
                aux.setOpcion(true);
                this.alternativas[i] = aux;
            }
            else{
                //aux.setOpcion(true);
                this.alternativas[i] = aux;
            }
        }
    }

    public Pregunta(int cantidadAlternativas){
        this.cantidadAlternativas = cantidadAlternativas;
        this.alternativas = new Alternativa[this.cantidadAlternativas];
        crearAlternativas(this.alternativas.length);
    }

    public int getCantidadAlternativas() {
        return cantidadAlternativas;
    }

    public void setCantidadAlternativas(int cantidadAlternativas) {
        this.cantidadAlternativas = cantidadAlternativas;
    }

    public Alternativa getAlternativa(int i) {
        return this.alternativas[i];
    }
    
}   
-----------------------------------------package pruebaa;

public class Pruebaa {
    
    private Pregunta[] preguntas;
    private int puntajeTotal;
    private int puntajeObtenido;
    private int cantidadDePreguntas;
    private double nota;
    
    public Pruebaa(int cantPreguntas, int cantAlternativas){
        this.preguntas = new Pregunta[cantPreguntas];
        this.cantidadDePreguntas = cantPreguntas;
        this.puntajeTotal = this.cantidadDePreguntas * 10;
        this.puntajeObtenido = 0;
        
        crearPreguntas(cantAlternativas);
    }
    
    private void crearPreguntas(int cantidadDeAlternativas){
        for (int i = 0; i < this.cantidadDePreguntas; i++) {
            Pregunta p = new Pregunta(cantidadDeAlternativas);
            this.preguntas[i] = p;
        }
    }
    
    public void calcularPuntaje(){
        if(this.puntajeObtenido >= 60){
            this.nota = (this.puntajeObtenido * 0.06) + 1;
        }
        else{
            this.nota = (this.puntajeObtenido * 0.05) + 1;
        }
    }
    
    public Pregunta getPregunta(int i) {
        return this.preguntas[i];
    }

    public int getPuntajeTotal() {
        return puntajeTotal;
    }

    public void setPuntajeTotal(int puntajeTotal) {
        this.puntajeTotal = puntajeTotal;
    }

    public int getPuntajeObtenido() {
        return puntajeObtenido;
    }

    public void agregarPuntajeObtenido(int puntajeObtenido) {
        this.puntajeObtenido += puntajeObtenido;
    }

    public int getCantidadDePreguntas() {
        return cantidadDePreguntas;
    }

    public void setCantidadDePreguntas(int cantidadDePreguntas) {
        this.cantidadDePreguntas = cantidadDePreguntas;
    }

    public double getNota() {
        return nota;
    }

    public void setNota(double nota) {
        this.nota = nota;
    }
}
