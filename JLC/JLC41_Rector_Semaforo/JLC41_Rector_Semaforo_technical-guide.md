# [JLC41 Trend] Traffic light: monthly MACD + weekly MACD + weekly stochastic {60/40} · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (definición de tendencia de Cava en *El arte de especular*, apartado I.5.3; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Semáforo de tendencia: comprueba a la vez las tres condiciones con las que Cava define la tendencia (MACD mensual, MACD semanal y estocástico semanal) y muestra uno de tres estados: ALCISTA, BAJISTA o INDEFINIDO. Se aplica sobre el gráfico diario del activo que se evalúa y lee por su cuenta los marcos semanal y mensual. Es el punto de partida de la sesión: fija el sentido de la tendencia en el que luego se leen las señales de los demás indicadores.

## Qué dice la fuente

- **Definición de tendencia (EA I.5.3, p. 37):** es alcista cuando el MACD mensual está cortado al alza, la línea rápida del MACD semanal está por encima de cero y la línea rápida del estocástico semanal está por encima de 60. Es bajista cuando el MACD mensual está cortado a la baja, la línea rápida del MACD semanal está por debajo de cero y la del estocástico semanal, por debajo de 40.
- **Ejemplo de la fuente (EA I.5.3, pp. 37-38):** en el IBEX 35 semanal el MACD semanal estuvo bajo cero desde finales de mayo de 2000 hasta comienzos de marzo de 2003 (tendencia bajista) y sobre cero desde entonces, con una señal falsa en abril de 2004.
- **MACD (EA IV.1, p. 101):** la línea rápida es la diferencia entre dos medias exponenciales, que suelen ser de 12 y 26 periodos; la lenta es una media exponencial de 9 periodos de la rápida.
- **Nivel cero (EA IV.2.1, p. 102):** cuando la línea rápida del MACD supera el nivel cero se considera señal de inicio de una tendencia alcista, y cuando lo pierde, de una bajista; la señal es muy significativa en gráficos semanales o mensuales. Combinada con el cruce de las dos líneas del MACD mensual, es aún más fiable.
- **Cruce mensual (EA IV.2.2.1, pp. 103-104):** el cruce de las dos líneas de un MACD mensual es una señal muy fiable por sí misma y más significativa que la de un gráfico semanal. El cruce al alza marca el inicio de una tendencia alcista y el cruce a la baja, el de una bajista, esté el MACD sobre o bajo cero. En el IBEX 35, el cruce al alza del MACD mensual de abril de 2003 coincidió con que el MACD semanal superó el cero.
- **Estocástico (EA V.1.1, pp. 141-143):** se dibuja con dos líneas, %K y %D. La %K es la más sensible y por eso la más rápida; la %D es la lenta y una versión allanada de la %K. Se suele trabajar con un intervalo de 14 periodos y se aplica también a gráficos semanales y mensuales.
- **Marcos y coincidencia (EA III.1.4, p. 80; III.1.1, p. 71):** cuanto mayor es el intervalo temporal del gráfico, más significativa es la señal del indicador, y para confirmar un cambio de tendencia debe coincidir más de un indicador de momento: uno solo no basta. La perspectiva de tendencia intermedia, entre 6 y 40 semanas, se obtiene con indicadores de periodo mensual y semanal.
- **Señales subordinadas a la tendencia (EA VII.3.1, pp. 187-188):** las señales de los sistemas están siempre condicionadas al sentido de la tendencia: si es alcista se siguen las de compra y si es bajista, las de venta. El semáforo calcula ese sentido para que los demás indicadores no tengan que suponerlo.
- **Jerarquía de marcos (EA I.4, p. 29, según la cabecera del script):** mensual para el cambio de tendencia, semanal para la dirección dominante y diario para el momento de entrada. Por eso los marcos del semáforo son mensual y semanal, fijos.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| MACD | 12 / 26 / 9 | EA IV.1, p. 101 |
| Marcos | Mensual y semanal, fijos | EA I.5.3, p. 37 |
| Umbral alcista del estocástico semanal | 60 | EA I.5.3, p. 37 |
| Umbral bajista del estocástico semanal | 40 | EA I.5.3, p. 37 |
| Nivel del MACD semanal | 0 | EA I.5.3, p. 37 |
| Estocástico %K | 14 barras semanales, sin suavizar | EA V.1.1, p. 141: 14 periodos habituales y la %K es la línea rápida |
| Condiciones que deben coincidir | Las tres | EA I.5.3, p. 37 |
| «Cortado al alza» | Línea rápida del MACD mensual por encima de su línea de señal, como estado | `[Elaboración]`: la fuente dice que el MACD esté cortado al alza; el script lo traduce a un estado medible |
| INDEFINIDO | Las tres condiciones no concuerdan | `[Elaboración]`: la fuente no define tendencia en ese caso y el script no la inventa |
| Recuento n↑ / n↓ | Cuántas de las tres condiciones apuntan a cada lado | `[Propuesta]`: solo informativo |
| Lectura de barras cerradas (por defecto) | Última barra semanal y mensual cerrada | `[Propuesta]`: evita que el estado cambie después; la fuente no lo trata |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Fondo verde tenue | Estado ALCISTA | Las tres condiciones apuntan al alza |
| Fondo rojo tenue | Estado BAJISTA | Las tres condiciones apuntan a la baja |
| Fondo sin color | Estado INDEFINIDO, o fondo desactivado | Las tres condiciones no concuerdan: la fuente no define tendencia |
| Tabla, fila «TENDENCIA» | Estado y recuento n↑ / n↓ | Manda el estado; el recuento es informativo `[Propuesta]` |
| Tabla, fila «MACD mensual» | «cortado al alza» o «cortado a la baja» | Condición 1: la línea rápida del MACD mensual, sobre o bajo su señal |
| Tabla, fila «MACD semanal» | Valor del MACD semanal con «(>0)» o «(<0)» | Condición 2: la línea rápida del MACD semanal, sobre o bajo cero |
| Tabla, fila «Estocástico %K sem.» | Valor con «(>60)», «(<40)» o «(40-60)» | Condición 3: entre 40 y 60 no cuenta a ningún lado |
| Tabla, última fila | «Barras cerradas» o «Barra en curso» y la referencia de la fuente | Dice qué barras lee el script |

## Cómo funciona, paso a paso

1. **Datos.** Pide al propio símbolo el MACD mensual, el MACD semanal y el %K semanal. No usa datos que aún no existen.
2. **Barras cerradas.** Con la opción activada (por defecto) todo se desplaza una barra y se usa la última barra semanal o mensual ya cerrada. Desactivada, se usa la barra en curso.
3. **MACD.** Línea rápida = media exponencial rápida menos media exponencial lenta (12 y 26); línea de señal = media exponencial de 9 de la línea rápida. Los mismos periodos para el mensual y el semanal.
4. **Estocástico %K semanal.** 100 × (cierre − mínimo de los mínimos de las últimas 14 barras semanales) ÷ (máximo de los máximos − mínimo de los mínimos de esas barras). Si el rango es cero, arrastra el último valor válido y, si no hay ninguno, vale 50. Sin suavizar: es la línea rápida. La fórmula impresa en EA V.1.1, p. 142, pone en el numerador el mínimo del día; el script usa el mínimo de las n barras, que es la definición habitual y la que la fuente usa en su fórmula de la %D (p. 143). `[Elaboración]`
5. **Condiciones.** Alcistas: MACD mensual sobre su señal, MACD semanal sobre cero y %K semanal sobre 60. Bajistas: MACD mensual bajo su señal, MACD semanal bajo cero y %K semanal bajo 40.
6. **Estado.** ALCISTA si se cumplen las tres alcistas; BAJISTA si se cumplen las tres bajistas; INDEFINIDO en cualquier otro caso.
7. **Recuento.** Cuántas condiciones apuntan al alza y cuántas a la baja. `[Propuesta]`
8. **Alertas.** Saltan cuando el estado de la barra difiere del de la anterior y es el indicado.
9. **Repintado.** Con barras cerradas, el estado solo cambia en la primera barra de una semana o de un mes nuevos y no se corrige después. Sin ellas, la barra en curso puede cambiar hasta su cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| ALCISTA (3↑ / 0↓) | Las tres condiciones de Cava coinciden al alza: la tendencia dominante es alcista (EA I.5.3, p. 37) | No es una señal de compra: fija el sentido en el que se siguen las señales de compra de los demás indicadores (EA VII.3.1, pp. 187-188) |
| BAJISTA (0↑ / 3↓) | Las tres condiciones coinciden a la baja: la tendencia dominante es bajista | No es una orden de venta: fija el sentido en el que se siguen las señales de venta |
| INDEFINIDO | Las tres condiciones no concuerdan: Cava no define tendencia en ese caso `[Elaboración]` | No es un fallo del script ni falta de datos; tampoco dice que el mercado esté lateral |
| Dos condiciones en un sentido y la tercera sin cumplirse | Falta una condición: el estado es INDEFINIDO | No es una tendencia a medias: la fuente exige las tres `[Elaboración]` |
| Paso de ALCISTA a INDEFINIDO | Una de las tres condiciones ha dejado de cumplirse | No anuncia por sí solo una tendencia bajista: para eso deben cumplirse las tres bajistas |
| El estado cambia en la primera barra de una semana o de un mes | Con barras cerradas, el estado refleja la última barra completa | No es un retraso del script: es lo que evita que el estado se corrija después |

## Cuándo usarlo y cuándo no

- **Sí:** como primer paso de la sesión, sobre el gráfico diario del activo evaluado, antes de leer las señales de los demás indicadores. El sentido que muestra es el que se fija en el ajuste «Tendencia dominante» del indicador de CCI de este repositorio (JLC63).
- **No:** como señal de entrada o de salida, ni como sustituto de los demás indicadores: Cava pide que coincidan varios (EA III.1.4, p. 80).
- **Mal uso frecuente:** leer el estado como orden de compra o de venta; forzar un sentido cuando marca INDEFINIDO; registrar el estado con las barras cerradas desactivadas, porque la barra en curso puede cambiar; fiarse del estado en valores con poco histórico mensual, donde el MACD mensual tarda en estabilizarse `[Elaboración]`.

## Qué NO dice

- No dice cuándo entrar ni cuándo salir.
- No mide la fortaleza de la tendencia, solo su sentido: Cava pide situar las señales en el marco de la tendencia dominante y de su fortaleza (EA IV.2.2, p. 103). `[Hueco declarado]`
- No incluye otros criterios de tendencia de la misma fuente, como las medias móviles desplazadas que Cava expone justo antes (EA, pp. 36-37). `[Hueco declarado]`

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 37-38, 71, 80, 101-104, 141-143, 187-188) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
