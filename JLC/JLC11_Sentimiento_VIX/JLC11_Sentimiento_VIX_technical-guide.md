# [JLC11 Sentiment] VIX vs SMA10 + bands · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (regla de Cava, *El arte de especular*, apartado II.2.3; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Compara el VIX con su media simple de 10 sesiones y dibuja bandas porcentuales alrededor de ella. Mide miedo o complacencia del mercado americano respecto a lo reciente, no respecto a un nivel absoluto. Es un indicador de sentimiento: se mira una vez al día, antes de mirar activos.

## Qué dice la fuente

Cava usa el VIX de forma dinámica: compara su nivel con la media simple de las diez últimas sesiones y presta poca atención al valor absoluto (EA II.2.3.2, pp. 60-61). La volatilidad suele moverse en sentido contrario al precio (nota 32, p. 61).

- **Condición de tendencia (p. 61):** las posiciones deben ir siempre en sintonía con la tendencia dominante del precio.
- **VIX un 5 % o más por debajo de su media (p. 61):** con tendencia alcista, el mercado está parado y Cava no abriría compras. Con tendencia bajista, la caída de la volatilidad bajo la media indica la proximidad de una zona de sobrecompra, adecuada para vender cerca de una resistencia. Nota 33 (p. 61): entre 1989 y 2005 el S&P 500 bajó en los cinco días siguientes a aquel en que el VIX estuvo al menos un 5 % por debajo de su media de 10 sesiones.
- **VIX un 5 % o más por encima de su media, mejor un 10 % o un 12 % (p. 61):** momento a vigilar para abrir largos, con los indicadores de momento en sobreventa. Nota 35 (p. 61): entre 1989 y 2005, con el VIX al menos un 5 % por encima, el S&P 500 se comportó en los cinco días siguientes de forma más alcista que su media semanal.
- **Sistema de compra (p. 62):** señal de compra cuando el VIX cierra por encima de su media de 10 sesiones incrementada un 12 %; los largos se cancelan cinco días después. Lo describe como un sistema muy usado por quienes operan el futuro del S&P 500. Entre 1991 y octubre de 2005 dio beneficios en el 60 % de las señales y las ganancias duplicaron a las pérdidas. Es un dato del propio autor, no una validación independiente.
- **Alcance (p. 61):** Cava dice que el sistema funcionó muy bien de octubre de 2002 a mediados de enero de 2006, con las bolsas en fuerte tendencia alcista, y que no es perfecto.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Banda de señal de compra | +12 % | EA II.2.3.2, p. 62 |
| Banda de sesgo alcista | +5 % | EA nota 35, p. 61 |
| Banda de sesgo bajista | −5 % | EA nota 33, p. 61; la etiqueta «sesgo bajista» es `[Elaboración]` |
| Sesiones hasta la cancelación | 5 | EA II.2.3.2, p. 62 |
| Período de la media | 10 sesiones (ajustable) | EA II.2.3.2, p. 61 |
| VIX3M y backwardation | — | `[Aportado]`: no proceden de Cava |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| VIX | Cierre del VIX (el símbolo se declara en los ajustes, no es el del gráfico) | Su nivel absoluto importa poco: se lee frente a la media y las bandas |
| SMA10 VIX | Media simple del VIX, 10 sesiones | Referencia contra la que se mide el VIX |
| Banda +12 % | Media × 1,12 | Si el VIX la cruza al alza, señal de compra del sistema |
| Banda +5 % | Media × 1,05 | VIX por encima: sesgo alcista a 5 sesiones |
| Banda −5 % | Media × 0,95 | VIX por debajo: sesgo bajista a 5 sesiones `[Elaboración]`; léelo junto a la tendencia |
| VIX3M `[Aportado]` | Cierre del VIX a tres meses | Referencia para la estructura de plazo |
| Triángulo verde | El VIX cruza al alza la banda +12 % | Señal de compra del sistema |
| Cruz gris | Quinta sesión tras la señal | Momento en que el sistema cancela los largos |
| Fondo naranja `[Aportado]` | VIX por encima del VIX3M (backwardation) | Estrés inmediato en la estructura de plazo: contexto, no señal |

## Cómo funciona, paso a paso

1. Toma el cierre del VIX y, si está activo, el del VIX3M, desde los símbolos declarados en los ajustes. Si un símbolo no carga, no hay error: la línea queda vacía.
2. Calcula la media simple del VIX con el período de los ajustes (10 por defecto).
3. Calcula las tres bandas multiplicando la media por 1,12, 1,05 y 0,95.
4. Señal de compra: el VIX cruza por encima de la banda +12 %. Si ya estaba por encima en la barra anterior, no hay señal nueva: se marca solo el cruce.
5. Cancelación: cinco barras después de la última señal se marca la cruz. Si llega otra señal antes, la cuenta empieza de nuevo.
6. Backwardation `[Aportado]`: el VIX es mayor que el VIX3M, con el VIX3M activo.
7. Alertas: señal de compra, cruce a la baja de la banda −5 % y entrada en backwardation.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| El VIX cruza la banda +12 % | Señal de compra del sistema de la fuente; los largos se cancelan 5 sesiones después | No es una orden: la fuente pide además estar en sintonía con la tendencia y el script no lo comprueba |
| VIX más de un 5 % sobre la media | Sesgo alcista a 5 sesiones (nota 35) | No es señal por sí solo |
| VIX dentro de ±5 % de la media | Sin lectura en la fuente | No es neutralidad confirmada |
| VIX más de un 5 % bajo la media | Con tendencia alcista, mercado parado y sin compras; con tendencia bajista, zona de sobrecompra (p. 61). Nota 33: el S&P 500 bajó en los 5 días siguientes | No es señal de venta por sí solo: el script no distingue la tendencia |
| VIX por encima del VIX3M | Estrés inmediato en el plazo corto `[Aportado]` | No aparece en Cava; contexto, no señal |

La etiqueta «sesgo bajista» para la banda −5 % la pone el script a partir de la nota 33. Cava no la usa como señal de venta aislada: la lee junto a la tendencia.

## Cuándo usarlo y cuándo no

- **Sí:** una vez al día, sobre el mercado americano, antes de mirar activos. Gráfico diario, que es el marco de la fuente.
- **No:** como disparador de entrada en un activo concreto: el sistema está descrito para el futuro del S&P 500 (p. 62).
- **Mal uso frecuente:** leer niveles absolutos («el VIX está en 20, es alto»); aplicarlo a un activo individual; tratar la banda −5 % como venta sin mirar la tendencia.

## Qué NO dice

- No dice qué comprar ni cuándo entrar en nada concreto.
- No comprueba la tendencia del precio, que la fuente exige (p. 61). `[Hueco declarado]`
- No implementa la relación precio/volatilidad (EA II.2.3.1.1, pp. 58-59), ni el VXN del NASDAQ 100, ni el stop por volatilidad de 3 puntos (p. 62). `[Hueco declarado]`
- No es confirmación fuerte del ratio put/call (JLC12): ambos miden miedo por vías distintas; si coinciden en el extremo, el aviso gana peso. `[Elaboración]`

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Contrastada con EA II.2.3 (pp. 52-62): citas por página; VIX3M y backwardation marcados como añadido |
| 0.3.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 1.2.0.0. Corregidas páginas (tendencia y media de 10 sesiones, p. 61) y la lectura del −5 %, que con tendencia bajista indica sobrecompra |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script |
