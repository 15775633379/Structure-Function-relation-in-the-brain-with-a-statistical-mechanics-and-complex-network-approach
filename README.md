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

En este trabajo, se busca estudiar un subgrupo de sujetos, ver **figura 1**, de la población de humanos adultos sanos y jóvenes ofrecida por el proyecto del conectoma humano, elegidos en términos de su desempeño, alto o bajo, en un conjunto de pruebas psicométricas. Se quieren contruir las redes de conetividad estructural y funcional para comparar sus propiedades con las caracteristicas cognitivas y psicologicas extraidas de los sujetos elegidos. El proyecto conectoma humano (HCP) es un esfuerzo inter-institucional liderado por el King´s College de London, el Imperial College de London y la universidad de Oxford con el fin de mapear la conectividad anatómica y funcional en el cerebro humano y estudiar su relación con la cognición, la conducta y la herencia genética.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/abf703684f2929a2c75fdcddf4d47e877ae02ed4/Images/subjects_hcp_1200.jpeg)

**Figure 1.** Sujetos elegidos, se muestra su código dentro del HCP-1200, notación para este trabajo y categoría.

De todos los datos ofrecidos por el HCP para el estudio del adulto joven, en este trabajo solo se usaron algunos resultados de tareas cognitivas, pruebas de personalidad y algunos archivos provenientes de dMRI, fMRI y sMRI a 3T. El resumen de los archivos a utilizar, y su ubicación en la estructura de datos ofrecida por el HCP por medio del acceso desde Amazon Web Services se muestra en la **figura 2**. Las tareas experimentales cognitivas elegidas fueron las tres realizadas sincrónicamente con las resonancias funcionales elegidas; es decir las tareas denominadas: Memoria Operativa, Emoción y Social. Los archivos necesarios para construir la conectividad estructural se encuentran en la carpeta T1W y los necesarios para construir la conectividad funcional en la carpeta MNINonLinear.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/f5b0ace72789ea9d1bde6a52cb30c030f2136c7a/Images/diagrama_datos_HCP.PNG)

**Figure 2.** Resumen de los archivos utilizados provenientes de las resonancias y su ubicación en la estructura de datos del proyecto conectoma humano.

Para caracterizar psicológicamente a los sujetos elegidos, se eligieron los resultados de los cinco grandes de la personalidad (Big-Five), ver **figura 3**, entendidos como 5 rasgos resultado del análisis de reducción de dimensionalidad de los ítems utilizados en la prueba, los cuales se suponen relativamente ortogonales y permiten caracterizar la personalidad de las personas de acuerdo con los valores asociados a cada uno de los 5 rasgos y de acuerdo la combinación de dichos valores en un perfil más globales de personalidad. 

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/d87eb4978cc6f3c923962533900f04eab1b2da2c/Images/personality_test.jpeg)

**Figure 3.** Tests de personalidad extraídos del HCP.

Finalmente, en el analisis cognitivo de los sujetos se usaron 6 medidas, 3 ofrecidas por el HCP y 3 construidas a partir de medidas ofrecidas por el HCP - en la **figura 4** se muestra el nombre de la medida en este trabajo y a la derecha su traducción en términos de las medidas ofrecidas por el HCP. Las medidas consistentes en una fracción buscan tener en cuenta tanto la precisión como los tiempos de reacción, de tal forma que toman valores más altos cuando la precisión es alta y los tiempos de reacción media menores.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/d87eb4978cc6f3c923962533900f04eab1b2da2c/Images/pruebas_psicometricas.jpeg)

**Figure 4.** Medidas de las tareas exprimentales del HCP extraídas de los sujetos. Los puntajes de social, emoción y memoria operativa fueron los que se utilizaron para elegir las poblaciones por tarea.

## Brain Network Construction
Se presentan los resultados de la primera parte del trabajo, correspondiente a la construcción del modelo de grafo de la conectividad estructural, de la conectividad funcional y del modelo mecánico estadístico que nos permite simular la conectividad funcional a partir de la estructural.

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/3ab8a961e42dcf69fcecbe062a6e9ff94cc9418f/Images/conectividades_WM_M+.png)

**Figure 5.** Las diferentes matrices de conectividad extraidas para el sujeto de sexo masculino con mayor puntaje en la prueba de working memory (WM M+). Dado que la conectividad estructural es muy dispersa se aplico un logaritmo a cada una de sus componentes para mejorar la visualización

### Parcelation

Se hizo uso de los resultados expuestos en [Neuroparc](https://github.com/neurodata/neuroparc) para elegir la parcelación de AAL (Automated Anatomical Labeling) que divide el cerebro en 116 regiones incluyendo el cortex y las regiones subcorticales, generando asi los nodos sobre lo que se contruiran las redes estructurales y funcionales.

### Structural Connectivity (SC)

Los datos con la informacion estructural, extraidos por resonancia magnetica de difusion, y proporcionados por el HCP (en la carpeta **T1w**), sirven de base para construir un tractograma. Existen múltiples formas de hacer tractografía, y el método que se usó aquí fue a traves de un algoritmo local denominado $\textit{Particle Filtering Tracking}$. Todos los tractos nerviosos (streamlines) que el algoritmo estima se guardan en un archivo TRK o tractograma en un formato de representación estándar RASMM de NiBabel. 

Aunando el tractograma que se extrae de los datos del HCP con la parcelación de AAL, se determina la matriz de **conectividad estructural** mediante el conteo de los tractos que van de una región o nodo específico a otro, como el peso de los enlaces. A la matriz estructural se le aplico un umbral de 0.05 según su normalización respecto del enlace con mayor peso. El código asociado al algoritmo y la contruccion de la red se implementó en Python por medio de las librerías especializadas para el procesado y análisis de imágenes médicas DIPY & NiBabel.

### Functional Connectivity (FC)

La información usada para construir la conectividad funcional de cada sujeto durante cada una de las tareas que se han de estudiar, proviene de los datos resonancia magnética funcional preprocesados y limpios de cualquier actividad funcional producida por movimientos motores involuntarios, dando como resultado una imagen funcional o tensor de tercer orden que contiene en sus componentes (o voxels) la señal BOLD medida cada 0.72 segundos, y formando así unas series de tiempo para cada voxel.

Una vez cargada la parcelación al archivo funcional, las series de tiempo se promedian dentro de los voxeles que conforman una parcela o nodo, y se define una medida de correlación que cuantifica los vinculos funcionales. Para este caso se toma el coeficiente de Pearson, una medida de correlación lineal, como el criterio para establecer correlaciones dentro de las series de tiempo del archivo obtenido, generando asi una matriz simétrica que representa la conectividad funcional. Finalmente, se le aplicó un umbral a esta matriz, conservando unicamente las correlaciones que tengan una magnitud de al menos el $5\%$ respecto a la correlación más alta encontrada.

### Spin Glass Model for Functional Connectivity

Se quieren modelar las correlaciones en la actividad metabólica cerebral, tal como se mide por medio de fMRI. Para esto consideramos que cada parcela sólo puede tener dos estados de activación, +/-1; +1 cuando la parcela presenta un valor mayor al de su promedio en la señal BOLD y -1 cuando presenta un valor menor, de esta forma asociando a cada estado de activación cerebral un estado de espín neto sobre la red. Se considera que la interacción entre regiones cerebrales es lineal y tal que busca alinear (i.e. poner en el mismo estado) a los nodos vecinos, donde para tener en cuenta la influencia de factores externos y que la mayoría de la actividad cerebral es autogenerada, puede introducirse un factor estocástico, que modifica el estado de region/nodo con cierta probabilidad; y que se modela como un ruido térmico, lo que nos lleva a modelos del mismo tipo que el denominado en física estadística como Modelo de Ising.

Se puede establecer un Hamiltoniano que de cuenta de la interacción entre espines/nodos como, 

$$H = \frac{1}{2}\Theta \sum_i S_i - \frac{1}{2}W \sum_{i,j}C_{i,j}S_iS_j$$


donde $S_i$, $S_j$ indican el estado del nodo (+/-1), $\Theta$ índica el umbral de energía para que una región cambie su estado; $W$ es un parámetro de escala para la matriz de adyacencia, $A_{i,j}$ es la matriz de adyacencia a la conectividad estructural y $T$ se define como la temperatura del sistema, parámetro que modulará la aleatoriedad de la ocurrencia de los estados.

Se utilizará al igual que en física estadística y entendiéndose en el sentido de la teoría de la información el principio de máxima entropía, para asociar una probabilidad de ocurrencia de estado a cada energía definida por el Hamiltoniano. Muestreando los estados de espín de la red usando un algoritmo de Metropolis Hasting modificado, donde cada 500 iteraciones se invierte el estado de todos los espines para navegar entre distintos atractores o mínimos de energía, y así construir la conectividad funcional simulada cuantificando correlaciones en la actividad cerebral modelada. 

Se exploraron distintos valores de parámetros y se escogieron aquellos alrededor de los cuales las simulaciones presentaron comportamiento en transición de fase para la mayoría de sujetos, esto inspirado en la hipótesis del cerebro crítico. De esta forma se tomó $W = 8.53$, $\Theta=1$ y $T = 4$.

## Results (e.g. Working Memory Task)

Se presentan algunos de los resultados de la comparación entre la conectividad estructural/simulada respecto a las conectividades funcionales. Así mismo se muestran algunos resultados de las tareas experimentales y de la prueba psicométrica de personalidad para los sujetos elegidos junto a varias propiedades topológicas globales y nodales de sus redes cerebrales.

Para guiarse en el análisis de resultados es útil tener en cuenta las preguntas que guían este trabajo:

- ¿Hay relación entre los resultados tareas cognitivas y de personalidad con las propiedades topológicas de las redes cerebrales?
- ¿Es posible discernir una relación entre las diferencias en propiedades topológicas estructurales entre los sujetos y sus propiedades topológicas funcionales?
- ¿El modelo generalizado de Ising logra reproducir aspectos producto de interacciones de alto orden de la conectividad funcional implícitos en la estructura? 
- ¿Qué propiedades topológicas tiene la conectividad funcional simulada por medio del modelo generalizado de Ising? ¿Difieren de las de la conectividad estructural?

Los resultados se agrupan por los sujetos elegidos como peores o mejores respecto a las tareas denominadas social, de emoción y de memoria operativa. Se muestran primero los resultados en las tareas experimentales y la prueba de personalidad, luego se presentan las comparaciones con distancia euclidiana entre la conectividad estructural/simulada y las conectividades funcionales; junto a esta información se encuentran también las propiedades topológicas globales de la red estructural, simulada, la funcional del reposo y la funcional de la tarea correspondiente con la que se eligieron los sujetos. Finalmente se presentan algunas propiedades topológicas nodales locales (entropía y energía) y globales (cercanía e intermediación) para la red estructural y funcional de la tarea correspondiente a la población.

### Psychometric and Personality Tests

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/aae061020726dfb9486246459233b9ed8a8293f5/Images/psicometricas_Memoria%20Operativa.png)

**Figure 5.** Para la población de sujetos clasificada respecto a las tareas de memoria operativa, se muestran los resultados en las pruebas psicométricas y los rasgos de personalidad.

### Differences between Structural and Functional Connectivities

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/310c588097c09ed069da0a324f4dd295d9842db4/Images/distancias_WM.png)

**Figure 6.** Se muestran las distancias euclidianas entre la conectividad estructural y simulada con las conectividades funcionales para distintas tareas.
    
### Global Properties

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/310c588097c09ed069da0a324f4dd295d9842db4/Images/globales_WM.png)

**Figure 7.** Para la población de sujetos clasificada respecto a las tareas de memoria operativa, se muestran las propiedades topológicas globales obtenidas para las redes estructurales, en reposo, simuladas y de memoria operativa.

### Local Properties

![image](https://github.com/DiegoHerediaF/Network-science-and-statistical-mechanics-for-the-study-of-structure-function-relation-in-the-brain/blob/aae061020726dfb9486246459233b9ed8a8293f5/Images/locales_WM.png)

**Figure 8.** Para la población de sujetos clasificada respecto a las tareas de memoria operativa, se muestran las medidas locales, obtenidas para las regiones cerebrales de las redes estructurales y funcionales (asociadas a la tarea de memoria operativa).

## Conclusions

- No se encontró una relación entre las propiedades topológicas de las redes estructurales y las redes funcionales, así como tampoco una relación entre la similitud de las redes estructurales y funcionales con el desempeño en las pruebas cognitivas. 
    
- Las medidas utilizadas para calificar el desempeño de los sujetos en la tarea de memoria de trabajo y emoción, parecen dar cuenta de un desempeño general de los sujetos en las pruebas cognitivas, mientras en la tarea social no.
    
- Se evidencia que las propiedades topológicas de las redes cerebrales construidas en este trabajo logran identificar la existencia de algunos sujetos atípicos en los resultados de tareas experimentales y prueba de personalidad. Sugiriendo la posibilidad de una rica interacción entre neurociencia y psicología, lo que podría dar lugar por ejemplo a una neurociencia de redes de la personalidad.
    
- Mientras en la red estructural los nodos con mayor Energía nodal tienden a tener menores Entropías nodales, en la red funcional los nodos con mayor Energía nodal tienden a tener mayor Entropía nodal; mostrando así unos principios de organización de la conectividad local distintos entre estas dos redes.
   
- El modelo generalizado de Ising sí logró dar cuenta de relaciones de más alto orden implícitas en la estructura, de tal forma que la red funcional simulada muestra en todos los casos unas distancias euclideanas menores con las redes funcionales experimentales que la red estructural.
