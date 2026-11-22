# [JLC42 Trend] Dashboard: MACD + stochastic + CCI + ADX/DI + EMA, monthly/weekly/daily · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (tablero con los indicadores del método de Cava en *El arte de especular*; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Una tabla sobre el gráfico de precio, sin dibujar nada más, que muestra a la vez cinco indicadores del método de Cava (MACD, estocástico, CCI, ADX/DI y medias exponenciales) en tres marcos: mensual, semanal y diario. Resuelve el problema de las escalas: el MACD (unidades de precio), el CCI (sin límites) y el estocástico (de 0 a 100) no caben en un panel sin deformar alguno, pero en una tabla se comparan estados y no alturas. La fila TENDENCIA repite el semáforo de EA I.5.3 y añade un recuento de coincidencia en el marco diario. Se aplica sobre el gráfico diario.

## Qué dice la fuente

- **Definición de tendencia (EA I.5.3, p. 37):** alcista con el MACD mensual cortado al alza, la línea rápida del MACD semanal sobre cero y la línea rápida del estocástico semanal sobre 60; bajista con las tres condiciones inversas y el estocástico bajo 40.
- **Jerarquía de marcos (EA I.4, p. 29, según la cabecera del script):** vigilar a diario el precio y los indicadores de momento en los gráficos mensual, semanal y diario: mensual para el cambio de tendencia, semanal para la dirección dominante y diario para el momento de entrada. La tabla es esa vigilancia en una pantalla.
- **Coincidencia de indicadores (EA III.1.4, p. 80):** para confirmar un cambio de tendencia debe coincidir más de un indicador de momento (el MACD, el estocástico, los DI y el ADX, y las medias, por ejemplo); uno solo es insuficiente. Cuanto mayor es el intervalo del gráfico, más significativa es la señal.
- **MACD (EA IV.1, p. 101; IV.2.1, p. 102; IV.2.2, p. 103):** línea rápida = diferencia de dos medias exponenciales (12 y 26) y lenta = media exponencial de 9 de la rápida. Que la línea rápida supere el nivel cero es señal de inicio de una tendencia alcista, y que lo pierda, de una bajista; es muy significativa en semanal y mensual. El cruce de las dos líneas no debe operarse solo: hay que situarlo en el marco de la tendencia dominante y de su fortaleza.
- **Estocástico (EA V.1.1, p. 141; V.1.2, p. 143):** intervalo habitual de 14 periodos; la %K es la línea rápida. Las lecturas cerca de 80 se consideran sobrecompra y las cercanas a 20, sobreventa.
- **CCI (EA VII.1, pp. 185-186; VII.3.1, pp. 187-188):** se calcula con el precio «significativo» (media del máximo, el mínimo y el cierre) frente a su media simple, y se divide por una constante por la media de las desviaciones. Cava prefiere 14 periodos. Considera sobrecompra por encima de 50 y sobreventa por debajo de -50, salvo que a simple vista sean más significativos el 100 y el -100. Las señales están siempre condicionadas al sentido de la tendencia: en una alcista, la señal de compra llega cuando el CCI supera 50, y eso indica una tendencia fuerte.
- **ADX y DI (EA VIII.5.1, p. 207; VIII.6, p. 208; VIII.6.4, pp. 214-215):** Wilder trabaja con 14 periodos (Elder propone 13; no hay periodo mágico). El ADX mide la fuerza de la tendencia, no su dirección. Se suele considerar que lecturas por encima de 40 indican una tendencia fuerte y por debajo de 20, una tendencia leve o un movimiento lateral. El DI que domina (+DI o -DI) indica qué fuerzas controlan el precio (EA VIII, p. 212).
- **ADX como filtro y la media de 20 (EA VIII.6.6, pp. 216-217):** con el ADX sobre 30, con pendiente positiva y sobre los DI, el mercado tiene tendencia y los sistemas seguidores son fiables; si cae por debajo de 30, dejan de serlo. Muchos especuladores aprovechan los retrocesos a la media exponencial de 20 sesiones para incorporarse a la tendencia cuando el ADX tiene pendiente positiva o supera 30. En la nota 68 (p. 216), Cava dice trabajar con medias de 5, 10, 20 y 40, y que muchos especuladores usan valores de la serie de Fibonacci, el 55 entre ellos.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Marcos | Mensual, semanal y diario | EA I.4, p. 29 (según la cabecera del script) |
| Semáforo | Tres condiciones: MACD mensual, MACD semanal y %K semanal | EA I.5.3, p. 37 |
| MACD | 12 / 26 / 9 | EA IV.1, p. 101 |
| Estocástico %K | 14, sin suavizar | EA V.1.1, p. 141 |
| Niveles 80 y 20 (texto del marco diario) | Sobrecompra y sobreventa | EA V.1.2, p. 143 |
| Niveles 60 y 40 | Alto y bajo en mensual y semanal; color en los tres marcos | EA I.5.3, p. 37 para el semanal. Su uso en el mensual y en el color del diario es `[Elaboración]` |
| CCI | 14 | EA VII.1, p. 186; VII.3.1, p. 187 |
| Umbral del CCI | ±50 (ajustable) | EA VII.3.1, p. 187 |
| Constante del CCI | 0,015 | `[Elaboración]`: es el valor habitual de Lambert. EA VII.1, pp. 185-186, imprime 0,15 en la fórmula y en el texto; con 0,15 los niveles ±50 y ±100 de la propia fuente quedarían fuera de escala |
| ADX y DI | 14 | EA VIII.5.1, p. 207 |
| ADX bajo 20 y sobre 40 | «sin tend.» y «muy fuerte» | EA VIII.6, p. 208 |
| ADX sobre 30 | «fuerte» | EA VIII.6.6, p. 216 |
| Etiquetas «media», «fuerte», «muy fuerte» y «sin tend.» | Cuatro tramos del ADX | `[Elaboración]`: la fuente da los niveles, no los nombres |
| EMA corta | 20 | EA VIII.6.6, p. 217 |
| EMA larga | 55 | Cabecera del script. EA VIII.6.6, nota 68 (p. 216), solo menciona el 55 como valor de Fibonacci |
| Recuento n↑ / n↓ | Seis lecturas del marco diario | `[Propuesta]`: lectura de la exigencia de EA III.1.4, p. 80; la fuente no da cifra |
| Alertas de cinco de seis | Cinco o más lecturas | `[Propuesta]` |
| Lectura de barras cerradas (por defecto) | Mensual y semanal desplazados una barra | `[Propuesta]` |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Columnas MENSUAL, SEMANAL y DIARIO | Estado de cada indicador en cada marco | Verde al alza, rojo a la baja, gris neutro; el ADX va aparte |
| Fila «MACD corte» | Línea rápida frente a su señal | Cruce del MACD (EA IV.2.2, p. 103), como estado |
| Fila «MACD vs 0» | Línea rápida frente a cero | Nivel cero (EA IV.2.1, p. 102) |
| Fila «Estoc. %K» | %K en cada marco | «alto» y «bajo» según 60 y 40; en el diario, «sobrec.» y «sobrev.» según 80 y 20 |
| Fila «CCI» | CCI en cada marco frente al umbral | «sobrec.» verde: sobre +umbral; «sobrev.» rojo: bajo -umbral |
| Fila «ADX fuerza» | ADX en cada marco | Fuerza, no dirección: «sin tend.», «media», «fuerte», «muy fuerte» |
| Fila «DI dirección» | +DI frente a -DI | Qué fuerzas dominan |
| Fila «Precio vs EMA» | Cierre frente a la EMA corta y la larga | Posición del precio `[Elaboración]` |
| Fila «TENDENCIA» | Semáforo, referencia y recuento diario | Manda el estado; el recuento es informativo `[Propuesta]` |

## Cómo funciona, paso a paso

1. **Marcos.** El mensual y el semanal se piden al propio símbolo, sin usar datos que aún no existen. El diario se calcula sobre el marco del gráfico.
2. **Barras cerradas.** Con la opción activada (por defecto), el mensual y el semanal se desplazan una barra y se usa la última cerrada. El diario no se desplaza.
3. **MACD.** Línea rápida = media exponencial rápida menos lenta; señal = media exponencial de la rápida. La tabla da dos lecturas: la rápida frente a su señal y la rápida frente a cero.
4. **Estocástico %K.** 100 × (cierre − mínimo de los mínimos de n barras) ÷ (máximo de los máximos − mínimo de los mínimos). Si el rango es cero, arrastra el último valor válido y, si no hay ninguno, vale 50. Sin suavizar.
5. **CCI.** Precio significativo = (máximo + mínimo + cierre) ÷ 3. CCI = (precio significativo − su media simple de n barras) ÷ (0,015 × desviación media). Si la desviación es cero, arrastra el último valor válido y, si no hay ninguno, vale 0.
6. **ADX y DI.** Se calculan con el periodo de los ajustes, el mismo para los DI y para el ADX.
7. **Medias.** Se compara el cierre con la media exponencial corta y la larga de cada marco.
8. **TENDENCIA.** Alcista si el MACD mensual está sobre su señal, el MACD semanal sobre cero y el %K semanal sobre 60; bajista con las tres inversas y el %K bajo 40; INDEFINIDO en cualquier otro caso.
9. **Recuento diario.** Seis lecturas al alza: MACD sobre su señal, MACD sobre cero, %K sobre 60, CCI sobre el umbral, +DI sobre -DI y cierre sobre la EMA corta. Seis a la baja: las contrarias. El ADX y la EMA larga no cuentan. `[Propuesta]`
10. **Alertas.** Las tres de TENDENCIA saltan cuando el estado cambia al indicado. Las dos de cinco de seis saltan cuando el recuento llega a cinco o más tras haber estado por debajo.
11. **Repintado.** Mensual y semanal no repintan con barras cerradas; el diario cambia hasta el cierre de la barra.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| TENDENCIA en ALCISTA o BAJISTA | Las tres condiciones de Cava coinciden (EA I.5.3, p. 37) | No es una señal de compra o de venta: fija el sentido en el que se leen las señales (EA VII.3.1, p. 188) |
| TENDENCIA en INDEFINIDO | Las tres condiciones no concuerdan: Cava no define tendencia `[Elaboración]` | No es un fallo; el resto de la tabla es contexto y no permiso para entrar |
| Recuento diario de 5 o 6 en un sentido | Casi todas las lecturas del marco diario coinciden: la exigencia de EA III.1.4, p. 80 `[Propuesta]` | No sustituye al semáforo: el recuento es solo del marco diario |
| CCI «sobrec.» en verde | El CCI supera el umbral; con tendencia alcista, Cava lo lee como señal de compra y de tendencia fuerte (EA VII.3.1, p. 188) | No es por sí mismo una señal de venta: Cava lo lee en el sentido de la tendencia |
| ADX «sin tend.» | Tendencia leve o movimiento lateral (EA VIII.6, p. 208) | No dice hacia dónde saldrá el precio: el ADX no mide dirección (EA VIII.5.1, p. 207) |
| ADX «fuerte» o «muy fuerte» | Fuerza de tendencia suficiente para fiarse de los sistemas seguidores, si además tiene pendiente positiva y está sobre los DI (EA VIII.6.6, p. 216) | La tabla no muestra la pendiente del ADX ni su posición frente a los DI |
| Precio sobre o bajo la EMA | Posición del cierre frente a la media `[Elaboración]` | En la fuente la media de 20 sirve de soporte o resistencia en los retrocesos de una tendencia con ADX sobre 30 (EA VIII.6.6, p. 217), no de señal por sí sola |

## Cuándo usarlo y cuándo no

- **Sí:** como punto de partida de la sesión, sobre el gráfico diario, para ver en un solo slot y sin deformar escalas el estado de cinco indicadores en tres marcos.
- **No:** como sistema de entrada o de salida, ni en gráficos que no sean diarios, porque la columna DIARIO usa el marco del gráfico.
- **Mal uso frecuente:** tratar el recuento de cinco o seis como una orden; leer el CCI «sobrec.» como señal de venta sin mirar la tendencia; leer la columna DIARIO como diaria en un gráfico semanal; olvidar que la barra diaria en curso cambia durante la sesión.

## Qué NO dice

- No dice cuándo entrar ni cuándo salir.
- No muestra la pendiente del ADX ni su posición frente a los DI, que la fuente exige junto al nivel 30 (EA VIII.6.6, p. 216). `[Hueco declarado]`
- No detecta divergencias ni fallos, que Cava trata en cada indicador (por ejemplo, EA V.1.4 y VII.3.2). `[Hueco declarado]`
- No incluye el RSI ni otros indicadores del método. `[Hueco declarado]`

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 37, 80, 101-103, 141-143, 185-188, 207-208, 212, 214-217) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
