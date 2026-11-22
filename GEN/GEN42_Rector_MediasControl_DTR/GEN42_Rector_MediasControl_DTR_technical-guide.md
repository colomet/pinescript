# [GEN42 Rector] Control SMAs: 6/70/200 (Trullas) · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Agrupación y períodos de David Trullás, citados por cortesía; el código es propio. Los períodos 6, 70 y 200 son `[Aportado]` |
| Script | Versión 0.1.0.0 (ver control de cambios) |

---

## Qué es

Tres medias móviles simples del precio elegido en el ajuste «Fuente» (por defecto, el cierre), dibujadas sobre las velas: rápida (6), intermedia (70) y lenta (200). Es una agrupación: reúne en un solo indicador tres medias estándar para no cargar tres. Por su título es de la categoría Rector, la de la tendencia. No emite señales ni alertas.

## Qué dice la fuente

La fuente es el indicador de David Trullás «Medias Móviles de Control (SMA 6, 70, 200)». El código de ese indicador trae un comentario con el propósito y los componentes `[Aportado]`:

- **SMA 6, rápida:** captura la inercia y los giros de muy corto plazo.
- **SMA 70, media:** sirve de referencia para la tendencia intermedia de la sesión.
- **SMA 200, lenta:** delimita la tendencia estructural o de largo plazo.

El cálculo es la media aritmética de las últimas N velas, el estándar de Pine. Según la cabecera del script, ninguna fuente fija los períodos 6, 70 y 200: son los del autor `[Aportado]`.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Períodos | 6, 70 y 200 velas | `[Aportado]`: los del autor; ninguna fuente los fija |
| Cálculo | Media aritmética simple de N velas | Estándar de Pine |
| Precio | El cierre por defecto, elegible en «Fuente» | Del script |
| Límite de los períodos | De 1 a 1000 velas | Del script |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea azul (SMA rápida) | Media simple de 6 velas | Inercia y giros de muy corto plazo `[Aportado]` |
| Línea naranja (SMA intermedia) | Media simple de 70 velas | Referencia de la tendencia intermedia `[Aportado]` |
| Línea roja (SMA lenta) | Media simple de 200 velas | Tendencia estructural, de largo plazo `[Aportado]` |

## Cómo funciona, paso a paso

1. Toma el precio elegido en «Fuente» (por defecto, el cierre).
2. Calcula con cada período la media simple de ese precio: la suma de las últimas N velas dividida entre N.
3. Dibuja las tres líneas, cada una con su color y su grosor.
4. No compara las líneas entre sí ni el precio con ellas, y no emite señales ni alertas.

Cada media aparece cuando hay N velas cargadas: antes de eso no tiene valor.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| El precio cruza la línea azul | Un giro de muy corto plazo, según el autor `[Aportado]` | Un cambio de tendencia: la media de 6 velas sigue de cerca al precio `[Elaboración]` |
| El precio frente a la línea naranja | La referencia de la tendencia intermedia, según el autor `[Aportado]` | Una señal de compra o de venta: el script no las emite |
| El precio frente a la línea roja | La referencia de la tendencia estructural, de largo plazo, según el autor `[Aportado]` | Una señal: el script no compara el precio con la media ni avisa |
| Una línea no aparece | Hay menos velas cargadas que el período de esa media | Un fallo del script: la media de N velas no tiene valor hasta reunir N velas |
| Se cambia el ajuste «Fuente» | Las tres líneas se recalculan con ese precio | Un cambio de períodos |

## Cuándo usarlo y cuándo no

- **Sí:** para tener en un solo indicador las tres medias de Trullás, con sus períodos, sus colores y su grosor ajustables, sin cargar tres indicadores.
- **No:** como fuente de entradas y salidas, porque no las da; tampoco para medir la fuerza de la tendencia.
- **Mal uso frecuente** `[Elaboración]`: tomar los períodos 6, 70 y 200 por cifras de Cava, cuando son de Trullás; leer el cruce de dos de las medias como una señal del script, que no las compara.

## Qué NO dice

- No da entradas ni salidas.
- No mide la fuerza de la tendencia.
- No compara las líneas entre sí ni el precio con ellas.
- No define alertas.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-14 | Primer borrador |
| 0.2.0.0 | 2026-11-14 | Renombrada a GEN42 |
| 0.3.0.0 | 2026-11-14 | Descrita como agrupación de tres SMA |
| 0.3.1.0 | 2026-11-15 | «Del cierre» pasa a «de la fuente elegida (por defecto, el cierre)», según el código |
| 0.4.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.0.0. Cifras y descripción de las líneas contrastadas con el código original de Trullás |
