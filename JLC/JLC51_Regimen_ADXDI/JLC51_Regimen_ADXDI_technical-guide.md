# [JLC51 Regime] ADX/DI: 14 {40/30/20} · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (sistema del movimiento direccional de Wilder según Cava, capítulo VIII de *El arte de especular*; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja en un panel el ADX, el +DI y el -DI de Wilder (periodo 14) y marca dos avisos de inicio de tendencia: la mejor señal de Cava y el giro del ADX de Elder. Los fondos señalan una tendencia fortalecida (ADX sobre 30) y una muy fuerte (ADX sobre 40 y subiendo). Sirve de filtro de régimen: dice si el mercado tiene tendencia y, por tanto, si encajan los sistemas de seguimiento de tendencia o los de sobrecompra y sobreventa. La dirección la dan el +DI y el -DI, no el ADX. Se aplica sobre el gráfico del valor, en el marco con el que se opera.

## Qué dice la fuente

- **ADX (EA VIII.5.1, p. 207):** cociente entre el valor absoluto de la diferencia de los dos DI y su suma, multiplicado por 100, con periodo 14. Cuanto más alto, más fuerte la tendencia. No informa de la dirección: para conocerla basta mirar el gráfico del precio (EA VIII.6.1, p. 208).
- **+DI y -DI (EA VIII.4.1, pp. 203-204):** el DI es el movimiento direccional dividido por el rango verdadero, con periodo 14. El que está por encima indica qué fuerzas controlan el precio: con el -DI por encima, las bajistas (EA VIII.6.3, p. 212).
- **Niveles y pendiente (EA VIII.6.1, p. 208; VIII.6.5, p. 215):** por encima de 40 se considera una tendencia fuerte y por debajo de 20, una tendencia leve o un movimiento lateral. Con pendiente positiva la tendencia se fortalece y con pendiente negativa se debilita. Con el ADX subiendo y sobre 40, los sistemas de seguimiento de tendencia dan resultados magníficos. Subiendo entre 15 y 20, la tendencia es todavía débil pero se fortalece. Si supera 30, la tendencia se ha fortalecido y sigue siendo fuerte aunque pierda la pendiente mientras se mantenga sobre 30.
- **Mejor señal de compra (EA VIII.6.2, pp. 209-210):** el ADX cae por debajo del +DI y del -DI, permanece cierto tiempo con lecturas inferiores a 20, gira al alza, adquiere pendiente positiva y supera al -DI. En ese momento el +DI debe tener pendiente positiva y el -DI estar girado a la baja. Permite incorporarse en la primera onda del movimiento, cuando emerge una nueva tendencia.
- **Mejor señal de venta (EA VIII.6.3, p. 212):** la simétrica: el ADX supera al +DI, con el -DI en pendiente positiva y el +DI girado a la baja. Cuanto menor es el nivel alcanzado por el ADX y más tiempo ha permanecido bajo los DI, mayor es el recorrido posterior.
- **Regla de Elder (EA VIII.6.3, p. 213):** en *Trading for a Living*, Elder considera que la mejor señal del movimiento direccional llega cuando el ADX cae por debajo de los DI, gira al alza y sube de 4 a 12 puntos desde su mínimo. Según Elder, anuncia muy probablemente el comienzo de una nueva tendencia.
- **Periodo (EA VIII.6.4, pp. 214-215):** Cava trabaja con 14, siguiendo la recomendación de Wilder. Elder recomienda 13 y no existe un periodo mágico. Lo habitual es de 5 a 14, y con gráficos semanales quizá convenga 7, a decidir por prueba y error.
- **Filtro de régimen (EA VIII.6.6, pp. 216-217):** algunos especuladores usan el ADX para filtrar las señales de otros sistemas (p. 216). Con pendiente positiva, sobre 30 y sobre los DI hay un mercado con tendencia, y las señales de los sistemas seguidores de tendencia son muy fiables (p. 216). Con el ADX cayendo y lecturas bajo 30, conviene pasar a sistemas de sobrecompra y sobreventa (p. 217).
- **Giro a la baja (EA VIII.6.8, pp. 219-220):** cuando el ADX, tras un tramo al alza, alcanza un máximo y gira a la baja, el precio suele iniciar una consolidación. Si cae por debajo de 30, ya no conviene aplicar sistemas tendenciales (p. 219). Con el ADX bajo los dos DI se obtienen mejores resultados con las Bandas de Bollinger y los niveles de sobrecompra y sobreventa del RSI, el estocástico o el CCI, y Wilder recomienda evitar los sistemas de seguimiento de tendencia (p. 220).
- **Más de un indicador (EA III.1.4, p. 80):** Cava pide que más de un indicador de momento confirme la señal.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Periodo del ADX y de los DI | 14 | EA VIII.4.1, pp. 203-204; VIII.5.1, p. 207; VIII.6.4, p. 214 |
| Nivel 20 | Lectura baja y condición previa de la mejor señal | EA VIII.6.1, p. 208; VIII.6.2, p. 209 |
| Nivel 30 | Tendencia fortalecida | EA VIII.6.5, p. 215 |
| Nivel 40 con pendiente positiva | Resultados magníficos de los sistemas seguidores | EA VIII.6.5, p. 215 |
| Mejor señal de compra | ADX bajo 20 y bajo los dos DI, giro al alza y cruce del -DI | EA VIII.6.2, pp. 209-210 |
| Mejor señal de venta | Lo mismo en sentido contrario: cruce del +DI | EA VIII.6.3, p. 212 |
| Regla de Elder | Subida de 4 a 12 puntos desde el mínimo | EA VIII.6.3, p. 213 |
| Pendiente positiva o negativa | Comparación con la barra anterior | `[Propuesta]`: la fuente habla de pendiente sin medirla |
| Caducidad de la condición previa | 60 barras, ajustable | `[Propuesta]`: la fuente dice «cierto tiempo» sin cifra |
| Desarme por nivel 30 | Activado por defecto | `[Propuesta]` |
| Disparo único de cada marca | Una vez por armado | `[Propuesta]` |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| ADX (verde) | Fuerza de la tendencia | Sube si hay tendencia, suba o baje el precio |
| +DI (azul) y -DI (rojo) | Presión compradora y vendedora | El que está por encima domina |
| Niveles 20, 30 y 40 | Umbrales de la fuente | Bajo 20, tendencia leve; sobre 30, fortalecida; sobre 40, fuerte |
| Fondo gris | ADX sobre 30 | Tendencia fortalecida: terreno de los sistemas seguidores |
| Fondo verde | ADX sobre 40 y subiendo | Tendencia muy fuerte y ganando fuerza; no indica dirección |
| Triángulo verde, abajo | Mejor señal de compra de Cava; el plazo de su condición previa es `[Propuesta]` | Posible inicio de una tendencia alcista |
| Triángulo rojo, arriba | Mejor señal de venta de Cava; el plazo de su condición previa es `[Propuesta]` | Posible inicio de una tendencia bajista |
| Círculo naranja, abajo | Giro del ADX de 4 a 12 puntos desde su mínimo (Elder) | Aviso más temprano y menos estricto que el triángulo; no indica dirección |

## Cómo funciona, paso a paso

1. **ADX y DI.** Se calculan con la función `ta.dmi` de TradingView, con el mismo periodo para el ADX y los DI.
2. **Condición previa de la mejor señal.** Se arma cuando el ADX está bajo 20 y bajo los dos DI, y se renueva en cada barra en que sigue cumpliéndose. Caduca si pasan más barras que la caducidad desde la última vez que se cumplió o, con el ajuste activo, si el ADX supera 30. `[Propuesta]`
3. **Mejor señal de compra.** Con la condición armada: +DI sobre -DI, el ADX cruza al alza el -DI, el +DI sube respecto a la barra anterior y el -DI baja. Marca el triángulo verde y desarma la condición.
4. **Mejor señal de venta.** La simétrica: -DI sobre +DI, el ADX cruza al alza el +DI, el -DI sube y el +DI baja. Marca el triángulo rojo y desarma la condición.
5. **Regla de Elder.** Se arma cuando el ADX está bajo los dos DI. Se sigue el mínimo del ADX mientras cae. La marca sale una sola vez, cuando el ADX sube y la subida desde ese mínimo cruza 4 puntos sin pasar de 12; después se desarma.
6. **Fondos.** Verde si el ADX supera 40 y sube; si no, gris si supera 30.
7. **Barra en curso.** El código no espera al cierre de la barra: una marca puede aparecer y desaparecer mientras se forma y queda fija al cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| ADX bajo 20 y bajo los dos DI | Tendencia leve o movimiento lateral (EA VIII.6.1, p. 208); es la condición previa de la mejor señal | No dice hacia dónde saldrá el precio |
| Triángulo verde | Posible inicio de una tendencia alcista: la mejor señal de compra de Cava (EA VIII.6.2, pp. 209-210) | No es una orden de compra: conviene que la confirmen otros indicadores (EA III.1.4, p. 80) |
| Triángulo rojo | Posible inicio de una tendencia bajista (EA VIII.6.3, p. 212) | No es una orden de venta |
| Círculo naranja | El ADX ha subido de 4 a 12 puntos desde su mínimo tras caer bajo los DI (EA VIII.6.3, p. 213) | No indica dirección: se mira el +DI frente al -DI |
| Fondo gris | ADX sobre 30: tendencia fortalecida (EA VIII.6.5, p. 215) | No dice si es alcista o bajista |
| Fondo verde | ADX sobre 40 y subiendo: los sistemas seguidores dan resultados magníficos (EA VIII.6.5, p. 215) | No es una señal alcista ni de compra: el color no indica dirección |
| ADX alto y cayendo | La tendencia se debilita (EA VIII.6.1, p. 208) | No significa que la tendencia haya terminado: lo más probable es una pausa (EA VIII.6.1, p. 208) |

## Cuándo usarlo y cuándo no

- **Sí:** como filtro de régimen sobre el gráfico del valor, para decidir entre sistemas de seguimiento de tendencia y sistemas de sobrecompra y sobreventa (EA VIII.6.6, pp. 216-217); y como aviso temprano de una tendencia que nace, con el triángulo y el círculo.
- **No:** para saber la dirección de la tendencia por sí solo (se mira el +DI frente al -DI y el gráfico del precio, EA VIII.6.1, p. 208), ni como orden de entrada sin confirmación de otros indicadores (EA III.1.4, p. 80).
- **Mal uso frecuente** `[Elaboración]`: leer un ADX alto como tendencia alcista; tomar el fondo verde por una señal de compra; usar el círculo naranja como señal de dirección.

## Qué NO dice

- No define salidas, stops ni tamaño de la posición.
- No marca el giro a la baja del ADX, que la fuente trata en EA VIII.6.8 (pp. 219-220). `[Hueco declarado]`
- No cruza el ADX con las divergencias de los indicadores de momento: con el ADX subiendo, plano o ligeramente a la baja pero sobre 30, una divergencia anuncia más probablemente un movimiento lateral que el final de la tendencia (EA VIII.6.5.1, pp. 215-216). `[Hueco declarado]`
- No incluye el retroceso a la media exponencial de 20 sesiones como punto de entrada (EA VIII.6.6, p. 217). `[Hueco declarado]`
- La duración de «cierto tiempo» bajo 20 no la cuantifica la fuente: el plazo de 60 barras y el desarme por nivel 30 son `[Propuesta]`.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 80, 203-204, 207-210, 212-217, 219-220) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
