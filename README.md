# Práctica CleanCode

A continuación se corregirá el cuarto ejercicio de la primera evaluación de programación en el cual se pedía realizar un menú de opciones que permite al usuario elegir entre tres operaciones matemáticas: suma, multiplicación y conteo de números.


### Código realizado para responder el dia del examen
```
import java.util.Scanner;

/**
 * @author Francisco Jesús Da Silva Arana DAW 1º
 * @version 1
 */
public class Ejercicio04 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int opcion= 0;

        do {
            System.out.println("Elige una opción:");
            System.out.println("1. Sumar números.");
            System.out.println("2. Multiplicar números.");
            System.out.println("3. Contar números.");

            opcion = sc.nextInt();
            int n_num = 0;
            int sum = 0 ;
            int produc = 1;

            switch (opcion) {
                case 1 -> {
                    System.out.print("¿Cuántos números vamos a sumar? ");
                    n_num = sc.nextInt();
                    System.out.println("Introduce los " + n_num + " números:");
                    for (int i = 0; i < n_num; i++) {
                        sum += sc.nextInt();
                    }
                    System.out.println("Suma = " + sum);
                }
                case 2 -> {
                    System.out.print("¿Cuántos números vamos a multiplicar? ");
                    n_num = sc.nextInt();
                    System.out.println("Introduce los " + n_num + " números:");
                    for (int i = 0; i < n_num; i++) {
                        produc *= sc.nextInt();
                    }
                    System.out.println("Producto = " + produc);
                }
                case 3 -> {
                    System.out.println("Introduce números (0 para terminar):");
                    boolean exit = true;
                    int contador = 0;
                    while (exit) {
                        int num_cont = sc.nextInt();
                        if (num_cont == 0) {
                            exit = false;
                        } else {
                            contador += 1;
                        }
                    }
                    System.out.println("Has introducido " + contador + " números.");
                }
                default -> System.out.println("Opción incorrecta.");
            }

        }while (opcion != 1 && opcion !=2 && opcion !=3);

    }
}
```
### Codigo corregido usando las claves a seguir para el CleanCode

En el siguiente código se podrá observar que, a diferencia de la versión previa, se hace uso de:

1. **_Nombres significativos_**: los nombres de las variables, constantes, métodos y clases son descriptivos y significativos, lo que facilita la lectura y el entendimiento del código.

2. **_Funciones cortas:_** cada método tiene una tarea específica y no es demasiado largo, lo que hace que el código sea más legible y fácil de mantener.

3. **_Comentarios útiles:_** hay comentarios que explican lo que hace cada método y cada parte del código, lo que ayuda a entender lo que está sucediendo.

4. **_Evita la repetición:_** en lugar de repetir el mismo código varias veces, se utilizan bucles y funciones para reducir la cantidad de código y hacerlo más legible.

5. **_Modularidad:_** el código está organizado en métodos y clases, lo que hace que sea más fácil de leer, entender y mantener.

6. **_Uso de constantes:_** se utilizan constantes para representar las opciones del menú, lo que hace que el código sea más legible y evita errores tipográficos.
``` 
import java.util.Scanner;

/**
 * @author Francisco Jesús Da Silva Arana DAW 1º
 * @version 2
 */
public class CorreccionEjercicio04 {

    // Scanner para leer la entrada del usuario
    private static final Scanner scanner = new Scanner(System.in);

    // Constantes que representan las opciones del menú
    private static final int OPCION_SUMAR = 1;
    private static final int OPCION_MULTIPLICAR = 2;
    private static final int OPCION_CONTAR = 3;

    /**
     * Función principal que ejecuta el menú y llama a las funciones correspondientes.
     * El menú se repite hasta que el usuario introduce una opción válida.
     */
    public static void main(String[] args) {
        int opcion;

        do {
            imprimirMenu();
            opcion = obtenerOpcion();
            ejecutarOpcion(opcion);
        } while (!esOpcionValida(opcion));

    }

    /**
     * Imprime el menú de opciones.
     */
    private static void imprimirMenu() {
        System.out.println("Elige una opción:");
        System.out.println("1. Sumar números.");
        System.out.println("2. Multiplicar números.");
        System.out.println("3. Contar números.");
    }

    /**
     * Lee la opción elegida por el usuario.
     *
     * @return La opción elegida por el usuario.
     */
    private static int obtenerOpcion() {
        System.out.print("Introduce la opción elegida: ");
        int opcion = scanner.nextInt();
        scanner.nextLine(); // Evitar el salto de línea
        System.out.println(); // Dejar una línea en blanco para que sea más legible
        return opcion;
    }

    /**
     * Comprueba si la opción elegida por el usuario es válida.
     *
     * @param opcion La opción elegida por el usuario.
     * @return true si la opción es válida, false en caso contrario.
     */
    private static boolean esOpcionValida(int opcion) {
        return opcion >= OPCION_SUMAR && opcion <= OPCION_CONTAR;
    }

    /**
     * Ejecuta la opción elegida por el usuario.
     *
     * @param opcion La opción elegida por el usuario.
     */
    private static void ejecutarOpcion(int opcion) {
        switch (opcion) {
            case OPCION_SUMAR:
                ejecutarOpcionSumar();
                break;
            case OPCION_MULTIPLICAR:
                ejecutarOpcionMultiplicar();
                break;
            case OPCION_CONTAR:
                ejecutarOpcionContar();
                break;
            default:
                System.out.println("Opción incorrecta. Inténtalo de nuevo.");
                System.out.println(); // Dejar una línea en blanco para que sea más legible
                break;
        }
    }

    /**
     * Pide al usuario una serie de números y los suma.
     */
    private static void ejecutarOpcionSumar() {
        System.out.print("¿Cuántos números vamos a sumar? ");
        int cantidad = scanner.nextInt();
        scanner.nextLine(); // Evitar el salto de línea

        int suma = 0;
        for (int i = 1; i <= cantidad; i++) {
            System.out.print("Introduce el número " + i + ": ");
            int numero = scanner.nextInt();
            scanner.nextLine(); // Evitar el salto de línea
            suma += numero;
        }

        System.out.println("La suma de los números es: " + suma);

        System.out.println(); // Dejar una línea en blanco para que sea más legible
    }

    /**
     * Pide al usuario una serie de números y los multiplica.
     */
    private static void ejecutarOpcionMultiplicar() {
        System.out.print("¿Cuántos números vamos a multiplicar? ");
        int cantidad = scanner.nextInt();
        scanner.nextLine(); // Evitar el salto de línea

        int producto = 1;
        for (int i = 1; i <= cantidad; i++) {
            System.out.print("Introduce el número " + i + ": ");
            int numero = scanner.nextInt();
            scanner.nextLine(); // Evitar el salto de línea
            producto *= numero;
        }

        System.out.println("El producto de los números es: " + producto);
        System.out.println(); // Dejar una línea en blanco para que sea más legible
    }
    /**
     * Pide al usuario una serie de números y los cuenta.
     */
    private static void ejecutarOpcionContar() {
        int cuenta = 0;
        int numero = 1;

        System.out.println("Introduce números (0 para terminar):");
        while (numero != 0) {
            System.out.print("Introduce el número: ");
            numero = scanner.nextInt();
            scanner.nextLine(); // Evitar el salto de línea
            if (numero != 0) {
                cuenta++;
            }
        }

        System.out.println("Has introducido " + cuenta + " números.");
    }
}


 ```
