# tarea2-programacion
equipo de fútbol java
+----------------+     +-------------------+
|   Persona      |     |     Jugable       |
+----------------+     +-------------------+
| - nombre       |     | + jugar()         |
| - edad         |     +-------------------+
+----------------+              ^
         ^                      |
         |                      |
+----------------+     +-------------------+
|   Miembro      |     |      Jugador      |
+----------------+     +-------------------+
| - id           |     | - posicion        |
| + entrenar()   |     | + atacar()        |
+----------------+     | + defender()      |
         ^             +-------------------+
         |                      ^
         |                      |
+----------------+     +-------------------+
|  Entrenador    |     |     Delantero     |
+----------------+     +-------------------+
| - experiencia  |     | + hacerGol()      |
| + dirigir()    |     +-------------------+
+----------------+
                        +-------------------+
                        |     Defensor      |
                        +-------------------+
                        | + tacklear()      |
                        +-------------------+
                        
interface Jugable {
    void jugar();
}

class Persona {
    protected String nombre;
    protected int edad;

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}

// Clase Miembro que hereda de Persona
abstract class Miembro extends Persona {
    protected int id;

    public Miembro(String nombre, int edad, int id) {
        super(nombre, edad);
        this.id = id;
    }

    public abstract void entrenar();
}

// Clase Entrenador que hereda de Miembro
class Entrenador extends Miembro {
    private int experiencia;

    public Entrenador(String nombre, int edad, int id, int experiencia) {
        super(nombre, edad, id);
        this.experiencia = experiencia;
    }

    @Override
    public void entrenar() {
        System.out.println(nombre + " esta dirigiendo el entrenamiento.");
    }

    public void dirigir() {
        System.out.println(nombre + " esta dirigiendo el partido.");
    }
}

// Clase Jugador que hereda de Miembro 
abstract class Jugador extends Miembro implements Jugable {
    protected String posicion;

    public Jugador(String nombre, int edad, int id, String posicion) {
        super(nombre, edad, id);
        this.posicion = posicion;
    }

    public abstract void atacar();
    public abstract void defender();

    @Override
    public void jugar() {
        System.out.println(nombre + " esta jugando como " + posicion);
    }

    @Override
    public void entrenar() {
        System.out.println(nombre + " esta entrenando.");
    }
}

// Clase Delantero que hereda de Jugador
class Delantero extends Jugador {
    public Delantero(String nombre, int edad, int id) {
        super(nombre, edad, id, "Delantero");
    }

    @Override
    public void atacar() {
        System.out.println(nombre + " esta atacando.");
    }

    @Override
    public void defender() {
        System.out.println(nombre + " esta ayudando en defensa.");
    }

    public void hacerGol() {
        System.out.println(nombre + " ha marcado un gol");
    }
}

// Clase Defensor que hereda de Jugador
class Defensor extends Jugador {
    public Defensor(String nombre, int edad, int id) {
        super(nombre, edad, id, "Defensor");
    }

    @Override
    public void atacar() {
        System.out.println(nombre + " esta subiendo al ataque.");
    }

    @Override
    public void defender() {
        System.out.println(nombre + " esta defendiendo.");
    }

    public void tacklear() {
        System.out.println(nombre + " ha realizado un tackle.");
    }
}

// Clase principal 
public class EquipoFutbol {
    public static void main(String[] args) {
        Entrenador entrenador = new Entrenador("Pep Guardiola", 50, 1, 20);
        Delantero delantero = new Delantero("Lionel Messi", 34, 10);
        Defensor defensor = new Defensor("Sergio Ramos", 35, 4);

        // polimorfismo 
        Miembro[] miembros = {entrenador, delantero, defensor};
        for (Miembro miembro : miembros) {
            miembro.entrenar();
        }

        System.out.println("\nAcciones especificas:");
        entrenador.dirigir();
        delantero.jugar();
        delantero.hacerGol();
        defensor.jugar();
        defensor.tacklear();
    }
}
