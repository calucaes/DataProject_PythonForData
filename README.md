DataProject: Análisis Exploratorio de Datos con Python

1. Descripción del proyecto

El objetivo es explorar los datos de campañas telefónicas de una entidad bancaria y las características de sus clientes. El proyecto aplica limpieza y transformación, análisis descriptivo, combinación de tablas y visualización.

Se estudia la tasa de suscripción, sus diferencias por canal, por resultado de campañas anteriores y por momento del contacto. También se exploran las distribuciones de edad, duración e ingresos, las correlaciones entre variables numéricas y algunas características de los clientes.

Herramientas: Python, Pandas, Matplotlib, Visual Studio Code y Jupyter Notebook.

2. Estructura del proyecto

- `notebooks/analisis_eda_paso_a_paso.ipynb`: notebook principal, organizado por pasos y guardado con las celdas ejecutadas, sus resultados y los gráficos visibles.
- `data/raw/`: archivos originales `bank-additional.csv` y `customer-details.xlsx`.
- `data/input/customer-details-combinado.csv`: copia de las tres hojas del Excel apiladas, incluida como alternativa si el entorno no puede leer directamente el archivo Excel.
- `data/processed/`: campañas limpias, fichas de clientes combinadas y tabla final cruzada, generadas por el notebook.
- `outputs/graficos/`: catorce gráficos PNG generados por el notebook.
- `README.md`: este documento.

3. Carga y ejecución del proyecto

1. Abrir en Visual Studio Code la carpeta `PYTHON FOR DATA`.
2. Abrir `notebooks/analisis_eda_paso_a_paso.ipynb` y seleccionar el kernel de Python que se va a utilizar.
3. Si Pandas o Matplotlib no están disponibles, ejecutar la primera celda `%pip install pandas matplotlib` en el kernel seleccionado.
4. Ejecutar las celdas en orden con **Shift + Enter**. El notebook intenta leer el Excel original con `pd.read_excel`, apilar las hojas y conservar el año de cada hoja. Si el entorno no dispone del lector de Excel que necesita Pandas, el notebook usa el CSV combinado de `data/input/`.
5. Al terminar, revisar las tablas que aparecen debajo de las celdas, los gráficos del notebook y los archivos guardados en `data/processed/` y `outputs/graficos/`.

Los archivos originales de `data/raw/` se conservan sin modificaciones. El notebook guarda los resultados preparados en `data/processed/` y las imágenes en `outputs/graficos/`.

4. Datos y combinación de las tablas

`bank-additional.csv` contiene 43.000 registros y 24 columnas originales. Se elimina `Unnamed: 0`, que corresponde a un índice exportado. Las cuatro columnas económicas con coma decimal se convierten a valores numéricos. La fecha, cuyo mes está escrito en español, se convierte a fecha y se extraen el mes y el año del contacto.

`customer-details.xlsx` contiene tres hojas (`2012`, `2013` y `2014`) con 43.170 fichas en total. El notebook intenta leer todas las hojas con `pd.read_excel(..., sheet_name=None)`, añade el año de procedencia y las apila con `pd.concat`. Si no puede leer el Excel, utiliza `data/input/customer-details-combinado.csv`, que contiene esas hojas ya apiladas.

Las campañas se enlazan con las fichas de clientes mediante un `merge` de tipo `left` por `id_` e `ID`, conservando todos los registros de campaña. Las 43.000 campañas encontraron ficha de cliente en los datos usados para este análisis.

5. Limpieza y buenas prácticas

- Se conservan los archivos originales en `data/raw/`.
- Se elimina el índice exportado, no una característica de los clientes.
- Se convierten a números las cuatro columnas económicas que usan coma decimal.
- Se convierten las fechas con meses en español y se extraen mes y año.
- Se revisan valores ausentes y duplicados. Los valores ausentes se conservan y no se imputan.
- Se utiliza un cruce `left` para conservar todas las campañas.
- Los resultados se interpretan como descriptivos y no se afirma que una variable cause la suscripción.
- La duración se interpreta con cautela porque solo se conoce al terminar la llamada.

6. Análisis y visualizaciones

El notebook contiene catorce gráficos:

- Resultado general de las campañas.
- Tasa de suscripción por canal.
- Tasa según el resultado de la campaña anterior.
- Mediana de duración según el resultado.
- Histogramas y diagramas de caja para edad, duración e ingresos.
- Correlación entre variables numéricas.
- Tasa de suscripción por mes y por año de contacto.
- Tasa de suscripción según el año de alta del cliente.

También se comparan las visitas web mensuales con el número de niños y adolescentes en el hogar. Los diagramas de caja ayudan a identificar observaciones alejadas, pero no significan automáticamente que sean errores. Las correlaciones muestran asociaciones lineales y no demuestran causalidad.

7. Resultados destacados

- Hubo 4.844 suscripciones entre 43.000 campañas: una tasa general del **11,27 %**.
- La tasa fue del **14,74 %** para `cellular` y del **5,16 %** para `telephone`.
- En los registros con resultado anterior `SUCCESS`, la tasa fue del **65,32 %** (938 de 1.436 contactos). Es un grupo más pequeño que el total.
- La mediana de duración fue de **449 segundos** en las llamadas asociadas a suscripción y de **163 segundos** en las demás. Esta diferencia se conoce después de la llamada.
- La mitad central de las duraciones está entre **102 y 319 segundos**. Hay 3.072 llamadas por encima del límite superior de los bigotes; no se eliminaron porque no se consideran errores automáticamente.
- La mediana de edad es de **38 años** y la mitad central va de **32 a 47 años**. Faltan 5.120 edades.
- La mitad central de los ingresos va aproximadamente de **49.610 a 136.745**. No aparecen ingresos fuera de los bigotes del diagrama.
- `emp.var.rate` y `euribor3m` presentan una correlación alta (aproximadamente **0,97**). La correlación describe asociación, no causalidad.
- La tasa mensual varía entre el **10,25 %** en septiembre y el **12,36 %** en octubre. Por año de contacto, va del **10,87 %** al **11,68 %**, sin una tendencia continua.
- Los ingresos medios y las visitas web mensuales medias son parecidos entre los grupos `yes` y `no`.
- La tasa por año de alta es del **4,59 %** para 2012, **7,74 %** para 2013 y **23,01 %** para 2014. Es una diferencia descriptiva que convendría investigar con más datos.
- Faltan 9.256 valores de `euribor3m` y 248 fechas. No se imputaron.

El enunciado describe una entidad portuguesa, pero las coordenadas del CSV no parecen concordar con esa descripción. Se conservaron, pero no se utilizaron para extraer conclusiones geográficas.

8. Autoría

Carlos Luque Camacho
