# [JLC62 Diagnostic] Stochastic: 14 {80/60/40/20} · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (estocástico de Lane según Cava, capítulo V de *El arte de especular*; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja en un panel el estocástico tal como lo describe Cava: la línea %K sin suavizar, la línea %D calculada como razón de sumas de 3 periodos, los niveles 80 y 20 (sobrecompra y sobreventa) y los niveles 60 y 40 (filtro de tendencia con el gráfico semanal). Mide dónde cierra el precio dentro del rango de las últimas 14 barras: cerca de 100 si cierra cerca del máximo del rango y cerca de 0 si cierra cerca del mínimo. Es un diagnóstico: solo dibuja, no marca señales ni genera alertas. Se aplica sobre el gráfico del valor, en el marco que se evalúa.

## Qué dice la fuente

- **Concepto (EA V.1.1, p. 141):** mide la posición relativa del cierre dentro del rango de un intervalo, que suele ser de 14 días. Parte de que, en una tendencia alcista, los cierres tienden a quedar cerca de la parte alta del rango y, en una bajista, cerca de los mínimos. Por eso detecta cuándo, en un mercado alcista, los cierres se agrupan más cerca de los mínimos que de los máximos, lo que suele anticipar un techo (y a la inversa en un mercado bajista). Se aplica sobre todo a gráficos diarios, pero sirve también en intradiarios, semanales y mensuales.
- **Las dos líneas (EA V.1.1, pp. 141-142):** %K es la línea continua, la más sensible y rápida; %D es la discontinua, la más lenta (p. 141). %K es la más sensible de las dos, pero %D es la más significativa y la que da las principales señales (p. 142).
- **Fórmula de %K (EA V.1.1, p. 142):** %K = 100·(C − L)/(Hn − Ln), donde C es el cierre de hoy, L el mínimo de hoy, Ln el menor de los mínimos de los últimos n días y Hn el mayor de los máximos de esos n días. Lane recomendó n = 3 para el corto plazo y se hizo más popular 5; Hartle, en 1991, usa 14.
- **Fórmula de %D (EA V.1.1, p. 143):** %D = 100·(H3/L3), donde H3 es la suma de 3 periodos de (C − Ln) en el cálculo de %K y L3 la suma de 3 periodos de (Hn − Ln). Es una versión allanada de %K, y la fuente deja experimentar con otros periodos.
- **Niveles 80 y 20 (EA V.1.2, p. 143):** el indicador se mueve siempre entre 0 y 100. Lecturas cerca de 80 son sobrecompra y cerca de 20, sobreventa. La interpretación más sencilla y tradicional es que, al llegar a 80 o más, el precio está a punto de girarse a la baja, y que al caer por debajo de 20 se anticipa un suelo.
- **Matiz sobre los niveles (EA V.1.2, pp. 143-145):** llegar a sobrecompra o sobreventa no indica necesariamente un giro inmediato. Con una tendencia fuerte (ADX girado al alza, onda 3 de una pauta de impulso u onda C de una pauta plana), el estocástico permanece mucho tiempo en la zona, precisamente porque la tendencia es fuerte (p. 143). Ejemplo: el estocástico de 14 semanal del Index Dólar estuvo por debajo de 20 más de tres meses mientras caía (p. 144). La lectura tradicional sí es muy útil con un movimiento lateral o una tendencia escasa (p. 145).
- **Filtro de tendencia (EA I.5.3, p. 37):** la tendencia es alcista cuando, además de las condiciones del MACD, la línea rápida del estocástico semanal está por encima de 60, y bajista cuando está por debajo de 40.
- **Las señales hay que confirmarlas (EA V.1.3, p. 146):** las señales de los indicadores de momento son alarmas que deben confirmarse con el movimiento del precio.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Periodo de %K | 14, sin suavizar | EA V.1.1, pp. 141-142 (14 días habituales; Hartle, 1991) |
| Periodo de %D | 3 | EA V.1.1, p. 143 |
| %D como razón de sumas | 100·Σ3(C − Ln)/Σ3(Hn − Ln), no la media simple de %K | EA V.1.1, p. 143 |
| Niveles 80 y 20 | Sobrecompra y sobreventa | EA V.1.2, p. 143 |
| Niveles 60 y 40 | Filtro de tendencia con %K semanal | EA I.5.3, p. 37 |
| Mínimo del rango en %K | Ln, el menor mínimo de los n días, en el numerador | `[Elaboración]`: la fórmula impresa de %K usa el mínimo de hoy (EA V.1.1, p. 142), pero la definición de %D de la misma fuente parte de (C − Ln) |
| Rango cero | Si el máximo y el mínimo del periodo coinciden, arrastra el último valor válido (50 en la primera barra) | `[Propuesta]` |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| %K (azul, grosor 2) | Línea rápida, sin suavizar | La más sensible: reacciona a cada barra |
| %D (naranja, grosor 1) | Línea lenta: razón de sumas de 3 periodos | La que la fuente considera más significativa (EA V.1.1, p. 142) |
| Nivel 80 (continua) | Sobrecompra | Cerca o por encima, el cierre está en la parte alta del rango |
| Nivel 20 (continua) | Sobreventa | Cerca o por debajo, el cierre está en la parte baja del rango |
| Niveles 60 y 40 (discontinuas) | Filtro de tendencia con %K semanal | Sobre 60 apoya tendencia alcista; bajo 40, bajista |
| Banda gris tenue, de 20 a 80 | Relleno | Zona entre sobreventa y sobrecompra |

## Cómo funciona, paso a paso

1. **Rango.** Para cada barra toma el mayor máximo y el menor mínimo de las últimas n barras (14 por defecto).
2. **%K.** 100 × (cierre − mínimo del rango) ÷ (máximo del rango − mínimo del rango). Va sin suavizar, a diferencia del estocástico «lento». Si el rango es cero, arrastra el último valor válido y, si no hay ninguno, vale 50. `[Propuesta]`
3. **%D.** 100 × (suma de los últimos 3 valores de «cierre − mínimo del rango») ÷ (suma de los últimos 3 valores de «máximo − mínimo del rango»). Es una razón de sumas, no la media simple de %K. Misma guarda ante rango cero. `[Propuesta]`
4. **Dibujo.** %K, %D, los cuatro niveles y la banda entre 20 y 80.
5. **Barra en curso.** El código no espera al cierre de la barra: las líneas se mueven mientras se forma y quedan fijas al cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| %K sobre 80 | Sobrecompra: el cierre está en la parte alta del rango (EA V.1.2, p. 143) | Una señal de venta por sí sola: con tendencia fuerte puede quedarse ahí mucho tiempo (EA V.1.2, p. 143) |
| %K bajo 20 | Sobreventa: el cierre está en la parte baja del rango (EA V.1.2, p. 143) | Una señal de compra por sí sola, por la misma razón (EA V.1.2, p. 144) |
| Sobrecompra o sobreventa con tendencia escasa o lateral | La lectura tradicional resulta muy útil: zona de posible techo o suelo (EA V.1.2, p. 145) | Que el giro esté garantizado: debe confirmarlo el precio (EA V.1.3, p. 146) |
| %K semanal sobre 60 | Cumple la condición del estocástico para tendencia alcista (EA I.5.3, p. 37) | Una tendencia alcista completa: la definición de Cava exige además el MACD mensual y el semanal (EA I.5.3, p. 37) |
| %K semanal bajo 40 | Cumple la condición del estocástico para tendencia bajista (EA I.5.3, p. 37) | Una tendencia bajista completa, por la misma razón |
| %K semanal entre 40 y 60 | No cumple ninguna de las dos condiciones de la fuente (EA I.5.3, p. 37) | Una señal contraria |
| %K cruza %D | Las dos líneas se cortan; Lane considera más fiable el cruce de %K sobre %D cuando %D ya se ha girado (EA V.1.3, p. 146) | Una señal por sí sola: el script no marca los cruces |

## Cuándo usarlo y cuándo no

- **Sí:** como diagnóstico del tramo, con el ADX a la vista, para saber si el precio se agota o tiene fuerza; y con el gráfico semanal, para la condición del estocástico en la definición de tendencia de Cava.
- **No:** solo, para decidir una entrada; como señal de giro cuando la tendencia es fuerte (EA V.1.2, p. 143); con los niveles 60 y 40 como filtro de tendencia fuera del marco semanal.
- **Mal uso frecuente** `[Elaboración]`: vender porque marca 85 sin mirar el ADX; suavizar %K, que deja de ser la línea rápida; leer divergencias sobre %K cuando la fuente las mide sobre %D (EA V.1.4, p. 147); mezclar los dos juegos de niveles entre marcos.

## Qué NO dice

- No dibuja señales ni genera alertas: son dos líneas y cuatro niveles.
- No dice si el mercado va a girar: dice si el tramo gana o pierde fuerza, y el giro lo confirma el precio (EA V.1.3, p. 146).
- Figuras de la fuente que el script no implementa. `[Hueco declarado]`
  - Cruce de %K sobre %D a la derecha del giro de %D, más fiable según Lane (V.1.3, p. 146).
  - Divergencias, medidas sobre la línea %D (V.1.4, pp. 147-149).
  - Bisagra: caída significativa de la pendiente de %K, que anuncia pérdida de ímpetu y giro. Cava aconseja bajar a un gráfico horario y buscar una figura de agotamiento antes de darla por buena (V.1.5, pp. 149-150).
  - Alarmas de Pring: si %K, que subía con la tendencia, se gira bruscamente a la baja, tras uno o dos periodos más de subida es probable un techo (V.1.6, p. 151).
  - %K en un extremo, según Lane: tras tocar 0 suele rebotar hasta la zona de 20-25 % y volver a 0, con un rebote de 2 a 4 días en diario; una lectura de 100 revela fortaleza de la tendencia (V.1.7, p. 152).
  - Fallo (V.1.8, pp. 152-154).
  - Estocástico pop de Bernstein (V.1.9, pp. 154-158).
  - Combinación con el MACD mensual (V.2, desde la p. 158).

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 37, 141-159) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
