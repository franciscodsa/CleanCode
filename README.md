# Práctica CleanCode

A continuación se corregirá el cuarto ejercicio de la primera evaluación de programación en el cual se pedía realizar un menú de opciones que permite al usuario elegir entre tres operaciones matemáticas: suma, multiplicación y conteo de números.


### Código realizado el día del examen
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
### Código corregido usando las claves a seguir para el CleanCode

En el siguiente código se podrá observar que, a diferencia de la versión previa, se hace uso de:

1. **_Nombres significativos_**: los nombres de las variables, constantes, métodos y clases son descriptivos y significativos, lo que facilita la lectura y el entendimiento del código.

2. **_Funciones cortas:_** cada método tiene una tarea específica y no es demasiado largo, lo que hace que el código sea más legible y fácil de mantener.

3. **_Comentarios útiles:_** hay comentarios que explican lo que hace cada método y cada parte del código, lo que ayuda a entender lo que está sucediendo.

4. **_Evita la repetición:_** en lugar de repetir el mismo código varias veces, se utilizan bucles y funciones para reducir la cantidad de código y hacerlo más legible.

5. **_Modularidad:_** el código está organizado en métodos, lo que hace que sea más fácil de leer, entender y mantener.

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
            cuenta = (numero != 0) ? cuenta + 1 : cuenta;
        }

        System.out.println("Has introducido " + cuenta + " números.");
    }
}

```


 Ahora se corregirá el primer ejercicio de la segunda evaluación de programación. En este era necesario crear una matriz de números aleatorios y luego generar una matriz de caracteres utilizando los números de la matriz anterior. Los números pares se representaban con la letra 'p' y los impares con la
letra 'i'.

### Código realizado el día del examen

```
/**
 * @author Francisco
 * @version 1
 */
public class Ejercicio01 {
    public static void main(String[] args) {
        int [][] arrNum = new int[5][5];

        for (int i = 0; i <5 ; i++) {
            for (int j = 0; j <5 ; j++) {
                arrNum [i][j]= (int)(Math.random()*10);
            }
        }

        for (int i = 0; i <5 ; i++) {
            for (int j = 0; j <5 ; j++) {
                System.out.print(arrNum [i][j] + "  ");
            }
            System.out.println();
        }

        System.out.println();

        char [][] arrChar = new char[5][5];

        for (int i = 0; i <5 ; i++) {

            for (int j = 0; j <5 ; j++) {
                if (arrNum[i][j] % 2 == 0){
                    arrChar[i][j] = 'p';
                }else{
                    arrChar[i][j] = 'i';
                }
            }

        }

        for (int i = 0; i <5 ; i++) {
            for (int j = 0; j <5 ; j++) {
                System.out.print(arrChar [i][j] + "  ");
            }
            System.out.println();
        }




    }
}

```
### Código corregido usando las claves a seguir para el CleanCode
Los cambios realizados fueron:

1. Se agregaron comentarios para explicar el propósito de cada método y para documentar la versión y el autor del programa.
2. Se extrajeron los bucles de impresión del arreglo a dos métodos separados para reducir la duplicación de código.
3. Se utilizó una constante TAMAÑO_ARRAY para indicar el tamaño del array, lo que hace que sea fácil de cambiar en el futuro si es necesario.
4. Se utilizó el operador ternario ```? :``` para simplificar la lógica de conversión de números pares e impares a caracteres 'p' e 'i'.
5. Se reestructuró el código a una manera modular para facilitar su lectura y mantenimiento.
```
/**
 * Esta clase contiene un programa que crea una matriz de números aleatorios y luego genera una matriz de caracteres
 * utilizando los números de la matriz anterior. Los números pares se representan con la letra 'p' y los impares con la
 * letra 'i'.
 * @author Francisco
 * @version 2
 */
public class CorreccionEjercicio01 {
    private static final int TAMAÑO_ARRAY = 5;

    /**
     * El método main es el punto de entrada del programa.
     *
     * @param args Los argumentos de la línea de comandos, no se usan en este programa.
     */
    public static void main(String[] args) {
        int[][] intArray = new int[TAMAÑO_ARRAY][TAMAÑO_ARRAY];
        char[][] charArray = new char[TAMAÑO_ARRAY][TAMAÑO_ARRAY];

        //Llena un array de números aleatorios y lo imprime
        llenarArray(intArray);
        imprimirArray(intArray);
        //Genera un array de caracteres a partir del array de enteros
        generarArray(intArray, charArray);
        imprimirArray(charArray);
    }

    /**
     * Este método llena una matriz de números aleatorios.
     *
     * @param array La matriz a llenar con números aleatorios.
     */
    private static void llenarArray(int[][] array) {
        for (int i = 0; i < TAMAÑO_ARRAY ; i++) {
            for (int j = 0; j < TAMAÑO_ARRAY ; j++) {
                array[i][j] = (int)(Math.random() * 10);
            }
        }
    }

    /**
     * Este método genera una matriz de caracteres a partir de una matriz de números. Los números pares se representan
     * con la letra 'p' y los impares con la letra 'i'.
     *
     * @param intArray La matriz de números a utilizar para generar la matriz de caracteres.
     * @param charArray La matriz de caracteres a generar.
     */
    private static void generarArray(int[][] intArray, char[][] charArray) {
        for (int i = 0; i < TAMAÑO_ARRAY ; i++) {
            for (int j = 0; j < TAMAÑO_ARRAY ; j++) {
                //if-else simplificado y legible haciendo uso de expresión ternaria
                charArray[i][j] = (intArray[i][j] % 2 == 0) ? 'p' : 'i';
            }
        }
    }

    /**
     * Este método imprime un array de caracteres en la consola.
     *
     * @param array La matriz a imprimir.
     */
    private static void imprimirArray(char[][] array) {
        for (int i = 0; i < TAMAÑO_ARRAY ; i++) {
            for (int j = 0; j < TAMAÑO_ARRAY ; j++) {
                System.out.print(array[i][j] + "  ");
            }
            System.out.println();
        }
    }

    /**
     * Este método imprime un array de números en la consola.
     *
     * @param array La matriz a imprimir.
     */
    private static void imprimirArray(int[][] array) {
        for (int i = 0; i < TAMAÑO_ARRAY ; i++) {
            for (int j = 0; j < TAMAÑO_ARRAY ; j++) {
                System.out.print(array[i][j] + "  ");
            }
            System.out.println();
        }
        System.out.println();
    }
}


```
