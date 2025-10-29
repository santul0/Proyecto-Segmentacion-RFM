# Proyecto-Segmentacion-RFM
Análisis RFM de clientes de e-commerce para definir estrategias de marketing.
---

## 1. El Problema de Negocio

Imaginá que sos el gerente de marketing de un e-commerce. Tenés un presupuesto limitado y un objetivo de ventas. Por un lado, tenés clientes fieles que compran todos los meses pero, por otro, tenés clientes que compraron una sola vez hace 6 meses.
El problema es: ¿les mandás la misma campaña de "20% OFF" a los dos? Si lo hacés, estás perdiendo plata: le estás regalando un descuento a tu cliente fiel que iba a comprar de todas formas, y quizás ese 20% no es suficiente para que el cliente "casi perdido" vuelva.
Este proyecto nació para solucionar ese despilfarro. El objetivo fue dejar de adivinar y usar datos para segmentar la base de clientes en grupos accionables, permitiendo así maximizar el ROI de las campañas de marketing.

---

## 2. Metodología

Para lograr ese objetivo, apliqué un modelo de marketing: el análisis RFM.
En lugar de ver a los clientes como una gran masa, este modelo los califica individualmente basándose en su comportamiento de compra. Para hacerlo, respondí a tres preguntas clave:
  -Recencia (R): ¿Cuán recientemente nos compró?
  -Frecuencia (F): ¿Qué tan seguido nos compra?
  -Monetario (M): ¿Cuánto dinero ha gastado en total?
El proceso técnico fue un trabajo de análisis de datos usando Python, principalmente con las librerías Pandas, Matplotlib y Seaborn.

El Sistema de Puntuación (Scoring): Primero, no se puede comparar directamente "10 días" con "10 compras". Necesitaba un sistema de calificación universal. Para esto, usé una técnica de cuartiles. Tomé a todos los clientes y los dividí en 4 grupos iguales para cada una de las 3 métricas (R, F y M). Luego, les asigné un puntaje del 1 al 4.

Puntaje 4 = El mejor 25%

Puntaje 3 = El siguiente 25%

Puntaje 2 = El siguiente 25%

Puntaje 1 = El peor 25%

La clave del modelo se aplicó así:

Puntaje R (Recencia): 4 = El más reciente (mejor), 1 = El más antiguo (peor). (Nota: Esto se logra invirtiendo la escala, ya que un valor numérico más bajo de días es mejor).

Puntaje F (Frecuencia): 4 = El más frecuente (mejor), 1 = El menos frecuente (peor).

Puntaje M (Monetario): 4 = El que más gastó (mejor), 1 = El que menos gastó (peor).

Al final de este paso, cada cliente tenía un "código" de 3 dígitos (ej. "444", "121", "412").

La Lógica de Negocio para cada Segmento

Con esos "códigos", definí 6 segmentos estratégicos. En lugar de crear reglas para las 64 combinaciones posibles (4x4x4), usé patrones (expresiones regulares o Regex) para agrupar los perfiles lógicos:
(Una expresión regular o "Regex" es simplemente un "mini-lenguaje" usado para buscar patrones en el texto. Por ejemplo, el patrón ^[3-4] significa "el texto debe empezar con un '3' o un '4'", permitiéndonos agrupar códigos similares).

a. Clientes VIP: (Patrón Regex: ^[3-4][3-4][3-4]$)
 Los mejores en todo. Clientes que puntuaron alto (3 o 4) en Recencia, Frecuencia Y Gasto. Son la "joya" del negocio.

b. Clientes en Riesgo: (Patrón Regex: ^[1-2][3-4][3-4]$)
 Clientes que eran VIPs. Puntuaron alto (3 o 4) en Frecuencia y Gasto, pero su puntaje de Recencia es bajo (1 o 2). Gastaban mucho y seguido, pero hace mucho no vuelven. ¡Son la "bomba de tiempo"!

c. Clientes Nuevos: (Patrón Regex: ^[3-4]1[1-2]$)
 Los que acaban de llegar. Tienen un puntaje de Recencia alto (3 o 4), pero su Frecuencia es la peor (1) y su Gasto es bajo (1 o 2). Son los "One-and-Done" que hay que fidelizar.

d. Clientes Perdidos: (Patrón Regex: ^[1-2]11$)
 Los peores clientes. Puntuación baja en casi todo. Recencia baja (1 o 2), Frecuencia (1) y Gasto (1).

e. Clientes Promedio: (Patrón Regex: ^[2-3][2-3][2-3]$)
 Los que están "en el medio". Sus puntajes son moderados (2 o 3) en las tres categorías. Son la "panza" del negocio, que hay que cultivar para moverlos a VIP.

f. Otros:
  Este es el "cajón de sastre". Incluye a todos los clientes con combinaciones mixtas (ej. '421' - compró hace poco, pero ni seguido ni mucho) que no cayeron en las 5 reglas principales. El gran tamaño de este grupo justifica una "Fase 2" de este proyecto, donde se podrían aplicar técnicas de clustering (como K-Means) para descubrir sub-segmentos ocultos en él.

---

## 3. Hallazgos Clave: El Dashboard 📈

El análisis de RFM pintó un retrato muy claro de la base de clientes.

<img width="1790" height="1240" alt="image" src="https://github.com/user-attachments/assets/693930b8-1305-47fb-bb00-ebbda1bfdd28" />

Lo que nos dice este "Mapa":
A primera vista, podemos sacar 4 conclusiones de negocio clave:
El Gasto NO está distribuido por igual: El gráfico de "Gasto Promedio" (arriba-derecha) es el más impactante. Los 'Clientes VIP' gastan, en promedio, más del doble que cualquier otro segmento. Esto confirma que no todos los clientes valen lo mismo.
La Frecuencia es un problema real: El gráfico de "Frecuencia" (abajo-izquierda) muestra que la gran mayoría de los clientes (Nuevos, Perdidos, Promedio, Otros) son "One-and-Done". Compran una o dos veces y no vuelven. Los únicos que eran leales eran los VIPs y los 'En Riesgo'.
Hay una "Bomba de Tiempo": El segmento 'Clientes en Riesgo' es la gran alarma. Eran clientes leales (alta frecuencia) y gastaban bien, pero el gráfico de "Recencia" (abajo-derecha) muestra que no han vuelto en casi un año. Estamos a punto de perderlos para siempre.
El Tamaño de los Grupos: El gráfico de "Cantidad" (arriba-izquierda) nos da la escala. Los 'VIPs' y los 'Otros' son nuestros grupos más grandes, pero también tenemos un número preocupante de 'Clientes Perdidos' (829) y 'En Riesgo' (657) sobre los que hay que actuar.

---

## 4. Recomendaciones Estratégicas

Basado en los hallazgos, las acciones recomendadas son:
* **1. Clientes VIP:**
    * **Perfil:** Compran seguido, gastan mucho y vinieron hace poco.
    * **Acción:** **Retener y Deleitar.** No dar descuentos. Ofrecer acceso anticipado, envíos gratis, regalos.
* **2. Clientes en Riesgo:**
    * **Perfil:** Eran VIPs (gastaban mucho y seguido), pero hace mucho no compran.
    * **Acción:** **Reactivación Urgente.** Usar campañas de "Te extrañamos" con descuentos agresivos (ej. 20%).
* **3. Clientes Nuevos:**
    * **Perfil:** Compraron una sola vez, hace poco y gastaron poco.
    * **Acción:** **Fomentar la Frecuencia.** Ofrecer un descuento en la *segunda* compra para convertirlos en clientes leales.
* **4. Clientes Perdidos:**
    * **Perfil:** Compraron una vez, hace mucho y gastaron poco.
    * **Acción:** **No invertir.** Mantener en el newsletter general, pero no gastar presupuesto de marketing en ellos.
* **5. Clientes Promedio:**
    * **Perfil:** Compran y gastan de forma moderada. Son la "panza" del negocio.
    * **Acción:** **Cultivar y Vender más.** Moverlos hacia VIP. Ofrecer programas de puntos o recomendaciones personalizadas.
* **6. Otros:**
    * **Perfil:** Un grupo mixto que no encajó en las reglas principales.
    * **Acción:** **Monitorear (o Re-segmentar).**  No se aplica una estrategia por ahora.

Al final de este análisis, logramos transformar una base de datos caótica de transacciones en un mapa estratégico claro. Pasamos de "adivinar" a "diagnosticar".
En lugar de tener una conversación ineficiente con miles de clientes, la empresa ahora tiene la capacidad de tener 6 conversaciones personalizadas y rentables. Puede enfocarse en maximizar la retención de sus VIPs y, más importante aún, actuar sobre los "Clientes en Riesgo" antes de que sea demasiado tarde.
Acá es donde los datos se vuelven útiles. Este proyecto convirtió datos crudos en información; de esa información surgieron insights clave; y esos insights en un plan de acción. Este es el proceso que permite tomar decisiones estratégicas basadas en evidencia, que son las que realmente impactan de forma positiva en el ROI.
