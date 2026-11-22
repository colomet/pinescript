# [JLC12 Sentiment] Put/Call ratio + Bollinger bands · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (regla de Cava, *El arte de especular*, apartados II.2.4 y II.2.4.1; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja el ratio put/call de la CBOE (volumen de opciones de venta dividido entre el de opciones de compra) con bandas de Bollinger de 20 sesiones y desviación 2, para ver si el posicionamiento en opciones está en un extremo de miedo o de confianza. Se lee por opinión contraria: ratio alto, miedo y suelo probable; ratio bajo, confianza y techo probable. Es un indicador de sentimiento: se mira una vez al día.

## Qué dice la fuente

- **Qué mide (EA II.2.4, pp. 62-63):** la CBOE publica el volumen de opciones de compra y de venta y calcula el cociente entre ambos. Cava lo trata como indicador de opinión contraria, más fiable en valores extremos.
- **Lectura contraria (p. 63):** lecturas altas muestran excesivo sentimiento bajista y el suelo estaría próximo; lecturas bajas, excesivo sentimiento alcista y el techo estaría cerca.
- **Medias del ratio (p. 63):** se suele trabajar con una media de 10 o de 5 días del ratio global.
- **Rangos habituales (p. 63):** CBOE global, de 0,52 a 1,13; acciones (equity), de 0,35 a 0,75; OEX (S&P 100), de 0,77 a 1,55.
- **Niveles de giro del global (p. 63):** hacia 0,52, techo probable a corto plazo; hacia 1,13, suelo probable a corto plazo.
- **Regla de extremo (p. 64):** hay extremo de miedo cuando el ratio cierra por encima de la banda superior de Bollinger, con media de 20 sesiones y desviación 2.
- **Señal más significativa (p. 64):** si el ratio supera la banda superior y al día siguiente se coloca por debajo, Cava lo toma como un máximo de miedo. Pide mirar entonces el precio, por si hay una figura de agotamiento del movimiento bajista previo o un cruce violento de medias en un gráfico intradiario, y abrir en el sentido del giro con stop.
- **Extremo de miedo en mercado bajista (p. 64):** lo más probable es un rebote o un lateral. No es una gran señal de compra, pero tampoco el momento de abrir cortos.
- **Lado de la confianza (p. 65):** con tendencia bajista y subida del precio, si el ratio llega a la parte inferior de las bandas y gira al alza, cabe una posición corta si hay agotamiento del rebote o cruce de medias a la baja, siempre con stop.
- **Mejores señales (p. 65):** extremo de miedo con el precio en clara tendencia alcista, o confianza alta con el precio en clara tendencia bajista.
- **Preferencia de serie (p. 65):** las señales son más fiables en el ratio global y en el de índices, porque en el de acciones las cifras se distorsionan por operaciones casadas de grandes especuladores.
- **Media de 5 días (p. 65):** al llegar a 1, el mercado suele estar cerca de un suelo; cerca de 0,55, cerca de un techo.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Nivel de suelo | 1,13 | EA II.2.4.1, p. 63 |
| Nivel de techo | 0,52 | EA II.2.4.1, p. 63 |
| Período de Bollinger | 20 sesiones (ajustable) | EA II.2.4.1, p. 64 |
| Desviación de Bollinger | 2 (ajustable) | EA II.2.4.1, p. 64 |
| Suavizado | 10 sesiones (ajustable) | `[Aportado]`: Cava cita medias de 10 o 5 días (p. 63) pero no da regla con ellas |
| Cierre bajo la banda inferior | — | `[Elaboración]`: Cava describe esa zona (p. 65), no una regla de cierre |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Put/Call | Cierre del ratio (el símbolo se declara en los ajustes, no es el del gráfico) | Se lee frente a las bandas, no por su nivel |
| Suavizado `[Aportado]` | Media simple del ratio, 10 sesiones por defecto | Ayuda visual; la regla de extremo son las bandas |
| Bollinger superior e inferior | Media de 20 sesiones ± 2 desviaciones típicas | Ratio fuera de la banda: extremo |
| Bollinger base | Media de 20 sesiones | Referencia central |
| Líneas discontinuas en 1,13 y 0,52 | Niveles de giro del ratio global que da la fuente | Se leen junto a las bandas, no en su lugar |
| Punto rojo arriba | Primer cierre sobre la banda superior | Extremo de miedo: por opinión contraria, suelo probable a corto plazo |
| Punto verde abajo `[Elaboración]` | Primer cierre bajo la banda inferior | Extremo de confianza: techo probable a corto plazo |

## Cómo funciona, paso a paso

1. Toma el cierre del ratio desde el símbolo declarado en los ajustes. Si no carga, no hay error: el panel queda vacío.
2. Calcula la media simple y la desviación típica de 20 sesiones y construye las bandas: media ± 2 desviaciones.
3. Calcula el suavizado `[Aportado]` con el período de los ajustes.
4. Extremo de miedo: el ratio queda por encima de la banda superior. Extremo de confianza `[Elaboración]`: queda por debajo de la banda inferior.
5. Marca solo la primera barra de cada tramo fuera de banda.
6. Alertas: una por cada marca.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| Punto rojo (cierre sobre la banda superior) | Extremo de miedo; por opinión contraria, suelo probable a corto plazo (p. 64) | No es orden de compra: la fuente pide mirar el precio y poner stop |
| Cierre sobre la banda y regreso bajo ella al día siguiente | Máximo de miedo: señal significativa (p. 64) | El script no lo marca |
| Punto verde (cierre bajo la banda inferior) | Confianza alta; techo probable `[Elaboración]` | No es regla de la fuente: Cava describe la zona sin regla de cierre |
| Ratio cerca de 1,13 o de 0,52 | Suelo o techo probable a corto plazo (p. 63) | Los niveles son rangos habituales de su época, no fijos |
| Media de 5 días en 1 o cerca de 0,55 | Suelo o techo probable (p. 65) | El script no lo implementa |

## Cuándo usarlo y cuándo no

- **Sí:** como contexto diario del mercado americano, junto con JLC11. Cava lo plantea sobre el S&P 500 (p. 63).
- **No:** como orden de compra o venta directa. Es una lectura contraria: el libro pide confirmar con el precio y poner stop.
- **Mal uso frecuente:** tratar 0,52 y 1,13 como niveles fijos `[Elaboración]`: son los rangos habituales que da el libro, y las bandas son relativas.

## Qué NO dice

- No dice qué comprar ni cuándo entrar.
- No marca el máximo de miedo (cierre sobre la banda y regreso bajo ella al día siguiente), que Cava considera la señal significativa. `[Hueco declarado]`
- No comprueba la tendencia del precio ni las pautas de agotamiento o los cruces de medias que la fuente pide mirar (pp. 64-65). `[Hueco declarado]`
- No implementa la media de 5 días con sus niveles 1 y 0,55 (p. 65) ni el ratio de índices. `[Hueco declarado]`
- No es confirmación fuerte de JLC11: ambos miden miedo por vías distintas; si coinciden en el extremo, el aviso gana peso. `[Elaboración]`

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Contrastada con EA II.2.4 y II.2.4.1 (pp. 62-65). Corregido: la regla de Bollinger está en la p. 64; el libro sí cita medias de 10 o 5 días y sí describe el lado de la confianza |
| 0.3.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 1.0.0.0. El lado de la confianza pasa a la p. 65 |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script |
