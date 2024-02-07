# Las Leyes de Codd

Las 12 reglas de Codd son un sistema de 13 reglas —numeradas del 0 al 12— propuestas por el creador del modelo relacional de bases de datos, Edgar F. Codd, para definir los requerimientos que un sistema de administración de base de datos ha de cumplir para poder ser considerado relacional1​ como lo son, por ejemplo, las bases de datos relacionales.

Codd se percató de que existían bases de datos en el mercado que decían ser relacionales, pero lo único que hacían era guardar la información en tablas, sin estar estas tablas literalmente normalizadas; entonces publicó las 12 reglas que un verdadero sistema relacional debería cumplir, aunque en la práctica algunas de ellas son difíciles de realizar.

## Reglas

0. **Fundamental**:  El sistema debe calificar como relacional, como base de datos, y como sistema de gestión.

    - *Se ha de poder gestionar las bases de datos exclusivamente cons sus capacidades relacionales*.

1. **Información**: Toda información debe estar representada por los valores de las posiciones de las columnas dentro de las filas de las tablas.

    - *Cada objeto en su lugar*.

2. **Acceso Garantizado**: Se garantiza que todos y cada uno de los datos de una base de datos relacional son accesibles lógicamente mediante una combinación de nombre de tabla, valor de clave primaria y nombre de columna.

3. **Valores Nulos**: Admiten los valores nulos (distintos de la cadena vacía, los blancos, los ceros o cualquier otro número) para representar la información desconocida y la inaplicable de manera sistemática e independiente del tipo de dato.

    - *Se permiten valores vacíos -> Nulos*

4. **Catalogo**: El sistema debe soportar un catalogo relacional en linea.

    - *Que siempre soporte un query*

5. **Sub-Lenguaje**: El sistema debe soportar al menos un lenguaje relacional.

    - Soportar una sintaxis lineal.
    - Puede ser usado para interactividad y dentro de programas de aplicación.
    - Soporta operaciones de definición de datos y de manipulación de datos, seguridad y limitantes de integridad.

6. **Actualización de Visitas**: Todas las visitas pueden ser actualizadas teóricamente son también actualizables por el sistema.

7. **Alto Nivel**: El sistema debe soportar al tiempo las operaciones de insertar, actualizar y borrar.

8. **Independencia de los datos**: Cambios a nivel físico no requieren cambios en las apps basadas en la estructura.

9. **Independencia Lógica**: Cambios en el nivel lógico no requieren cambios en las apps basadas en la estructura.

10. **Integridad**: Las limitaciones de integridad deben de especificarse separadamente de los programas de la aplicación y almacenada en el catalogo.

11. **Distribución**: La distribución de las porciones de la BD a varias locaciones debe ser invisible a sus usuarios.

12. **No Sub-Version**: Si el sistema provee una interfaz de bajo nivel, entonces no se puede usar para socavar el sistema.
