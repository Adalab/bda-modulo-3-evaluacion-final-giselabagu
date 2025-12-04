# Módulo 3 - Ejercicio Evaluación Final

### Fase 2 - Análisis y Visualización

Para realizar el análisis de la Fase 2, es necesario tener el archivo csv final generado por la última celda del archivo Fase1_EDA_Limpieza.ipynb, llamado customer_summary.csv. Corresponde a la unión mediante un merge (inner join) de los dos csv originales ya transformados y limpios. Este nuevo archivo no está subido al repositorio para evitar una sobrecarga de peso.

#### Usando las herramientas de visualización que has aprendido durante este módulo, contesta a las siguientes gráficas usando la mejor gráfica que consideres:  

1. ¿Cómo se distribuye la cantidad de vuelos reservados por mes durante el año?

Mediante las gráficas boxplot y barplot se observa que:
- La demanda de vuelos no es constante a lo largo del año.
- Los meses con mayor número de vuelos reservados destacan (junio, julio, agosto y diciembre), lo que podría reflejar temporadas altas asociadas a vacaciones.
- Los meses con menor volumen pueden corresponder a temporadas bajas (enero, febrero, marzo, abril, noviembre).

Esta visualización permite identificar patrones estacionales en las reservas de vuelo, información útil para tomar decisiones relacionadas con la planificación operativa, marketing, análisis de comportamiento de clientes, etc.


2. ¿Existe una relación entre la distancia de los vuelos y los puntos acumulados por los cliente?

Analizando el scatterplot (gráfico de dispersión que muestra si hay correlación positiva, negativa o ninguna entre variables numéricas), podemos observar claramente 4 líneas de correlación positiva entre 'Puntos acumulados' y 'Distancia volada'.
Por lo tanto, para entender qué variable está relacionada con la división clara de líneas, se valoran diversas opciones aplicándolas como hue en la misma gráfica. 

Claramente, la variable 'Loyalty Card' es la que encaja, por lo que se podría decir que distintos tipos de tarjetas tienen reglas o beneficios diferentes que generan esas líneas.
- Aurora --> acumula puntos de forma mucho más rápida por cada unidad de distancia volada (pendiente mayor).
- Nova --> acumula puntos más lentamente que Aurora pero más rápidamente que Star.
- Star --> sería la opción de las 3 tarjetas que acumula puntos más lentamente.
- Para terminar, la línea más baja y menos definida podría ser un grupo residual o mezcla de clientes que acumulan puntos de manera más baja o irregular. 
Next steps: Analizar el origen de esta 4a línea.

3. ¿Cuál es la distribución de los clientes por provincia o estado?

- Ontario es la provincia con más clientes, con 130,258 registros.
- Le sigue British Columbia con 106,442 clientes.
- Luego está Quebec con 79,573 clientes.
- Provincias como Alberta, Manitoba y New Brunswick tienen cantidades menores, pero aún significativas (entre 15,000 y 23,000).
- Otras provincias como Nova Scotia, Saskatchewan, Newfoundland, Yukon y Prince Edward Island tienen menos clientes, con cifras que van desde alrededor de 1,500 hasta poco menos de 13,000.

En términos porcentuales, Ontario, British Columbia y Quebec concentran la mayor parte de la clientela, mostrando una clara concentración geográfica.

4. ¿Cómo se compara el salario promedio entre los diferentes niveles educativos de los clientes?

- Hay una tendencia clara: A medida que aumenta el nivel educativo, también lo hace el salario promedio. Esto es consistente con la teoría y estudios laborales habituales.

- Salario imputado para College: Hay que recordar que el salario para College fue imputado (por ausencia de datos reales) y está justo entre High School or Below y Bachelor, lo que tiene sentido considerando que el nivel educativo College se sitúa entre esos dos.

- Gran salto en Doctorado: El salario promedio para la categoría Doctor es significativamente mayor, lo que refleja el alto valor que suele tener un doctorado en términos salariales.

5. ¿Cuál es la proporción de clientes con diferentes tipos de tarjetas de fidelidad? 

- Cada cliente tiene un tipo de Loyalty Card (Star, Nova, Aurora).
- Al contar cuántos clientes hay en cada categoría y convertirlo a porcentaje, podemos ver qué tan común o popular es cada tipo de tarjeta.
- Esto nos da una idea clara de la composición del programa de lealtad en términos de participación por tipo de tarjeta.

- Star: Es la categoría con mayor proporción de clientes, representando aproximadamente el 45.5% del total. Esto indica que casi la mitad de los clientes están inscritos en este nivel del programa de lealtad.
- Nova: Ocupa la segunda posición con un 33.9% de los clientes. Aunque es menor que Star, sigue siendo una parte importante de la base de clientes.
- Aurora: Representa el 20.6% restante, siendo el nivel con menor proporción de clientes dentro del programa.

Esta distribución sugiere que la mayoría de los clientes se encuentran en los niveles intermedios (Star y Nova), mientras que Aurora representa un grupo más pequeño. Esta información puede ayudar a enfocar estrategias de marketing y promociones específicas según el nivel de fidelidad de los clientes.

Next Steps: Se podría analizar si tienen relación los outliers que habíamos visto en la Fase 1 de clientes que realizan muchas reservas de vuelos/ recorren mucha distancia de vuelos con la tarjeta de fidelidad Aurora.

6. ¿Cómo se distribuyen los clientes según su estado civil y género?

Podemos ver estos datos de diferentes maneras, pero llegando a las mismas conclusiones:
- No hay diferencias notables entre géneros.
- Aproximadamente un 15% son divorciadas/os, un 58% son casadas/os y un 27% solteras/os.

- Hay 30,634 mujeres divorciadas y 30,128 hombres divorciados.
- La categoría más grande es la gente casada, con casi el mismo número de hombres (117,482) y mujeres (117,363).
- El grupo de solteros también es equilibrado, con alrededor de 54,760 mujeres y 53,393 hombres.

- Entre los Divorciados, el 50.42% son mujeres y el 49.58% son hombres.
- Entre los Casados, el 49.97% son mujeres y el 50.03% son hombres.
- Entre los Solteros, el 50.63% son mujeres y el 49.37% son hombres.

- El 15.11% del total son mujeres divorciadas, el 14.99% del total son hombres divorciados.
- El 57.88% del total son mujeres casadas, el 58.45% del total son hombres casados.
- El 27.01% del total son mujeres solteras, el 26.56% del total son hombres solteros.
