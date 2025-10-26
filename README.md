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
