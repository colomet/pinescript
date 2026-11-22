# [GEN81 Pack] RSI and MACD · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Adaptación del script «RSI y MACD Completo» de David Trullás; según la cabecera, el cálculo y el dibujo son los del original. RSI 14, MACD 12-26-9, nivel clave 40 y factor 30 son `[Aportado]`, de Trullás. Las citas de Cava son de *El arte de especular* (EA) |
| Script | Versión 0.1.2.0 (ver control de cambios) |

---

## Qué es

Un pack de dos indicadores en un solo panel debajo del precio: el RSI del cierre (categoría Diagnostic: «¿cuándo entro?») y el MACD con línea, señal e histograma (categoría Trend). La categoría del MACD la asignó Claude por delegación de Antonio `[Interpretación]`. Dibuja además una línea de referencia en el nivel clave del RSI (40 por defecto) y la línea cero del MACD. El MACD va multiplicado por un factor (30 por defecto) solo para verlo a la escala del RSI, que va de 0 a 100: los cruces y las divergencias se mantienen, pero los valores del MACD que se ven no son los reales. No emite señales ni alertas.

Según la cabecera del script, respecto al original cambian la estructura del código, las explicaciones en los ajustes (tooltips y un resumen), los nombres de las series, que ya no llevan cifras fijas, y el color de la línea cero, que pasa a gris y ajustable. El cálculo y el resto del dibujo son los del original.

## Qué dice la fuente

Según la cabecera del script, el RSI de 14 velas, el MACD 12-26-9, el nivel clave 40 y el factor 30 son de Trullás y ninguna fuente los fija aquí `[Aportado]`. Lo que sigue son coincidencias con Cava; no hacen de este script una regla suya.

- **MACD (EA IV.1, p. 101):** la línea rápida es la diferencia entre dos medias exponenciales del cierre, que generalmente son de 12 y 26 períodos; la lenta es una media exponencial de 9 períodos de la rápida; el histograma es la diferencia entre las dos. Cava añade que cada cual puede usar otros períodos. Es el MACD del script.
- **RSI (EA VI.1, p. 165; VI.2, p. 166):** oscilador de Wilder (1978) que va de 0 a 100 y mide la fuerza del movimiento con las diferencias entre cierres (p. 165). Se suele trabajar con 7, 9 o 14 períodos; con 14, los niveles habituales de sobrecompra y sobreventa son 70 y 30 (p. 166). El script dibuja el RSI de 14 velas y no esos niveles.
- **El nivel 40 (EA VI.2, p. 166; VI.5, p. 168; VI.6, p. 176):** en una clara tendencia alcista, algunos especuladores usan 80 y 40 como niveles de sobrecompra y sobreventa (p. 166). Con una tendencia alcista muy acusada es poco probable que el RSI baje de 20, y por eso se suele situar la línea de sobreventa en 40 (p. 168). En tendencias alcistas el RSI diario puede bajar de 50 pero difícilmente pierde el 40, y las lecturas próximas a 40 deberían considerarse sobreventa (p. 176). El 40 del script es de Trullás; coincide con ese nivel de Cava, pero el script solo lo dibuja.
- **RSI y MACD en un mismo panel (EA IV.4.1, pp. 132-134):** Cava combina los dos indicadores solapándolos sin modificar sus escalas, para obtener señales más tempranas que con el MACD solo, que es más retrasado (p. 132). Si las dos líneas del MACD caen y el RSI las cruza al alza, es el primer aviso de que la tendencia bajista pierde fuerza (p. 132); en su ejemplo del Index Dólar, ese cruce al alza anticipó solo un rebote dentro de la tendencia bajista (p. 133). Si las dos líneas suben con clara pendiente y el RSI las cruza a la baja, es el primer aviso de pérdida de fuerza de la alcista (p. 134). Lo decisivo son los cruces del RSI con la línea lenta del MACD, y avisa de que, al ser distinta la escala del MACD, solaparlos exige cuidado (p. 134). El script los dibuja juntos, con el MACD multiplicado por el zoom `[Aportado]`, y no marca esos cruces.
- **Cero y cruces del MACD (EA IV.2.1, p. 102; IV.2.2, p. 103; IV.2.2.2, p. 105):** el cero es el equilibrio: que la línea rápida lo supere es señal de inicio de tendencia alcista, y que lo pierda, de bajista; es muy significativo en gráficos semanales o mensuales (p. 102). El cruce de la rápida sobre la lenta es señal de compra, y a la baja, de venta; Cava no recomienda operar solo por los cruces, sino situarlos en el marco de la tendencia dominante y su fortaleza (p. 103). La señal es más fiable cuanto más cerca de cero se produce el cruce (p. 105).
- **Divergencias (EA III.2.1-III.2.2, pp. 90-92; IV.2.3, p. 109; VI.4, pp. 166-167):** hay divergencia cuando el indicador no confirma el movimiento del precio (p. 90). La alcista es la del precio con mínimos decrecientes e indicador con mínimos crecientes (p. 91); la bajista, la del precio con máximos crecientes e indicador con máximos decrecientes (p. 92). Informa de una pérdida de ímpetu, pero es condición necesaria y no suficiente para el cambio de tendencia: se confirma cuando se cruzan las medias o se perfora la línea «2-4» de la pauta (p. 91). En el capítulo del MACD lo repite y añade como confirmación la rotura de una resistencia o de un soporte significativos (p. 109). En el RSI es la señal más fiable y frecuente (p. 166), y más aún en zona extrema, por encima de 70 o por debajo de 30 (p. 167).

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Periodo del RSI | 14 velas | `[Aportado]`: de Trullás. Es uno de los tres que cita Cava: 7, 9 o 14 (EA VI.2, p. 166) |
| Nivel clave del RSI | 40 | `[Aportado]`: de Trullás. Coincide con la sobreventa de Cava en tendencia alcista (EA VI.2, p. 166; VI.5, p. 168) |
| MACD | Medias exponenciales de 12 y 26 velas del cierre; señal de 9 | `[Aportado]`: de Trullás. Son los habituales de Cava (EA IV.1, p. 101) |
| Factor del MACD | 30 por defecto, de 1 a 200 | `[Aportado]`: de Trullás. Solo cambia la escala del dibujo |
| Límites de los ajustes | Periodo del RSI de 1 a 500 velas; nivel clave de 0 a 100 | Del script |
| Cero del MACD | 0 | Equilibrio del MACD (EA IV.2.1, p. 102) |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea verde (RSI) | El RSI del cierre, de 0 a 100 (14 velas por defecto) | Sube con las subidas recientes y baja con las caídas. Se compara con el nivel clave y con las líneas del MACD (EA IV.4.1, pp. 132-134) |
| Línea gris discontinua (Nivel clave RSI) | Línea horizontal en el valor del ajuste (40 por defecto) | Referencia fija: cruzarla no da señal en el script. En Cava, el 40 es la sobreventa en tendencia alcista (EA VI.5, p. 168) |
| Línea azul (Línea MACD (con zoom)) | Media exponencial de 12 menos media exponencial de 26 del cierre, multiplicada por el zoom | Sobre cero, la media rápida está sobre la lenta; bajo cero, al revés. Su valor no es el real, salvo con zoom 1 |
| Línea roja (Línea de señal (con zoom)) | Media exponencial de 9 de la línea MACD, multiplicada por el zoom | Su cruce con la azul es el cruce clásico del MACD (EA IV.2.2, p. 103) |
| Columnas (Histograma MACD (con zoom)) | Línea MACD menos señal, multiplicada por el zoom; verde azulado sobre cero y granate bajo cero | Cada barra es la diferencia entre las dos líneas (EA IV.1, p. 101): cambia de signo en el cruce |
| Línea gris continua (Línea cero) | El cero del MACD, que es también el 0 de la escala del RSI | Equilibrio: que la línea rápida lo supere se considera señal de inicio de tendencia alcista, y que lo pierda, de bajista (EA IV.2.1, p. 102) |

Los colores son los que trae por defecto; se cambian en el grupo «Aspecto» (ver la guía operativa).

## Cómo funciona, paso a paso

1. Calcula el RSI del cierre con el periodo del ajuste «Periodo RSI (velas)» (el RSI estándar de Pine).
2. Calcula el MACD del cierre con 12, 26 y 9: línea, señal e histograma (el MACD estándar de Pine).
3. Multiplica las tres series del MACD por el mismo factor, el del ajuste «Zoom del MACD (factor)».
4. Dibuja en el mismo panel el histograma en columnas, la línea MACD, la línea de señal y el RSI, más el nivel clave y la línea cero.
5. No compara las líneas entre sí ni con el nivel clave, y no emite señales ni alertas.

**Qué hace el factor y qué no.** Multiplicar las tres series por el mismo número positivo no cambia su orden: los cruces entre ellas, el signo y las divergencias del MACD son los mismos con cualquier factor. Lo que cambia es la cifra: con un factor distinto de 1, los valores del MACD que se ven no son los reales y no sirven para compararlos con otro activo ni con otra herramienta. El factor no se adapta solo al precio del activo: lo elige quien usa el script, y el MACD crece con el precio mientras que el RSI no `[Elaboración]`.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| La línea azul cruza la roja | El cruce clásico del MACD: la rápida supera a la lenta (compra) o la pierde (venta) (EA IV.2.2, p. 103). Es más fiable cuanto más cerca del cero (EA IV.2.2.2, p. 105) | Una entrada: Cava no recomienda operar solo por los cruces, sino dentro de la tendencia dominante (EA IV.2.2, p. 103), y el script no marca el cruce |
| Las columnas cambian de color | El histograma cambió de signo: la línea azul acaba de cruzar la roja | Un aviso aparte: es el mismo cruce que ya se ve entre las dos líneas |
| La línea azul cruza la gris continua (el cero) | La rápida supera o pierde el equilibrio: señal de inicio de tendencia alcista o bajista, muy significativa en gráficos semanales o mensuales (EA IV.2.1, p. 102) | Una señal del script: no la marca |
| El RSI cruza las líneas del MACD | Con las dos líneas del MACD cayendo, que el RSI las cruce al alza es el primer aviso de que la bajista pierde fuerza; con las dos subiendo con clara pendiente, que las cruce a la baja avisa de lo mismo en la alcista (EA IV.4.1, pp. 132 y 134). Lo decisivo es el cruce con la línea lenta, la de señal (p. 134) | Un cambio de tendencia: en el ejemplo del Index Dólar, el cruce al alza del RSI anticipó solo un rebote dentro de la tendencia bajista (p. 133). Tampoco un punto fijo: con otro zoom, el RSI cruza las líneas en otros puntos `[Elaboración]` |
| El RSI cruza el nivel clave | El RSI pasa de un lado a otro de la línea (40 por defecto) | Una señal del script: solo dibuja la línea. En Cava, el 40 forma parte de un sistema con el MACD semanal sobre cero y el RSI diario (EA VI.5, p. 168) |
| El RSI llega a una zona extrema (70 o 30 con 14 velas) | Sobrecompra o sobreventa; las señales del RSI son más fiables en esas zonas (EA VI.2, p. 166) | Una orden de salida: en una tendencia fuerte el RSI llega rápido a un extremo, y cancelar por eso suele ser prematuro (EA VI.4, p. 167). El script no dibuja esos niveles |
| Precio e indicador (RSI o MACD) no se acompañan en dos máximos o dos mínimos seguidos | Divergencia: el movimiento pierde fuerza. Bajista: el precio dibuja máximos crecientes y el indicador, máximos decrecientes (EA III.2.2, p. 92). Alcista: el precio dibuja mínimos decrecientes y el indicador, mínimos crecientes (EA III.2.2, p. 91; la del MACD, EA IV.2.3, p. 109) | Un cambio de tendencia: es condición necesaria y no suficiente (EA III.2.1, p. 91). El script no la marca: se ve a ojo |
| El MACD sale aplastado o se sale del panel | El zoom no encaja con el precio del activo: el adecuado depende de él | Un fallo del cálculo: con cualquier factor, los cruces y el signo son los mismos |

## Cuándo usarlo y cuándo no

- **Sí:** para tener en un solo panel el RSI y el MACD del mismo activo y marco, con el nivel clave y el cero, y mirar a ojo los cruces, las divergencias y el RSI frente a las líneas del MACD, que es la combinación de EA IV.4.1 (pp. 132-134), aquí con el MACD multiplicado por el zoom `[Elaboración]`.
- **No:** para leer valores reales del MACD si el factor no es 1; para comparar el MACD entre activos; para decidir una entrada con un solo cruce o con el nivel 40, porque el script no los señala; para recibir alertas.
- **Mal uso frecuente** `[Elaboración]`: tomar por reales los valores del MACD que muestra el panel (con factor 30 van multiplicados por 30); tomar el nivel 40 por una señal del script; tomar los parámetros 14, 12-26-9, 40 y 30 por reglas de Cava, cuando son de Trullás aunque algunos coincidan con valores habituales de Cava.

## Qué NO dice

- No da entradas ni salidas, y no define alertas.
- No marca los cruces del MACD, los del RSI con las líneas del MACD ni las divergencias.
- Cruzar el nivel clave no es una señal del script.
- Solo dibuja una línea de referencia del RSI, el nivel clave. Los niveles 70 y 30 del RSI de 14 velas (EA VI.2, p. 166) y el eje 50 (EA VI.6, p. 174) solo se ven si se pone uno de ellos como nivel clave, de uno en uno.
- No aplica el sistema de Cava del nivel 40: compra cuando el RSI diario cae bajo 40 y lo recupera, con el MACD semanal sobre cero (EA VI.5, p. 168). El script dibuja la línea y nada más, y no calcula el MACD semanal.
- No mide la tendencia ni la volatilidad.
- Con un factor distinto de 1, el valor del MACD que se lee no es el real.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-14 | Creación. Se refiere al script 0.1.0.0 (GEN61) |
| 0.2.0.0 | 2026-11-21 | Plantilla estándar y código 0.1.0.0. Citas contrastadas con EA (pp. 90-92, 101-103, 105, 109, 132-134, 165-168, 174 y 176) |
| 0.3.0.0 | 2026-11-22 | Renombrada a GEN81 Pack. Categoría Pack (RSI Diagnostic, MACD Trend). Describe el código 0.1.2.0; línea cero gris y ajustable. Las citas de Cava se arrastran de la v0.2.0.0 y no se han recontrastado con el libro en esta versión |
