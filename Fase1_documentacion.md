# Módulo 3 - Ejercicio Evaluación Final

### PREGUNTAS PILI
- Arreglar las bbdd? nombres columnas minúscula y sin espacios?

- Points Accumulated es de tipo float, sí que hay algunos valores con decimales, tienen sentido? (ejemplo: np.float64(16.2), np.float64(16.25))

- Confirmar lógica de negocios: Es normal que la acumulación sea más granular (floats) y el canje sea solo en números enteros. La diferencia en tipo de dato refleja esta lógica de negocio, no es un error.

### Fase 1 - Exploración

EDA del archivo Customer Flight Activity:

    - Número de filas duplicadas: 1864. Se observa que esas filas son idénticas entre ellas (incluyendo sobre todo el id Loyalty Number y Year/Month, que son las que servirían para diferenciar unas con otras) así que se eliminan.

    - NaNs o nulos: No hay ningún nan en todo el df.

    - Loyalty Number --> identificador único para cada cliente.

    - Year --> solo tiene 2 valores únicos: 2017 y 2018

    - Month --> Cualquiera de todos los meses del año (1 - 12) Tiene una distribución igual para cada mes porque se han introducido datos por id cliente haya tomado vuelos o no.

    - Flights Booked --> Distribución extremadamente sesgada hacia la derecha (el 48.58% del dataset tiene 0 vuelos, solo el 25% superior supera los 8 vuelos). Distribución 'long tail'.

    - Flights with Companions --> Distribución muy sesgada a la derecha. Percentil 25% = 0 --> Más del 50% de los clientes nunca volaron con acompañantes. Distribución 'long tail'.

    - Total Flights --> Distribución extremadamente sesgada a la derecha. Percentil 25% = 0 --> Al menos el 25% no han volado nunca y al menos el 50% han volado como mucho 1 vez. La media es mayor porque hay un grupo más pequeño de clientes que voló muchas veces, el 25% superior viaja bastante (+10 viajes). Distribución 'long tail'.

    - Distance --> Mucha diversidad en las distancias (muchos valores únicos). Distribución muy sesgada a la derecha: Percentil 25% = 0, la mediana es mucho menor que la media, la 'long tail' sube la media. Alta desviación estándard que refleja una gran dispersión.

    - Points Accumulated --> Única columna de tipo float64. El 25% tienen 0 puntos acumulados, un cuarto de los clientes no ha acumulado puntos. La distribución está sesgada a la derecha, con unos pocos clientes acumulando muchos puntos, por eso la media es más del doble que la mediana. Alta desviación estándard que refleja una gran dispersión. El valor 0 es importante y refleja falta de participación o uso del programa.

    - Points Redeemed --> Variable fuertemente sesgada a la derecha, mayoría sin canjes y pocos canjes grandes. El 25%, 50% y 75% percentiles son 0, lo que indica que al menos el 75% de los clientes no han canjeado puntos. La media és muy por encima de la mediana porque un pequeño grupo de clientes canjea muchos puntos. Alta desviación estándard que refleja una gran dispersión.

    - Dollar Cost Points Redeemed --> El 75% de los valores son 0, lo que indica que la mayoría no canjearon puntos. La media es baja (2.5) pero hay casos con costos altos de hasta 71 dólares, por eso también hay una desviación estándar alta (alta dispersión).