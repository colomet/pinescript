# [JLC81 Pack] Price: moving averages + displaced averages + pivots · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC81 Pack] Price: moving averages + displaced averages + pivots` |
| Nombre corto | `JLC81 Price` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del valor en el marco con el que operes. El script no fuerza ningún marco: usa el del gráfico.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el precio, sin panel aparte: las medias, las medias desplazadas, los triángulos de máximo y mínimo aislado y sus líneas.
4. Todo se enciende y se apaga por separado. Vienen encendidas las piezas de fuente (EMA 20, EMA 55 y las tres medias desplazadas) y los máximos y mínimos aislados con sus líneas. Vienen apagadas la EMA 50, la SMMA 150 y el fondo de tendencia.
5. Las medias desplazadas se proyectan hacia delante: sus últimos tramos quedan sobre barras que aún no existen. Es lo que significa «desplazada».

## Ajustes

Tres grupos en el diálogo del indicador: «De fuente (Cava)», «[Aportado] — no procede de Cava» y «Pivotes [Propuesta]». Las longitudes y los desplazamientos de las medias desplazadas (3x3, 7x5 y 25x5), los colores y los grosores son fijos: no se ajustan.

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| EMA 20 · retroceso con ADX (VIII.6.6) | Sí | Muestra la EMA 20 (azul). El texto del ajuste recuerda la regla de Cava, que usa el ADX; el indicador no calcula el ADX | Apágalo si no usas los retrocesos a la EMA 20. Las alertas de la EMA 20 saltan aunque la línea esté oculta |
| EMA 20 · período | 20 | Período de la EMA 20 (mínimo 1). También rige las alertas de la EMA 20 | 20 es el período de Cava. Si lo cambias, los nombres siguen diciendo 20 |
| EMA 55 · predisposición (Cap. I) | Sí | Muestra la EMA 55 (verde azulado) | Apágalo si no usas el sistema de la media de 55 sesiones. La alerta de la EMA 55 salta aunque la línea esté oculta |
| EMA 55 · período | 55 | Período de la EMA 55 (mínimo 1). También rige la alerta de la EMA 55 | 55 es el período de Cava. Si lo cambias, los nombres siguen diciendo 55 |
| Medias desplazadas 3x3 / 7x5 / 25x5 (I.5.2) | Sí | Muestra las tres medias simples desplazadas hacia delante. Longitudes y desplazamientos fijos | Apágalo si no usas ese criterio de tendencia. El criterio, el fondo y las alertas siguen calculándose |
| Colorear fondo según las desplazadas | No | Pinta el fondo de verde suave si el precio está por encima de las tres medias desplazadas y de rojo suave si está por debajo de las tres; sin color si discrepan. Tiene explicación al pasar el ratón (tooltip) | Actívalo para ver el criterio de un vistazo. Funciona aunque las líneas estén ocultas |
| EMA 50 [Aportado] | No | Muestra la EMA 50 (gris) | Solo si la usas por criterio propio: no procede de Cava |
| EMA 50 · período | 50 | Período de la EMA 50 (mínimo 1) | Solo cuenta si la EMA 50 está activada |
| SMMA 150 [Aportado] | No | Muestra la SMMA 150 (violeta): la media de Wilder (RMA) de 150 períodos | Solo si la usas por criterio propio: no procede de Cava |
| SMMA 150 · período | 150 | Período de la SMMA 150 (mínimo 1) | Solo cuenta si la SMMA 150 está activada |
| Máximos/mínimos aislados | Sí | Marca con un triángulo cada máximo aislado (rojo, sobre la barra) y cada mínimo aislado (verde, bajo la barra) | Apágalo si no quieres las marcas; apaga también las líneas proyectadas |
| Velas izquierda (filtro) | 5 | Velas a la izquierda con las que se compara un máximo o un mínimo para darlo por aislado (mínimo 1) | `[Propuesta]`: Cava, tomando a Drummond, define el aislado con un día a cada lado; el 5 es del script. Con menos velas salen más marcas y menos relevantes |
| Velas derecha (confirmación) | 5 | Velas a la derecha con las que se compara. El pivote se confirma esas velas después de formarse, y el triángulo se dibuja ya sobre el propio máximo o mínimo (mínimo 1) | Con menos velas la marca aparece antes y con menos confirmación; con más, más tarde |
| Proyectar líneas de soporte/resistencia | Sí | Proyecta hacia la derecha una línea discontinua desde el último máximo aislado (roja) y otra desde el último mínimo aislado (verde). Solo se conserva la última de cada tipo | Apágalo si las líneas estorban. Necesita «Máximos/mínimos aislados» activado |

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| EMA 20 · período | 20 | 20 sesiones | 20 semanas |
| EMA 55 · período | 55 | 55 sesiones | 55 semanas |
| EMA 50 · período | 50 | 50 sesiones | 50 semanas |
| SMMA 150 · período | 150 | 150 sesiones | 150 semanas |
| Velas izquierda (filtro) | 5 | 5 sesiones | 5 semanas |
| Velas derecha (confirmación) | 5 | 5 sesiones | 5 semanas |

Las medias desplazadas tienen longitud y desplazamiento fijos: 3 períodos desplazados 3, 7 desplazados 5 y 25 desplazados 5. En diario son sesiones; en semanal, semanas. El script usa el marco del gráfico; no fuerza ninguno. El pivote se confirma 5 barras después de formarse: en diario, una semana.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| EMA 20 | Línea azul, grosor 2 | Media exponencial de 20 sesiones |
| EMA 55 | Línea verde azulada, grosor 2 | Media exponencial de 55 sesiones |
| EMA 50 [Aportado] | Línea gris, grosor 1 | Media exponencial de 50 sesiones. No procede de Cava |
| SMMA 150 [Aportado] | Línea violeta, grosor 1 | Media de Wilder de 150 períodos. No procede de Cava |
| SMA 3x3 | Línea naranja, grosor 1 | Media simple de 3 períodos, desplazada 3 hacia delante |
| SMA 7x5 | Línea amarilla, grosor 1 | Media simple de 7 períodos, desplazada 5 hacia delante |
| SMA 25x5 | Línea marrón, grosor 1 | Media simple de 25 períodos, desplazada 5 hacia delante |
| Tendencia por medias desplazadas (I.5.2) | Fondo verde o rojo muy suave | Verde: el precio está por encima de las tres desplazadas. Rojo: por debajo de las tres. Sin color: discrepan. Solo con «Colorear fondo según las desplazadas» |
| Máximo aislado | Triángulo rojo hacia abajo, sobre la barra, pequeño | Máximo aislado confirmado. Se dibuja sobre el propio máximo |
| Mínimo aislado | Triángulo verde hacia arriba, bajo la barra, pequeño | Mínimo aislado confirmado. Se dibuja sobre el propio mínimo |
| Línea del último máximo | Línea roja discontinua, hacia la derecha | Nivel del último máximo aislado |
| Línea del último mínimo | Línea verde discontinua, hacia la derecha | Nivel del último mínimo aislado |

## Alertas

Cinco, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `Precio · recupera la EMA20` | El cierre cruza al alza la EMA 20 |
| `Precio · pierde la EMA20` | El cierre cruza a la baja la EMA 20 |
| `Precio · pierde la EMA55` | El cierre cruza a la baja la EMA 55 |
| `JLC81 Desplazadas · las tres al alza` | El precio pasa a quedar por encima de las tres medias desplazadas, cuando antes no lo estaba |
| `JLC81 Desplazadas · las tres a la baja` | El precio pasa a quedar por debajo de las tres medias desplazadas, cuando antes no lo estaba |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Cada una lleva su mensaje explicativo. Recomendado `[Propuesta]`: una vez por cierre de vela.

Ninguna depende de los interruptores de mostrar: saltan aunque la línea o el fondo estén ocultos. No hay alerta para la recuperación de la EMA 55. La alerta `Precio · recupera la EMA20` es solo el primer paso de la regla de Cava: el indicador no calcula el ADX ni mira el MACD y el estocástico que la regla pide.

Mientras la barra se forma, el cierre es el último precio y el cruce puede deshacerse; «una vez por cierre de vela» solo avisa si la barra termina cruzada.

## Marcos temporales

El del gráfico. La fuente plantea las medias de 20 y de 55 sesiones en diario, y aplica las desplazadas 3x3 y 7x5 a semanal y diario. El código no fuerza ningún marco. El script no espera al cierre de la barra: mientras se forma, las medias, el fondo y las marcas pueden cambiar; al cerrar, quedan fijos.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.2.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)»); nombres de alerta con su prefijo exacto |
