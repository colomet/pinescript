# [GEN44 Trend] EMA 50 + smoothing · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Indicador integrado «Moving Average Exponential» de TradingView, con la longitud por defecto cambiada a 50. No es autoría propia ni de Cava. El periodo 50 es `[Aportado]` y no tiene fuente confirmada |
| Script | Versión 0.1.1.0, estable (archivo `GEN44_Rector_EMA50.pine`) |
| Probada en TradingView | Sí (Antonio, 22/11/2026) |
| Validada en conector | No (límite de cuota diaria) |

---

## Qué es

La media móvil exponencial (EMA) de 50 velas del precio, dibujada sobre el precio, con un bloque opcional de suavizado: otra media calculada sobre la propia EMA y, si se elige, bandas de Bollinger. Es una referencia visual de tendencia de medio plazo. No añade señales ni alertas. Categoría 4, Trend.

## Qué dice la fuente

- **Base** `[Aportado]`: según la cabecera del script, el indicador integrado «Moving Average Exponential» de TradingView (plantilla oficial). El único cambio de cálculo es la longitud por defecto, 50.
- **Periodo 50** `[Aportado]`: sin fuente confirmada. El código que Antonio tenía en TradingView mencionaba, sin verificar, a Alex Ruiz como posible origen; la v0.1.1.0 no lo cita.
- **No es de Cava:** según el código anterior, ni «El arte de especular» ni «Sistemas de especulación en bolsa» definen una EMA de 50 general sobre el precio. Esa afirmación y la referencia a una media de 25/50 días del bono americano (SEB, «p. ~144») salen del comentario del código anterior y no se han comprobado contra el libro `[Por confirmar]`.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Longitud de la EMA | 50 velas (mínimo 1) | `[Aportado]`: sin fuente confirmada |
| Serie de precio | El cierre, ajustable | De la plantilla de TradingView |
| Desplazamiento | 0 (de −500 a 500) | De la plantilla de TradingView |
| Suavizado: longitud | 14 | De la plantilla de TradingView |
| Bandas: multiplicador | 2,0 (de 0,001 a 50) | De la plantilla de TradingView |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea azul «EMA» | La EMA de 50 velas del precio elegido (el cierre de serie) | Referencia de soporte o resistencia dinámica de fondo, más lenta que una EMA de 20 y más rápida que una SMA de 200 `[Elaboración]` |
| Línea amarilla «Media sobre la EMA» (opcional) | Una media del tipo elegido, calculada sobre la propia EMA | Suaviza la lectura de la EMA. No se desplaza con el Desplazamiento |
| Líneas verdes «Banda superior» y «Banda inferior» y relleno «Relleno de bandas» (opcionales) | La media de suavizado, que es una SMA, más y menos la desviación típica de la EMA por el multiplicador. Solo con «SMA + Bandas de Bollinger» | Se separan cuando la EMA ha variado mucho en las últimas velas del suavizado. No miden la dispersión del precio |

## Cómo funciona, paso a paso

1. Calcula la EMA de la serie elegida (el cierre) con la longitud elegida (50).
2. Si Tipo no es «Ninguna», calcula sobre esa EMA una media del tipo elegido, con la longitud de suavizado (14).
3. Si Tipo es «SMA + Bandas de Bollinger», calcula la desviación típica de la EMA en las velas de la longitud de suavizado, la multiplica por el multiplicador de bandas y la suma y resta a la media de suavizado. Rellena entre las dos bandas.
4. El Desplazamiento mueve solo la línea de la EMA. La media de suavizado y las bandas no se desplazan.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| El precio está por encima de la EMA | La EMA hace de soporte dinámico de fondo `[Elaboración]` | Una señal de compra |
| El precio está por debajo de la EMA | La EMA hace de resistencia dinámica de fondo `[Elaboración]` | Una señal de venta |
| La EMA sube o baja con claridad | La dirección de la tendencia de medio plazo `[Elaboración]` | Que la tendencia vaya a continuar |
| Las bandas están muy abiertas | La EMA ha cambiado mucho en las últimas velas del suavizado | Mucha dispersión del precio: las bandas se calculan con la desviación típica de la EMA, no con la del precio |

## Cuándo usarlo y cuándo no

- **Sí:** como referencia visual de fondo del medio plazo.
- **No:** como señal de entrada o de salida por sí sola: el script no añade señales propias. Tampoco como regla de Cava.
- **Mal uso frecuente** `[Elaboración]`: leer las bandas como dispersión del precio; esperar que el Desplazamiento mueva también el suavizado.

## Qué NO dice

- No da entradas ni salidas y no tiene alertas.
- El periodo 50 no tiene respaldo de fuente.
- No tiene respaldo de Cava.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Creación, a partir del código legado 0.1.0.0 (nombre GEN72) |
| 0.2.0.0 | 2026-11-21 | Plantilla estándar para el código legado 0.1.0.0 |
| 0.3.0.0 | 2026-11-22 | Renombrada a GEN44 Trend. Describe el código 0.1.1.0. Las citas del código anterior (Cava, SEB p. ~144) siguen sin comprobar contra el libro |
| 0.4.0.0 | 2026-11-22 | Script declarado estable y probado en TradingView por Antonio; campos «Probada» y «Validada en conector»; pasa a la carpeta del repo en Drive |
