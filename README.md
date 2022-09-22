# Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain

This project was realized by

**Diego A Heredia F**

**Juan C Higuera C**

This work was presented as a partial requirement to qualify for the title of **Physicist** and the grade obtained was **5.0/5.0**.

Using data from the HCP dataset, we study the topological properties of structural connectivity, functional connectivity, and simulated functional connectivity. We then compared these topological properties with psychological test scores for twelve subjects selected for having obtained extreme scores on these tests. We obtain that atypical subjects in the psychological test can be recognized as having atypical topological properties in their structural or functional connectivity.

**Keywords:** Neurociencia, Resonancia magnética nuclear funcional, Resonancia magnética nuclear de difusión, relación estructura y función, modelo generalizado de Ising, Entropía, Análisis de redes.

## Description

El desarrollo de las técnicas de neuroimagen ha permitido por primera vez en la historia acceder a la estructura y dinámica cerebral en tiempo real. Atendiendo a esta oportunidad, en este trabajo se hace uso de datos de Resonancia magnética nuclear, Ciencia de redes y Mecánica estadística, con el fin de explorar la relación entre la conectividad de tractos nerviosos del cerebro, su actividad metabólica y la función cerebral; esta ultima cuantificada por medio de tareas experimentales cognitivas y pruebas psicométricas. Para esto, primero se construyeron modelos de grafos, en los cuales los nodos se definieron como regiones cerebrales y los enlaces como cantidad de tractos nerviosos en el caso de la estructura, y como correlaciones de la actividad metabólica en el caso de la actividad cerebral. Además de esto, para explorar las interacciones de alto orden implícitas en la estructura, se hizo uso de un modelo mecánico estadístico capaz de simular correlaciones entre regiones cerebrales a partir de la información de su conectividad estructural, obteniendo así una red cerebral simulada a la cual junto al resto de redes cerebrales se le estudiaron sus propiedades topológicas. Se concluye que estas propiedades topológicas logran identificar a sujetos atípicos en los resultados psicológicos, sugiriendo la viabilidad de una rica interacción entre neurociencia de redes y psicología.

## Data

En este trabajo, se busca estudiar un subgrupo de sujetos, ver **figura 1**, de la población de humanos adultos sanos y jóvenes ofrecida por el proyecto del conectoma humano, elegidos en términos de su desempeño, alto o bajo, en un conjunto de pruebas psicométricas. El proyecto conectoma humano (HCP) es un esfuerzo inter-institucional liderado por el King´s College de London, el Imperial College de London y la universidad de Oxford con el fin de mapear la conectividad anatómica y funcional en el cerebro humano y estudiar su relación con la cognición, la conducta y la herencia genética.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/abf703684f2929a2c75fdcddf4d47e877ae02ed4/Images/subjects_hcp_1200.jpeg)

**Figure 1.** Sujetos elegidos, se muestra su código dentro del HCP-1200, notación para este trabajo y categoría.

De todos estos datos ofrecidos por el HCP para el estudio del adulto joven, en este trabajo solo se usaron algunos resultados de tareas cognitivas, pruebas de personalidad y algunos archivos provenientes de dMRI, fMRI y sMRI a 3T. El resumen de los archivos a utilizar, y su ubicación en la estructura de datos ofrecida por el HCP por medio del acceso desde Amazon Web Services se muestra en la **figura 2**. Las tareas experimentales cognitivas elegidas fueron las tres realizadas sincrónicamente con las resonancias funcionales elegidas; es decir las tareas denominadas: Memoria Operativa, Emoción y Social. Los archivos necesarios para construir la conectividad estructural se encuentran en la carpeta T1W y los necesarios para construir la conectividad funcional en la carpeta MNINonLinear.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/f5b0ace72789ea9d1bde6a52cb30c030f2136c7a/Images/diagrama_datos_HCP.PNG)

**Figure 2.** Resumen de los archivos utilizados provenientes de las resonancias y su ubicación en la estructura de datos del proyecto conectoma humano.

Para caracterizar psicológicamente a los sujetos elegidos, se eligieron los resultados de los cinco grandes de la personalidad (Big-Five), ver **figura 3**, entendidos como 5 rasgos resultado del análisis de reducción de dimensionalidad de los ítems utilizados en la prueba, los cuales se suponen relativamente ortogonales y permiten caracterizar la personalidad de las personas de acuerdo con los valores asociados a cada uno de los 5 rasgos y de acuerdo la combinación de dichos valores en un perfil más globales de personalidad. 

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/d87eb4978cc6f3c923962533900f04eab1b2da2c/Images/personality_test.jpeg)

**Figure 3.** Tests de personalidad extraídos del HCP.

Para evaluar cognitivamente a los sujetos se usaron 6 medidas, 3 ofrecidas por el HCP y 3 construidas a partir de medidas ofrecidas por el HCP - en la **figura 4** se muestra en la columna \textbf{Prueba Psicométrica} el nombre de la medida en este trabajo y a la derecha su traducción en términos de las medidas ofrecidas por el HCP. Las medidas consistentes en una fracción buscan tener en cuenta tanto la precisión como los tiempos de reacción, de tal forma que toman valores más altos cuando la precisión es alta y los tiempos de reacción media menores.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/d87eb4978cc6f3c923962533900f04eab1b2da2c/Images/pruebas_psicometricas.jpeg)

**Figure 4.** Medidas de las tareas exprimentales del HCP extraídas de los sujetos. Los puntajes de social, emoción y memoria operativa fueron los que se utilizaron para elegir las poblaciones por tarea.

## Brain Network Construction
Se presentan los resultados de la primera parte del trabajo, correspondiente a la construcción del modelo de grafo de la conectividad estructural, de la conectividad funcional y del modelo mecánico estadístico que nos permite simular la conectividad funcional a partir de la estructural.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/3ab8a961e42dcf69fcecbe062a6e9ff94cc9418f/Images/conectividades_WM_M+.png)

**Figure 5.** Las diferentes matrices de conectividad extraidas para el sujeto de sexo masculino con mayor puntaje en la prueba de working memory (WM M+). Dado que la conectividad estructural es muy dispersa se aplico un logaritmo a cada una de sus componentes para mejorar la visualización

### Parcelation

Se hizo uso de los resultados expuestos en [Neuroparc](https://github.com/neurodata/neuroparc) para elegir la parcelación de AAL (Automated Anatomical Labeling) que divide el cerebro en 116 regiones incluyendo el cortex y las regiones subcorticales, generando asi los nodos sobre lo que se contruiran las redes estructurales y funcionales.

### Structural Connectivity (SC)

Los datos con la informacion estructural, extraidos por resonancia magnetica de difusion, y proporcionados por el HCP (en la carpeta **T1w**), sirven de base para construir un tractograma. Existen múltiples formas de hacer tractografía, y el método que se usó aquí fue a traves de un algoritmo local denominado \textit{Particle Filtering Tracking}. Todos los tractos nerviosos (streamlines) que el algoritmo estima se guardan en un archivo TRK o tractograma en un formato de representación estándar RASMM de NiBabel. 

Aunando el tractograma que se extrae de los datos del HCP con la parcelación de AAL, se determina la matriz de **conectividad estructural** mediante el conteo de los tractos que van de una región o nodo específico a otro, como el peso de los enlaces. A la matriz estructural se le aplico un umbral de 0.05 según su normalización respecto del enlace con mayor peso. El código asociado al algoritmo y la contruccion de la red se implementó en Python por medio de las librerías especializadas para el procesado y análisis de imágenes médicas DIPY & NiBabel.

### Functional Connectivity (FC)

La información usada para construir la conectividad funcional de cada sujeto durante cada una de las tareas que se han de estudiar, proviene de los datos resonancia magnética funcional preprocesados y limpios de cualquier actividad funcional producida por movimientos motores involuntarios, dando como resultado una imagen funcional o tensor de tercer orden que contiene en sus componentes (o voxels) la señal BOLD medida cada 0.72 segundos, y formando así unas series de tiempo para cada voxel.

Una vez cargada la parcelación al archivo funcional, las series de tiempo se promedian dentro de los voxeles que conforman una parcela o nodo, y se define una medida de correlación que cuantifica los vinculos funcionales. Para este caso se toma el coeficiente de Pearson, una medida de correlación lineal, como el criterio para establecer correlaciones dentro de las series de tiempo del archivo obtenido, generando asi una matriz simétrica que representa la conectividad funcional. Finalmente, se le aplicó un umbral a esta matriz, conservando unicamente las correlaciones que tengan una magnitud de al menos el $5\%$ respecto a la correlación más alta encontrada.

### Spin Glass Model for Functional Connectivity

## Results (e.g. Working Memory Task)

### Psychometric Test
    
### Global Properties

### Local Properties

## Conclusions

- No se encontró una relación entre las propiedades topológicas de las redes estructurales y las redes funcionales, así como tampoco una relación entre la similitud de las redes estructurales y funcionales con el desempeño en las pruebas cognitivas. 
    
- Las medidas utilizadas para calificar el desempeño de los sujetos en la tarea de memoria de trabajo y emoción, parecen dar cuenta de un desempeño general de los sujetos en las pruebas cognitivas, mientras en la tarea social no.
    
- Se evidencia que las propiedades topológicas de las redes cerebrales construidas en este trabajo logran identificar la existencia de algunos sujetos atípicos en los resultados de tareas experimentales y prueba de personalidad. Sugiriendo la posibilidad de una rica interacción entre neurociencia y psicología, lo que podría dar lugar por ejemplo a una neurociencia de redes de la personalidad.
    
- Mientras en la red estructural los nodos con mayor Energía nodal tienden a tener menores Entropías nodales, en la red funcional los nodos con mayor Energía nodal tienden a tener mayor Entropía nodal; mostrando así unos principios de organización de la conectividad local distintos entre estas dos redes.
   
- El modelo generalizado de Ising sí logró dar cuenta de relaciones de más alto orden implícitas en la estructura, de tal forma que la red funcional simulada muestra en todos los casos unas distancias euclideanas menores con las redes funcionales experimentales que la red estructural.
