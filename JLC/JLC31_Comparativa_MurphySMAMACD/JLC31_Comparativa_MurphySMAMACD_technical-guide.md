# [JLC31 Comparative] SMA 10w/40w + weekly MACD · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (criterio de Murphy recogido por Cava en *Sistemas de especulación en bolsa*, apartado IX.2; en adelante SEB. El MACD se cita de *El arte de especular*; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja las medias simples de 10 y 40 semanas del símbolo del gráfico y su MACD semanal. Colorea el fondo según dónde cierra el precio respecto a las medias y marca con triángulos los cruces del MACD que van en la dirección de las medias. Está pensado para un gráfico de ratio entre dos símbolos: mide fuerza relativa, no el precio de un valor suelto. Es un indicador de tendencia intermedia: se lee en semanal.

## Qué dice la fuente

- **Murphy según Cava (SEB IX.2, p. 198):** Cava presenta a Murphy como un analista que se limita a detectar la tendencia de cada mercado con líneas de tendencia, medias móviles, volúmenes e indicadores de momento. Con ellas hace un análisis sectorial: parte de un conjunto de sectores que representa el 80 % del S&P 500 y determina cuáles lideran el movimiento del mercado, cuáles se comportan mejor y cuáles van retrasados; es decir, la fortaleza relativa de un sector frente a los índices y frente a los demás sectores. Fijado el sector más fuerte, pasa a identificar valores dentro de él.
- **Medias de 10 y 40 semanas y MACD semanal (SEB IX.2, p. 199 según la cabecera del script):** el script atribuye a este apartado las dos medias, la zona por encima de ellas y el MACD semanal, descritos en prosa y sin fórmula de cruce combinado.
- **Medias de 10, 20 y 40 semanas (SEB IX.1.2, p. 188):** aquí habla Cava, no Murphy. Dice que no hay medias mágicas; para detectar tendencias en cualquier mercado suele usar una media simple de 20 días y otra de 40 semanas, y para tendencias intermedias suelen funcionar las de 10, 20 y 40 semanas. Son referencias: los periodos óptimos de cada producto se buscan por prueba y error.
- **Definición del MACD (EA IV.1, p. 101):** la línea rápida es la diferencia entre dos medias exponenciales, que suelen ser de 12 y 26 periodos; la lenta es una media exponencial de 9 periodos de la rápida. Cada uno puede usar otros periodos.
- **Cruces del MACD (EA IV.2.2, p. 103; IV.2.2.2, pp. 105-106):** la forma más sencilla de operar con el MACD son los cruces de sus dos líneas; cuando la rápida supera a la lenta se desencadena una compra. La señal es más fiable cuanto más cerca de cero se produce el cruce (p. 105), y los cruces en gráficos semanales o mensuales son muy significativos (p. 106).

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Media corta | 10 semanas | El script la atribuye a SEB IX.2, p. 199; Cava cita las de 10, 20 y 40 semanas para tendencias intermedias (SEB IX.1.2, p. 188) |
| Media larga | 40 semanas | Igual que la media corta |
| MACD | 12 / 26 / 9 | Valores habituales del MACD (EA IV.1, p. 101); aplicarlos a este criterio es `[Propuesta]` |
| Zona verde y gris | Cierre sobre ambas medias / solo sobre la de 40 | El script las atribuye a SEB IX.2, p. 199 |
| Triángulo de compra | Cruce al alza del MACD con la media corta sobre la larga | `[Propuesta]`: la fuente lo describe en prosa, sin fórmula |
| Triángulo de venta y alerta de venta | Cruce a la baja con la media corta bajo la larga | `[Propuesta]`: simétrica de la de compra |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| SMA 10s (azul) | Media simple de 10 semanas del cierre, en el gráfico principal | Referencia corta. En un ratio A/B, el cierre por encima indica que A rinde mejor que B en las últimas semanas; por debajo, peor `[Elaboración]` |
| SMA 40s (naranja) | Media simple de 40 semanas del cierre, en el gráfico principal | Referencia larga: la tendencia de fondo de la fuerza relativa `[Elaboración]` |
| Fondo verde | Cierre por encima de las dos medias | Zona que el script marca como recomendada: la fuerza relativa va a favor en las dos escalas `[Elaboración]` |
| Fondo gris | Cierre por encima de la media de 40 semanas y no de la de 10 | La tendencia larga se conserva y la corta se ha enfriado `[Elaboración]` |
| Sin fondo | Cierre por debajo de la media de 40 semanas | Fuera del criterio |
| MACD (verde) y Señal (roja) | MACD semanal y su línea de señal, en el panel propio | Sus cruces, filtrados por las medias, dan los triángulos |
| Cero (gris) | Nivel de equilibrio del MACD | Referencia: el script no lo usa en ninguna condición |
| Triángulo verde, abajo | El MACD cruza al alza su señal con la media corta sobre la larga | Cruce a favor de la dirección de las medias `[Propuesta]` |
| Triángulo rojo, arriba | El MACD cruza a la baja su señal con la media corta bajo la larga | Cruce a favor de la dirección de las medias `[Propuesta]` |

## Cómo funciona, paso a paso

1. **Marco de cálculo.** Con «Forzar temporalidad semanal» activado, medias, MACD y cierre se piden en semanal (`W`) al símbolo del gráfico con `request.security`, sin adelantar datos futuros. Desactivado, se piden en la temporalidad del gráfico.
2. **Barra de lectura.** Con «Leer solo la barra cerrada» activado, cada valor se desplaza una barra del marco elegido y se lee la última barra cerrada. Desactivado, se lee la barra en curso. El desplazamiento se aplica dentro de la función que recibe `request.security`, porque Pine no admite el operador de historial sobre el resultado de una llamada ni sobre la tupla que devuelve `ta.macd()`.
3. **Medias.** `ta.sma(close, longitud)` con 10 y 40.
4. **MACD.** `ta.macd(close, 12, 26, 9)`: línea MACD y línea de señal.
5. **Cierre de referencia.** El cierre, en el mismo marco y con el mismo desplazamiento que las medias, para no comparar un cierre diario con medias semanales.
6. **Zonas.** «Por encima de ambas»: cierre mayor que la media corta y que la larga. «Por encima de la larga»: cierre mayor que la media larga. Fondo verde en el primer caso, gris en el segundo, ninguno en los demás.
7. **Triángulos `[Propuesta]`.** Compra: el MACD cruza al alza su señal y la media corta es mayor que la larga. Venta: cruza a la baja y la media corta es menor que la larga.
8. **Alertas.** Las cuatro de la guía operativa: los dos cruces, la entrada en la zona de fondo verde y la pérdida de la media de 40 semanas. Avisan del cambio, no del estado.
9. **Repintado.** Con la lectura en barra cerrada, la señal no cambia después de aparecer; la contrapartida es ir una barra del marco elegido por detrás. Sin ella, la señal puede desaparecer antes del cierre de la barra en curso.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| Fondo verde | El ratio cierra por encima de sus medias de 10 y 40 semanas: el activo del numerador rinde mejor que el del denominador en las dos escalas `[Elaboración]` | No es una orden de compra ni dice que el numerador suba en términos absolutos |
| Fondo gris | El ratio conserva la media de 40 semanas y ha perdido la de 10: la ventaja se ha enfriado, la tendencia larga sigue `[Elaboración]` | No es un giro de tendencia |
| Sin fondo | El ratio cierra por debajo de su media de 40 semanas: fuera del criterio | No es una señal de venta del activo: solo dice que el ratio ha perdido su tendencia larga |
| Triángulo verde o rojo | El MACD semanal cruza su señal en el mismo sentido que marcan las medias `[Propuesta]` | No es una regla de Cava: la condición combinada es del script |
| El MACD cruza al alza con la media corta bajo la larga | El cruce va contra la dirección de las medias y el script no lo marca | No significa que el cruce no exista: el filtro lo descarta |
| Triángulo con el MACD lejos de cero | Cruce válido para el script | Cava da más fiabilidad a los cruces cercanos a cero (EA IV.2.2.2, p. 105) y el script no lo comprueba |

## Cuándo usarlo y cuándo no

- **Sí:** sobre un gráfico de ratio entre dos símbolos (un sector frente a su índice, un activo frente a su sector), en semanal, para ver cuál de los dos lidera.
- **No:** sobre el precio de un valor suelto, donde la lectura de fuerza relativa no aplica; en un gráfico mensual con el semanal forzado, porque el script pediría un marco inferior al del gráfico; en marcos intradía.
- **Mal uso frecuente:** tratar el triángulo como orden de compra o de venta; esperar la señal dentro de la semana con el semanal forzado y la lectura en barra cerrada; buscar el fondo en el panel principal, cuando se pinta en el panel del MACD.

## Qué NO dice

- No dice qué comprar ni cuándo entrar en nada concreto.
- No reproduce el análisis sectorial de Murphy: la selección de sectores que suman el 80 % del S&P 500 y el reparto entre líderes y rezagados (SEB IX.2, p. 198). Dibuja la fuerza relativa del gráfico que se le da. `[Hueco declarado]`
- No usa líneas de tendencia ni volúmenes, que Murphy emplea también (SEB IX.2, p. 198). `[Hueco declarado]`
- No filtra los cruces por su distancia al nivel cero (EA IV.2.2.2, p. 105). `[Hueco declarado]`
- La condición que une el cruce del MACD con la dirección de las medias es `[Propuesta]`: no es una fórmula de la fuente.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.2.0.0 | 2026-11-21 | Guía técnica para el código 0.2.0.0 |
| 0.3.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.2.0.0. Citas contrastadas con SEB (pp. 188 y 198) y EA (pp. 101-106) |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script |
