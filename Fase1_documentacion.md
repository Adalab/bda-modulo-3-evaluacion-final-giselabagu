# Módulo 3 - Ejercicio Evaluación Final

### Fase 1 - Exploración

EDA del archivo Customer Flight Activity:

    - Número de filas duplicadas: 1864. Se observa que esas filas son idénticas entre ellas (incluyendo sobre todo el id Loyalty Number y Year/Month, que son las que servirían para diferenciar unas con otras) así que se eliminan.

    - NaNs o nulos: No hay ningún nan en todo el df.

    - Loyalty Number --> identificador único para cada cliente dentro del programa de lealtad de la aerolínea.

    - Year --> solo tiene 2 valores únicos: 2017 y 2018

    - Month --> Cualquiera de todos los meses del año (1 - 12) Tiene una distribución igual para cada mes porque se han introducido datos por id cliente haya tomado vuelos o no.

    - Flights Booked --> Distribución extremadamente sesgada hacia la derecha (el 48.58% del dataset tiene 0 vuelos, solo el 25% superior supera los 8 vuelos). Distribución 'long tail'. Tiene varios ouliers que podrían estudiarse más profundamente como Next Steps.

    - Flights with Companions --> Distribución muy sesgada a la derecha. Percentil 25% = 0 --> Más del 50% de los clientes nunca volaron con acompañantes. Distribución 'long tail'. Tiene varios ouliers que podrían estudiarse más profundamente como Next Steps.

    - Total Flights --> Distribución extremadamente sesgada a la derecha. Percentil 25% = 0 --> Al menos el 25% no han volado nunca y al menos el 50% han volado como mucho 1 vez. La media es mayor porque hay un grupo más pequeño de clientes que voló muchas veces, el 25% superior viaja bastante (+10 viajes). Distribución 'long tail'. Tiene varios ouliers que podrían estudiarse más profundamente como Next Steps.

    - Distance --> Mucha diversidad en las distancias (muchos valores únicos). Distribución muy sesgada a la derecha: Percentil 25% = 0, la mediana es mucho menor que la media, la 'long tail' sube la media. Alta desviación estándard que refleja una gran dispersión. Tiene bastantes ouliers que podrían estudiarse más profundamente como Next Steps.

    - Points Accumulated --> Única columna de tipo float64. El 25% tienen 0 puntos acumulados, un cuarto de los clientes no ha acumulado puntos. La distribución está sesgada a la derecha, con unos pocos clientes acumulando muchos puntos, por eso la media es más del doble que la mediana. Alta desviación estándard que refleja una gran dispersión. El valor 0 es importante y refleja falta de participación o uso del programa. Tiene bastantes ouliers que podrían estudiarse más profundamente como Next Steps.

    - Points Redeemed --> Variable fuertemente sesgada a la derecha, mayoría sin canjes y pocos canjes grandes. El 25%, 50% y 75% percentiles son 0, lo que indica que al menos el 75% de los clientes no han canjeado puntos. La media és muy por encima de la mediana porque un pequeño grupo de clientes canjea muchos puntos. Alta desviación estándard que refleja una gran dispersión. Prácticamente se consideran outliers todos los valores diferentes de 0.

    - Dollar Cost Points Redeemed --> El 75% de los valores son 0, lo que indica que la mayoría no canjearon puntos. La media es baja (2.5) pero hay casos con costos altos de hasta 71 dólares, por eso también hay una desviación estándar alta (alta dispersión). Al igual que en 'Points Redeemed', se consideran outliers todos los valores diferentes de 0. 

    - Se comprueba que estas 3 últimas variables 'Points Redeemed', 'Dollar Cost Points Redeemed' y 'Points Accumulated' están correlacionadas, tanto los ceros como los outliers. Como conslusión, se podría añadir que más personas acumulan puntos que las que después los gastan: Points Accumulated > Points Redeemed para la mayoría de clientes.


EDA del archivo Customer Loyalty History:

    - En este df no hay filas duplicadas.

    - Loyalty Number --> identificador único para cada cliente dentro del programa de lealtad de la aerolínea.

    - Country --> Solo hay 1 país en todo el df, Canadá.

    - Province --> Las províncias con mayor frecuencia relativa son: Ontario (32.29%), British Columbia (26.34%) y Quebec (19.72%). Las que tienen una menor frecuencia relativa: Yukon (0.66%) y Prince Edward Island (0.39%). Hay un total de 11 valores únicos.

    - City --> Las ciudades con mayor frecuencia relativa son: Toronto (20.02%), Vancouver (15.43%) y Montreal (12.30%). Se consideran categorías raras (< 1.0%) 4 ciudades: Peace River (0.68%), Whitehorse (0.66%), Kelowna (0.53%), Charlottetown (0.39%). Hay un total de 29 valores únicos.

    - Postal Code --> Hay 55 categorías distintas. Estan formados por combinaciones de letras y números (categórica).

    - Gender --> Female (50.25%) y Male (49.75%).

    - Education --> 5 Categorías distintas. Frecuencias relativas (%): Bachelor (62.59%), College (25.32%), High School or Below (4.67%), Doctor (4.39%), Master (3.04%).

    - Salary --> Tiene NULLS, un 25.32% de los datos. Tiene 20 valores negativos, se considera un error de inserción de los datos y se corrigen convirtiéndolos en valores absolutos. Habrá que tomar decisiones con los Nulls posteriormente.

    - Marital Status --> 3 categorías diferentes. Frecuencias relativas (%): Married (58.16%), Single (26.79%), Divorced (15.04%).

    - Loyalty Card --> 3 categorías diferentes. Frecuencias relativas (%): Star (45.63%), Nova (33.88%), Aurora (20.49%).

    - CLV --> Tiene una desviación estándar alta, valores dispersos. Mediana menor que la media, distribución sesgada a la derecha: 'long tail'. 

    - Enrollment Type --> 2 categorías diferentes. Frecuencias relativas (%): Standard (94.2%), 2018 Promotion (5.8%).

    - Enrollment Year --> Valores discretos y limitados (2012 a 2018). La mayoría de clientes (18%) se inscribieron en el 2018. El 2012 fue el año con menor proporción (10%).

    - Enrollment Month --> Valores discretos y limitados (1 a 12). No hay nada a destacar en ningún mes en concreto, la frecuencia de cada mes es muy parecida.

    - Cancellation Year --> Tiene NULLS, un 87.65% de los datos. Es de tipo float debido a la presencia de nans. Valores únicos sin nan: 2012 - 2018. Progresivamente han ido cancelando, máximo de cancelaciones en 2018 (31.2%).

    - Cancellation Month --> Tiene NULLS, un 87.65% de los datos. Es de tipo float debido a la presencia de nans. Valores discretos y limitados (1 a 12) sin incluir nans. Se observan mayores cancelaciones sobretodo en los meses de noviembre (10.26%) y diciembre (10.30%) seguidos de cerca por agosto (10.06%). Meses con menos cancelaciones son abril (6.58%) y febrero (6.72%).



### Fase 1 - Transformación

### ANOTACIONES
- Se decide trabajar con los nombres originales de las bases de datos, incluyendo espacios y mayúsculas. Para facilitar el trabajo con dichas bbdd, se podrían convertir fácilmente si fuera necesario. Por el momento se mantienen para evitar posibles errores con bbdd ya existentes.

- Lógica de negocios: Es normal que la acumulación ('Points Accumulated') sea más granular (floats) y el canje ('Points Redeemed') sea solo en números enteros. La diferencia en tipo de dato refleja esta lógica de negocio, no es un error.

- 'Salary' tiene valores negativos, se considera un error de inserción de los datos y se pasan a valores absolutos.

- Nulls 'Cancellation Years/Month' --> son de tipo float porque hay NaNs. Estos nulos corresponden a que todavía no se ha cancelado la correspondiente subscripción, por lo que tiene sentido su existencia y se mantienen. --> NEXT STEP: Se podría crear una columna que categorice esos nulos SI/NO.

- Nulls 'Salary' --> Se observa que coinciden todos los valores nulos de salary con la categoría College de la columna Education. Teniendo en cuenta que en Canadá el orden de Educación es el siguiente (de menos a más): High School or Below --> Educación secundaria, College	Formación Profesional --> Formación profesional post-secundaria, Bachelor --> Universidad (título de grado), Master	-->	Estudios de postgrado, Doctor --> Doctorado académico. Y que está clasificación coincide con las diferencias de salario (a mayor nivel de educación, mayor salario), se determina rellenar los nulos con un valor intermedio entre la mediana de High School or Below y Bachelor. Mediana y no media porque la mediana es más robusta ante valores extremos o outliers.

- Al analizar columnas con las funciones de soporte, quedan celdas de output largas. Realizar un Run All, puede tardar varios segundos. Existe el archivo Fase1_EDA_Limpieza_SinOutputCells.ipynb, una copia del archivo original Fase1_EDA_Limpieza.ipynb sin los outputs cargados.

- La última celda del archivo Fase1_EDA_Limpieza.ipynb crea un csv final llamado customer_summary.csv donde están unidos mediante un merge (inner join) los dos csv originales ya transformados y limpios. Este nuevo archivo no está subido al repositorio para evitar una sobrecarga de peso.