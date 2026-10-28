DataProject: Análisis Exploratorio de Datos con Python

1. Descripcion del proyecto

El objetivo es explorar los datos de campañas telefónicas de una entidad bancaria y las características de sus clientes. El proyecto aplica limpieza y transformación, análisis descriptivo, combinación de tablas y visualización.

Se estudia, entre otras cosas, la tasa de suscripción (`y`), sus diferencias por canal de contacto y por resultado de campañas anteriores, y las estadísticas de duración de llamadas, ingresos y visitas web.

Herramientas:
		 Python
		 Pandas
		 Matplotlib
		 Visual Studio Code 
		 Jupyter Notebook.

2. Estructura del proyecto

- Archivo en notebooks/analisis_eda_paso_a_paso.ipynb: NOTEBOOK PRINCIPAL. Contiene el análisis dividido en celdas para ejecutarlo y revisarlo paso a paso. Incluye cuatro gráficos de Matplotlib.
- Archivo en data/raw: ARCHIVOS ORIGINALES bank-additional.csv y customer-details.xlsx.
- Archivo en data/input/customer-details-combinado.csv: las tres hojas del Excel apiladas en un CSV listo para Pandas. Se incluye para que el notebook pueda leer los datos con read_csv.
- Archivo en data/processed: CAMPAÑAS LIMPIAS, FICHA CLIENTES COMBINADAS y TABLA F INAL CRUZADA.
- Archivo en outputs/graficos: GRAFICOS.

3. Carga y ejecución del proyecto

A. Abrir en Visual Studio Code la carpeta `PYTHON FOR DATA`.
B. Abrir notebooks/analisis_eda_paso_a_paso.ipynb y seleccionar el kernel de Python que se va a utilizar.
C. Si aparece un error porque falta Pandas o Matplotlib, ejecutar la primera celda %pip install pandas matplotlib. Después, ejecutar el resto de celdas en orden con Shift+Enter.
D. Cuando termine el notebook, abre la carpeta data/processed/ para consultar los CSV limpios y combinados. Ab re outputs/graficos/ para ver las imágenes PNG creadas por Matplotlib.

El Excel original se conserva en data/raw. El notebook lee la version combinada de sus tres hojas desde data/input/customer-details-combinado.csv.


4. Datos y combinación de las tablas

bank-additional.csv contiene 43.000 registros de campañas y 24 columnas originales. La columna `id_` identifica cada registro.

customer-details.xlsx contiene tres hojas (`2012`, `2013` y `2014`) y 43.170 fichas de clientes en total. Sus hojas están apiladas en data/input/customer-details-combinado.csv, con una columna que conserva el año de procedencia.

Las 43.000 campañas se enlazan con una ficha mediante los identificadores id_ e ID. Se conservan también las 170 fichas de clientes que no aparecen en las campañas.

5. Buenas prácticas aplicadas

- Los archivos originales se conservan sin cambios en data/raw/.
- Se elimina del análisis la columna Unnamed: 0, que es un índice exportado y no una característica del cliente. No se eliminan filas por valores repetidos en ese índice.
- Las cuatro columnas económicas con coma decimal se convierten a números para poder analizarlas.
- Se revisan los valores ausentes y los duplicados. Los valores ausentes se conservan; no se imputan.
- Se combinan las campañas y los clientes mediante un merge de tipo left, preservando todas las campañas.
- Los resultados se interpretan como descriptivos. No se afirma que una variable cause la suscripción.
- La duración de la llamada se interpreta con cautela porque solo se conoce después de la interacción.

6. Resultados destacados

- Hubo 4.844 suscripciones entre 43.000 campañas: una tasa general del 11,27 %.
- La tasa fue 14,74 % para el canal cellular y 5,16 % para telephone.
- En las campañas cuyo resultado anterior fue SUCCESS, la tasa fue 65,32 % (938 de 1.436 registros). Este grupo es menor que los demás.
- La mediana de duración fue 449 segundos en las llamadas asociadas a suscripción y 163 segundos en las demás. Esta diferencia es descriptiva y posterior a la llamada.
- Los ingresos medios fueron parecidos: aproximadamente 92.584 para `yes` y 93.325 para `no`. Las visitas web mensuales medias también fueron similares: 16,60 y 16,59.
- euribor3m tiene 9.256 valores ausentes; age, 5.120; y date, 248. No se rellenaron esos valores.
- El enunciado describe una entidad portuguesa, pero el rango de coordenadas del CSV no parece concordar (o yo no le encuentro sentido) con esa descripción. Se conservan las coordenadas, pero no se presentan conclusiones geográficas.

Los cuatro gráficos del notebook muestran la distribución de suscripciones, la tasa por canal, la tasa según el resultado anterior y la mediana de duración según el resultado. Se generan al ejecutar las celdas correspondientes.

7. Autoría

Carlos Luque Camacho
