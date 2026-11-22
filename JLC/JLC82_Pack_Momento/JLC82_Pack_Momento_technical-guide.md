# [JLC82 Pack] Momentum: stochastic + ADX/DI + CCI · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (estocástico, ADX con los DI y CCI según Cava, capítulos I, III, V, VII y VIII de *El arte de especular*; en adelante EA). El reescalado visual del CCI está rotulado `[Aportado]` en el código |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Reúne en un solo panel y en un solo indicador tres osciladores de momento: el estocástico de 14 (%K y %D), el ADX con las líneas DI y el CCI de 14. Cada uno se enciende y se apaga por separado, así que el pack sirve también como cualquier pareja de los tres.

Según su cabecera, aplica sin reinterpretarlas las reglas de `JLC62 Stochastic`, `JLC51 ADX` y `JLC63 CCI`, que siguen existiendo por separado. Sirve para ver a la vez si coinciden. El CCI se dibuja reescalado, así que para leer sus niveles con precisión vale `JLC63 CCI`. Las marcas del CCI también difieren de las de ese indicador: aquí son todas moradas, con la larga arriba y la corta abajo del panel.

## Qué dice la fuente

**Estocástico (EA V)**

- **Concepto (EA V.1.1, p. 141):** mide la posición relativa del cierre dentro del rango de un intervalo, que suele ser de 14 días. En una tendencia alcista los cierres tienden a quedar cerca de la parte alta del rango y en una bajista, cerca de los mínimos. Se aplica sobre todo a gráficos diarios, pero sirve también en intradiarios, semanales y mensuales.
- **Las dos líneas (EA V.1.1, pp. 141-143):** %K es la línea continua, la más sensible y rápida (p. 141). %D es la discontinua, la más lenta, y la más significativa: la que da las principales señales (p. 142). %K = 100·(C − L)/(Hn − Ln), con L el mínimo de hoy y Ln y Hn el menor mínimo y el mayor máximo de los n días (p. 142). %D = 100·(H3/L3), con H3 la suma de 3 periodos de (C − Ln) y L3 la suma de 3 periodos de (Hn − Ln) (p. 143).
- **Niveles 80 y 20 (EA V.1.2, pp. 143-145):** lecturas cerca de 80 son sobrecompra y cerca de 20, sobreventa. Con una tendencia fuerte el estocástico permanece mucho tiempo en la zona (p. 143), y la lectura tradicional resulta muy útil con un movimiento lateral o una tendencia escasa (p. 145).
- **Filtro de tendencia (EA I.5.3, p. 37):** la tendencia es alcista cuando, además de las condiciones del MACD, la línea rápida del estocástico semanal está por encima de 60, y bajista cuando está por debajo de 40.
- **Las señales hay que confirmarlas (EA V.1.3, p. 146):** las señales de los indicadores de momento son alarmas que deben confirmarse con el movimiento del precio.

**ADX y DI (EA VIII)**

- **ADX y DI (EA VIII.4.1, pp. 203-204; VIII.5.1, p. 207):** el DI es el movimiento direccional dividido por el rango verdadero. El ADX es el cociente entre el valor absoluto de la diferencia de los dos DI y su suma, por 100. Periodo 14. El ADX no indica la dirección de la tendencia, solo su fuerza (EA VIII.6.1, p. 208).
- **Niveles y pendiente (EA VIII.6.1, p. 208; VIII.6.5, p. 215):** por encima de 40 es una tendencia fuerte y por debajo de 20, una tendencia leve o un movimiento lateral. Con pendiente positiva la tendencia se fortalece y con pendiente negativa se debilita. Si supera 30, se ha fortalecido y sigue siendo fuerte aunque pierda la pendiente mientras se mantenga sobre 30.
- **Mejor señal de compra (EA VIII.6.2, pp. 209-210):** el ADX cae por debajo del +DI y del -DI, permanece cierto tiempo con lecturas inferiores a 20, gira al alza y supera al -DI, con el +DI en pendiente positiva y el -DI girado a la baja. Permite incorporarse en la primera onda de una tendencia nueva.
- **Mejor señal de venta (EA VIII.6.3, p. 212):** la simétrica: el ADX supera al +DI, con el -DI en pendiente positiva y el +DI girado a la baja.
- **Regla de Elder (EA VIII.6.3, p. 213):** en *Trading for a Living*, Elder considera que la mejor señal llega cuando el ADX cae por debajo de los DI, gira al alza y sube de 4 a 12 puntos desde su mínimo.
- **Periodo (EA VIII.6.4, pp. 214-215):** Cava trabaja con 14, siguiendo la recomendación de Wilder. Elder recomienda 13, y con gráficos semanales quizá convenga 7.
- **Régimen (EA VIII.6.6, pp. 216-217; VIII.6.8, p. 220):** con pendiente positiva, sobre 30 y sobre los DI hay un mercado con tendencia, y las señales de los sistemas seguidores de tendencia son muy fiables (p. 216). Con el ADX cayendo y lecturas bajo 30, conviene pasar a sistemas de sobrecompra y sobreventa (p. 217). Con el ADX bajo los dos DI se obtienen mejores resultados con los niveles de sobrecompra y sobreventa del RSI, el estocástico o el CCI (VIII.6.8, p. 220).

**CCI (EA VII)**

- **Cálculo (EA VII.1, pp. 185-186):** el CCI mide cuánto se aleja el precio «significativo», la media del máximo, el mínimo y el cierre, de su media simple, dividido por una constante por la desviación media. Lambert recomendó periodos de 5 a 20 días y Cava prefiere 14. El libro imprime la constante 0,15 (p. 186).
- **Interpretación tradicional (EA VII.2, pp. 186-187):** sobrecompra por encima de 50 o de 100 y sobreventa por debajo de −50 o −100, según el producto. Compra cuando, tras entrar en sobreventa, el CCI gira al alza y supera 0; venta cuando, tras entrar en sobrecompra, gira a la baja y pierde 0 (p. 187).
- **Sistema de Cava (EA VII.3.1, pp. 187-188):** 14 periodos, en semanal, diario o intradiario. Sobrecompra al superar 50 y sobreventa al perder −50, salvo que sean más significativos el 100 y el −100 (p. 187). Las señales están condicionadas siempre al sentido de la tendencia (pp. 187-188). Con tendencia alcista, la señal de compra llega cuando el CCI supera 50 y entra en sobrecompra, lo que indica una tendencia fuerte; las largas se cancelan cuando el CCI gira a la baja y pierde el cero (p. 188).
- **Lado bajista (EA VII.3.1, pp. 190-191):** con tendencia bajista, la señal de venta llega cuando el CCI pierde −50 y entra en sobreventa (p. 190). Las posiciones cortas se cancelan cuando el CCI supera el cero (p. 191).

**Confirmación**

- **Más de un indicador (EA III.1.4, p. 80; EA VII.3.1, p. 192):** Cava pide que más de un indicador de momento confirme la señal. Si otros indicadores confirman la del CCI, la confianza en ella aumenta notablemente.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Período de %K | 14, sin suavizar | EA V.1.1, pp. 141-142 |
| Período de %D | 3, razón de sumas: 100·Σ3(C − Ln)/Σ3(Hn − Ln) | EA V.1.1, p. 143 |
| Mínimo del rango en %K | Ln, el menor mínimo de los n días, en el numerador | `[Elaboración]`: la fórmula impresa de %K usa el mínimo de hoy (EA V.1.1, p. 142), pero la definición de %D parte de (C − Ln) |
| Rango cero del estocástico | Arrastra el último valor válido (50 en la primera barra) | `[Propuesta]` |
| Niveles 80 y 20 | Sobrecompra y sobreventa | EA V.1.2, p. 143 |
| Niveles 60 y 40 | Filtro de tendencia con el estocástico semanal | EA I.5.3, p. 37 |
| Alertas del estocástico | %K cruza a la baja el 80 y al alza el 20 | `[Elaboración]`: la fuente describe las zonas (EA V.1.2, p. 143), pero no fija esos cruces como señal |
| Período del ADX y de los DI | 14, también para el suavizado del ADX | EA VIII.4.1, pp. 203-204; VIII.5.1, p. 207; VIII.6.4, p. 214 |
| Nivel 20 | Lectura baja y condición previa de la mejor señal | EA VIII.6.1, p. 208; VIII.6.2, p. 209 |
| Nivel 30 | Tendencia fortalecida | EA VIII.6.5, p. 215 |
| Mejor señal de compra | ADX bajo 20 y bajo los dos DI, giro al alza y cruce del -DI | EA VIII.6.2, pp. 209-210 |
| Mejor señal de venta | Lo mismo en sentido contrario: cruce del +DI | EA VIII.6.3, p. 212 |
| Regla de Elder | Subida de 4 a 12 puntos desde el mínimo, tras estar bajo los DI | EA VIII.6.3, p. 213 |
| Pendiente positiva o negativa | Comparación con la barra anterior | `[Propuesta]`: la fuente habla de pendiente sin medirla |
| Caducidad de la condición previa | 60 barras, ajustable | `[Propuesta]`: la fuente dice «cierto tiempo» sin cifra |
| Desarme por nivel 30 | Activado por defecto | `[Propuesta]` |
| Disparo único de cada marca | Una vez por armado | `[Propuesta]` |
| Período del CCI | 14 | EA VII.1, p. 186; VII.3.1, p. 187 |
| Precio del CCI | (máximo + mínimo + cierre) ÷ 3 | EA VII.1, p. 185 |
| Desviación del CCI | Media de las desviaciones absolutas respecto a la media simple | EA VII.1, p. 186 |
| Constante del CCI | 0,015 | `[Elaboración]`: es el valor habitual de Lambert. EA VII.1, pp. 185-186, imprime 0,15 en la fórmula y en el texto |
| Umbral de entrada del CCI | ±50, ajustable | EA VII.3.1, p. 187 |
| Nivel de cancelación del CCI | 0 | EA VII.3.1, p. 188 (largas) y p. 191 (cortas) |
| Filtro de tendencia del CCI | Ajuste manual: Alcista, Bajista o Ambas | `[Elaboración]`: la fuente condiciona las señales a la tendencia, pero no dice cómo se introduce |
| Cuenta de posiciones del CCI | Solo cancela lo que antes ha entrado y no repite la entrada | `[Elaboración]`: Cava presenta la cancelación como una secuencia, entrada y después pérdida del cero |
| Reescalado visual del CCI | 50 + 50 · CCI / escala, con escala 200 | `[Aportado]` en el código: transformación solo de dibujo, sin base en la fuente |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea azul gruesa (%K) | Posición del cierre en el rango de 14 barras | Sobre 80, sobrecompra; bajo 20, sobreventa (EA V.1.2, p. 143) |
| Línea naranja fina (%D) | Versión allanada de %K, por razón de sumas de 3 barras | Es la más significativa según la fuente (EA V.1.1, p. 142) |
| Línea verde gruesa (ADX) | Fuerza de la tendencia | Sobre 30, tendencia fortalecida; bajo 20, leve o lateral (EA VIII.6.5, p. 215; VIII.6.1, p. 208) |
| Líneas azul y roja semitransparentes (+DI y -DI) | Fuerza de los movimientos al alza y a la baja | La que queda por encima indica qué fuerzas controlan el precio (EA VIII.6.3, p. 212) |
| Triángulo verde hacia arriba, abajo del panel | Mejor señal de compra del ADX | Posible inicio de una tendencia alcista (EA VIII.6.2, pp. 209-210) |
| Triángulo rojo hacia abajo, arriba del panel | Mejor señal de venta del ADX | Posible inicio de una tendencia bajista (EA VIII.6.3, p. 212). La marca se rotula «VIII.6.2», pero la venta está en el apartado VIII.6.3 |
| Círculo naranja, abajo del panel | Giro de Elder | El ADX sube de 4 a 12 puntos desde su mínimo tras caer bajo los DI (EA VIII.6.3, p. 213) |
| Línea morada gruesa (CCI reescalado) | El CCI real dibujado como 50 + 50 · CCI / escala | Con la escala por defecto, +200 queda en 100, el 0 en 50 y −200 en 0. Su altura no es comparable con la de `JLC63 CCI` |
| Tres líneas moradas claras en escalón | +umbral, -umbral y cero del CCI, reescalados | Con los valores por defecto, 62,5, 37,5 y 50 |
| Triángulo morado hacia arriba, arriba del panel | Entrada larga del CCI | El CCI ha entrado en sobrecompra con la tendencia alcista: prueba de fuerza (EA VII.3.1, p. 188) |
| Aspa morada, arriba del panel | Cancela larga | El CCI pierde el 0 (EA VII.3.1, p. 188) |
| Triángulo morado hacia abajo, abajo del panel | Entrada corta del CCI | El CCI ha entrado en sobreventa con la tendencia bajista (EA VII.3.1, p. 190) |
| Aspa morada, abajo del panel | Cancela corta | El CCI supera el 0 (EA VII.3.1, p. 191) |
| Líneas grises en 80, 60, 40, 30 y 20 | Niveles fijos del panel | 80 y 20, del estocástico (EA V.1.2, p. 143); 60 y 40, del filtro semanal de tendencia (EA I.5.3, p. 37); 30, del ADX (EA VIII.6.5, p. 215). El 20 es también el nivel bajo el que el ADX marca tendencia leve y el 40, el nivel sobre el que la marca fuerte (EA VIII.6.1, p. 208) |

## Cómo funciona, paso a paso

**Estocástico**

1. Toma el máximo y el mínimo de las últimas n barras, con n = 14.
2. %K = 100 · (cierre − mínimo de n) / (máximo de n − mínimo de n). Con rango cero repite el último valor, o 50 en la primera barra. `[Propuesta]`
3. %D = 100 · suma de 3 de (cierre − mínimo de n) / suma de 3 de (máximo de n − mínimo de n). No es una media de %K.
4. Alertas: %K cruza a la baja el 80, o %K cruza al alza el 20. `[Elaboración]`

**ADX y DI**

1. Calcula +DI, -DI y ADX con la función estándar de TradingView, con el mismo período para los DI y para el suavizado del ADX.
2. «Sube» o «baja» significa mayor o menor que en la barra anterior. `[Propuesta]`
3. *Mejor señal.* Arma una condición previa cuando el ADX está por debajo de los dos DI y de 20. La descarta cuando pasan más barras que la caducidad (60 por defecto) o, con el ajuste activo, cuando el ADX supera 30 sin haber disparado; y la desarma también al disparar. Compra: condición armada, +DI sobre -DI, el ADX cruza al alza el -DI, el +DI sube y el -DI baja. Venta: lo simétrico, con el cruce del +DI. `[Propuesta]` en la caducidad, el desarme por 30 y el disparo único.
4. *Giro de Elder.* Arma una condición cuando el ADX está por debajo de los dos DI, sin exigir 20 y sin caducidad. Sigue el mínimo del ADX, que es el valor de la última barra en que el ADX bajó. Dispara cuando el ADX sube y la subida desde ese mínimo cruza los 4 puntos sin pasar de 12. Al disparar, se desarma. `[Elaboración]`

**CCI**

1. Precio = (máximo + mínimo + cierre) / 3. CCI = (precio − media simple de n) / (0,015 · desviación media de n), con n = 14. Con desviación cero repite el último valor, o 0 en la primera barra. `[Propuesta]`
2. Entrada larga: el CCI real cruza al alza el umbral, el ajuste de tendencia es Alcista o Ambas y no hay ya una larga abierta. Cancela larga: con una larga abierta, el CCI real cruza a la baja el 0. Entrada corta: el CCI real cruza a la baja el -umbral, el ajuste es Bajista o Ambas y no hay ya una corta abierta. Cancela corta: con una corta abierta, el CCI real cruza al alza el 0.
3. Las señales se calculan siempre sobre el CCI real. El dibujo usa el reescalado: 50 + 50 · CCI / escala.

**Barra en curso.** El código no espera al cierre de la barra: mientras se forma, las líneas y las marcas pueden cambiar, y quedan fijas al cerrar.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| %K sobre 80 con el ADX bajo 20 y bajo los dos DI | Sobrecompra en un mercado sin tendencia: la lectura tradicional resulta muy útil (EA V.1.2, p. 145; VIII.6.8, p. 220) | Que el giro esté garantizado: lo confirma el precio (EA V.1.3, p. 146) |
| %K sobre 80 con el ADX sobre 30 | Tendencia fuerte: el estocástico puede permanecer mucho tiempo en la zona (EA V.1.2, p. 143) | Una señal de venta |
| %K bajo 20 con el ADX bajo 20 y bajo los dos DI | Sobreventa en un mercado sin tendencia (EA V.1.2, p. 145; VIII.6.8, p. 220) | Una señal de compra por sí sola |
| Triángulo verde o rojo del ADX | La mejor señal de Cava: posible inicio de una tendencia (EA VIII.6.2, pp. 209-210; VIII.6.3, p. 212) | Una orden de entrada: conviene que otros indicadores la confirmen (EA III.1.4, p. 80) |
| Círculo naranja | El ADX ha subido de 4 a 12 puntos desde su mínimo tras caer bajo los DI (EA VIII.6.3, p. 213) | Una indicación de dirección: se mira el +DI frente al -DI |
| Triángulo morado hacia arriba con la tendencia alcista fijada | Señal de compra y de tendencia fuerte: el CCI ha entrado en sobrecompra (EA VII.3.1, p. 188) | Una señal de venta por sobrecompra: aquí es prueba de fuerza, la contraria de la lectura tradicional (EA VII.2, p. 187) |
| Aspa morada | Cancelación de la posición abierta del CCI: pierde el 0 la larga (EA VII.3.1, p. 188) o lo supera la corta (p. 191) | Que la tendencia haya terminado |
| Marcas del CCI con la tendencia en «Ambas» | Una señal del CCI sin filtro: el script no sabe si la tendencia la acompaña | Una señal válida para Cava: él condiciona siempre las señales al sentido de la tendencia (EA VII.3.1, pp. 187-188) |
| Varios osciladores en el mismo sentido | Más de un indicador de momento apunta igual (EA III.1.4, p. 80) | Un giro garantizado: lo confirma el precio (EA V.1.3, p. 146) |
| Línea del CCI cerca de 62,5 con los valores por defecto | El CCI real cerca de +50 | El nivel 60 del estocástico: quedan casi a la misma altura, pero son lecturas distintas |
| Línea de 40 | La del estocástico semanal en tendencia bajista (EA I.5.3, p. 37) y también el nivel sobre el que el ADX marca tendencia fuerte (EA VIII.6.1, p. 208) | Una sola lectura: la misma altura sirve a dos indicadores |

## Cuándo usarlo y cuándo no

- **Sí:** para ver en un solo panel si coinciden el ADX (régimen y mejores señales), el estocástico (posición en el rango) y el CCI (fuerza), con la tendencia dominante ya conocida. Con el ADX con pendiente positiva, sobre 30 y sobre los DI, hay un mercado con tendencia (EA VIII.6.6, p. 216); con el ADX bajo los dos DI, valen los niveles de sobrecompra y sobreventa (EA VIII.6.8, p. 220).
- **No:** para leer niveles precisos del CCI, porque el dibujo está reescalado (usar `JLC63 CCI`); con la tendencia sin fijar en el ajuste del CCI; como orden de entrada sin confirmación del precio (EA V.1.3, p. 146).
- **Mal uso frecuente** `[Elaboración]`: leer la altura del CCI como si fuera la del indicador individual; tomar la escala de 200 por una regla de Cava; confundir el umbral del CCI dibujado en 62,5 y 37,5 con las líneas de 60 y 40 del estocástico; leer la línea de 40 solo como nivel del estocástico cuando el ADX también lo usa.

## Qué NO dice

- No calcula la tendencia dominante: se fija a mano en el ajuste. La fuente la define con tres condiciones (EA I.5.3, p. 37); `JLC41 Trend light` la muestra.
- No dibuja marcas del estocástico: solo dos alertas, que siguen la línea %K, no %D, que la fuente considera la más significativa (EA V.1.1, p. 142).
- No tiene alertas para la entrada corta ni para la cancelación corta del CCI, aunque dibuja las cuatro marcas.
- No pinta los fondos de régimen del ADX, sobre 30 y sobre 40, que sí tiene `JLC51 ADX`.
- La duración de «cierto tiempo» bajo 20 no la cuantifica la fuente: el plazo de 60 barras y el desarme por nivel 30 son `[Propuesta]`.
- Reglas de la fuente que el script no implementa. `[Hueco declarado]`
  - Estocástico: cruce de %K sobre %D a la derecha del giro de %D (V.1.3, p. 146); divergencias, medidas sobre %D (V.1.4, pp. 147-149); bisagra (V.1.5, pp. 149-150); alarmas de Pring (V.1.6, p. 151); %K en un extremo, según Lane (V.1.7, p. 152); fallo (V.1.8, pp. 152-154); estocástico pop de Bernstein (V.1.9, pp. 154-158); combinación con el MACD mensual (V.2, desde la p. 158).
  - ADX: giro a la baja del ADX (VIII.6.8, pp. 219-220); divergencias con el ADX sobre 30 (VIII.6.5.1, pp. 215-216); retroceso a la media exponencial de 20 sesiones como entrada (VIII.6.6, p. 217).
  - CCI: interpretación tradicional, con compra al superar 0 tras la sobreventa y venta al perder 0 tras la sobrecompra (VII.2, p. 187); sobrecompra para cortas y sobreventa para largas en los movimientos correctivos (VII.3.1, pp. 188 y 191); divergencias (VII.3.2, pp. 192-194).

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-17 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.2.0. Citas contrastadas con EA (pp. 37, 80, 141-158, 185-194, 203-220) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
